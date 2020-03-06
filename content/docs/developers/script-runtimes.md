---
title: 脚本运行
weight: 930
description: >
 描述对fxOM脚本运行时的支持。
---

CitizenFX支持可插入脚本运行时。 这些运行时被实现为CitizenFX组件（代码/组件/），实现了在fxScripting.idl中定义的fxOM（CitizenFX对象模型）接口。

在撰写本文时，使用的特定的接口格式是：

|           接口             |                                        目的                                      |
| -------------------------- | -------------------------------------------------------------------------------- |
| IScriptRuntime             | Base interface for script runtimes. Exposes basic lifetime management functions. |
| IScriptTickRuntime         | Allows exposing a Tick function for runtimes that need to run periodically.      |
| IScriptEventRuntime        | Allows exposing a TriggerEvent function to handle incoming script events.        |
| IScriptRefRuntime          | Allows exposing function references that can be called, duplicated and cloned.   |
| IScriptFileHandlingRuntime | Allows to mark a script runtime as handling specific files.                      |

另外，还有一个主机接口：“ IScriptHost”，它将被传递给“ IScriptRuntime :: Create”。

## Interface reference

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

这应该返回由SetParentObject设置的对象。

#### SetParentObject

```cs
void SetParentObject(void* object); // direct return value, not result_t
```

这将设置父对象。 这通常是本机的`fx :: Resource *`，可能与C ++中实现的运行时有关。

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

每当触发事件时，主机就会调用TriggerEvent。 “ eventName”包含已执行事件的名称，
argsSerialized和serializedSize表示参数数组（使用通用序列化约定进行序列化，请参见“常规”部分），以及
sourceId包含一个字符串，用于标识事件的来源。

### IScriptRefRuntime

“ref”是一个功能引用，用于允许其他资源（或主机）在脚本运行时中调用委托/关闭。
每个引用在资源级别上由一个整数标识，在主机中使用资源名称，实例ID和引用索引对其进行限定。
引用不应按索引进行引用计数，每个创建都应与单个删除配对。

#### CallRef

```cs
void CallRef(in int32_t refIdx, in char* argsSerialized, in uint32_t argsSize, out char* retvalSerialized, out uint32_t retvalSize);
```

调用引用时，主机将调用CallRef。 refIdx包含要调用的ref，argsSerialized / argsSize包含参数数组，retvalSerialized和retvalSize在完成时应包含返回值数组。

#### DuplicateRef

```cs
void DuplicateRef(in int32_t refIdx, out int32_t newRefIdx);
```

DuplicateRef应该返回一个新的引用索引，该引用将与refIdx相同的内部函数对象引用到newRefIdx中。

#### RemoveRef

```cs
void RemoveRef(in int32_t refIdx);
```

RemoveRef应该删除由refIdx标识的引用。

### IScriptFileHandlingRuntime

#### HandlesFile

```cs
int32_t HandlesFile(in char* scriptFile);
```

应该返回此运行时是否应处理指定的文件。

#### LoadFile

```cs
void LoadFile(in char* scriptFile);
```

此函数应在运行时加载文件。

### IScriptHost

#### InvokeNative

```cs
void InvokeNative(inout NativeCtx context);
```

调用本机函数。 “ nativeIdentifier”应包含本机函数标识符，“ numArguments”应包含参数数量，“ arguments”应包含在RAGE本机ABI之后的特定功能参数。

对于返回任何结果的本机，任何结果都将在上下文的第一个参数字段中返回。

#### OpenSystemFile

返回引用系统VFS中指定文件名的流。

#### OpenHostFile

返回相对于主机路径（`resources：/ resourceName /`）引用指定文件名的流。

#### CanonicalizeRef

#### ScriptTrace

### IScriptHostWithResourceData

这可以使用IScriptHost上的QueryInterface获得。

#### GetResourceName

返回父资源的名称。

#### GetNumResourceMetaData

不应使用此功能，而应使用本机中的 {{<native_link "GET_NUM_RESOURCE_METADATA">}} .

#### GetResourceMetaData

不应使用此功能，而应使用本机中的  {{<native_link "GET_RESOURCE_METADATA">}} .

### IScriptHostWithManifest

这可以使用IScriptHost上的QueryInterface获得。

#### IsManifestVersionBetween

```cs
bool IsManifestVersionBetween(guid_t* lowerBound, guid_t* upperBound);
```

返回主机资源的清单版本是否在GUID的特定范围内 (`lowerBound <= guid < upperBound`).

如果其中一个GUID为空GUID，则仅测试版本是否大于/小于另一个GUID。

## Conventions

### Serialization

序列化使用MessagePack进行，并为委托/功能引用使用特定的扩展ID。
