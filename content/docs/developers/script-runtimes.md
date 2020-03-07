---
title: 脚本运行环境
weight: 930
description: >
  描述对fxOM脚本运行环境的支持。
---

CitizenFX支持可插入脚本运行环境。这些运行环境被实现为CitizenFX组件 (`code/components/`)，实现了在 `fxScripting.idl` 中定义的 `fxOM` (CitizenFX对象模型)接口。

在撰写本文时，使用的特定接口是：

|             接口           |                         目的                                 |
| -------------------------- | ------------------------------------------------------------ |
| IScriptRuntime             | 脚本运行时的基本接口。公开基本的生命周期管理功能。           |
| IScriptTickRuntime         | 允许为需要定期运行的运行时公开 Tick 函数。                   |
| IScriptEventRuntime        | 允许公开一个触发事件函数(TriggerEvent)来处理传入的脚本事件。 |
| IScriptRefRuntime          | 允许公开可以调用，复制和克隆的函数引用。                     |
| IScriptFileHandlingRuntime | 允许将脚本运行时标记为处理特定文件。                         |

另外，还有一个主机接口：`IScriptHost`，它将被传递给 `IScriptRuntime::Create`.

## 接口参考

### IScriptRuntime

#### Create

```cs
void Create(in IScriptHost scriptHost);
```

创建脚本运行时时，主机将调用此方法。 通过的脚本主机会保存。

#### Destroy

```cs
void Destroy();
```

当脚本运行时即将销毁时，主机将调用此方法。

#### GetParentObject

```cs
void* GetParentObject(); // direct return value, not result_t
```

这应该返回由 `SetParentObject` 设置的对象。

#### SetParentObject

```cs
void SetParentObject(void* object); // direct return value, not result_t
```

这将设置父对象。这通常是本机的 `fx::Resource*`，可能与C++中实现的运行环境有关。

#### GetInstanceId

```cs
int GetInstanceId(); // direct return value, not result_t
```

这将返回运行时在初始化时创建的随机实例ID。

### IScriptTickRuntime

#### Tick

```cs
void Tick();
```

主机每隔一帧调用一次。

### IScriptEventRuntime

#### TriggerEvent

```cs
void TriggerEvent(in char* eventName, in char* argsSerialized, in uint32_t serializedSize, in char* sourceId);
```

TriggerEvent is called by the host whenever an event has been triggered. `eventName` contains the name of the executed event,
`argsSerialized` and `serializedSize` indicate the argument array (serialized using the common serialization convention, see the 'conventions' section), and
`sourceId` contains a string identifying the source of the event.

### IScriptRefRuntime

A 'ref' is a function reference, which is used to allow other resources (or the host) to invoke delegates/closures in the script runtime.
Each ref is identified by an integer on resource level, in the host it is qualified with the resource name, instance ID and the ref index.
Refs should not be reference counted by index, each creation should be paired with a single deletion.

#### CallRef

```cs
void CallRef(in int32_t refIdx, in char* argsSerialized, in uint32_t argsSize, out char* retvalSerialized, out uint32_t retvalSize);
```

CallRef is called by the host when a reference should be invoked. `refIdx` contains the ref to call, `argsSerialized`/`argsSize` contain the argument array, and `retvalSerialized` and `retvalSize` should contain the return value array upon completion.

#### DuplicateRef

```cs
void DuplicateRef(in int32_t refIdx, out int32_t newRefIdx);
```

DuplicateRef should return a new reference index referencing the same internal function object as `refIdx` into `newRefIdx`.

#### RemoveRef

```cs
void RemoveRef(in int32_t refIdx);
```

RemoveRef should delete the reference identified by `refIdx`.

### IScriptFileHandlingRuntime

#### HandlesFile

```cs
int32_t HandlesFile(in char* scriptFile);
```

Should return whether or not the specified file should be handled by this runtime.

#### LoadFile

```cs
void LoadFile(in char* scriptFile);
```

This function should load the file in the runtime.

### IScriptHost

#### InvokeNative

```cs
void InvokeNative(inout NativeCtx context);
```

Invokes a native function. `nativeIdentifier` should contain the native function identifier, `numArguments` the amount of arguments, and `arguments` the specific function arguments following the RAGE native ABI.

Any result, for natives that return any, will be returned in the first argument fields in the context.

#### OpenSystemFile

Returns a stream referencing the specified file name in the system VFS.

#### OpenHostFile

Returns a stream referencing the specified file name, relative to the host path (`resources:/resourceName/`).

#### CanonicalizeRef

#### ScriptTrace

### IScriptHostWithResourceData

This can be obtained using QueryInterface on the IScriptHost.

#### GetResourceName

Returns the name of the parent resource.

#### GetNumResourceMetaData

This function should not be used, instead the native {{<native_link "GET_NUM_RESOURCE_METADATA">}} should be used.

#### GetResourceMetaData

This function should not be used, instead the native {{<native_link "GET_RESOURCE_METADATA">}} should be used.

### IScriptHostWithManifest

This can be obtained using QueryInterface on the IScriptHost.

#### IsManifestVersionBetween

```cs
bool IsManifestVersionBetween(guid_t* lowerBound, guid_t* upperBound);
```

Returns whether or not the host resource's manifest version is within a specific range of GUIDs (`lowerBound <= guid < upperBound`).

If one of the GUIDs is the null GUID, only tests if the version is greater/less then the other GUID.

## Conventions

### Serialization

序列化使用MessagePack进行，并为委托/功能引用使用特定的扩展ID。
