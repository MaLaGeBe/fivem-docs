---
title: onClientResourceStop
weight: 546
---

在资源停止后调用。

参数
----------

```
string resourceName
```

- resourceName: 已停止的资源的名称。

示例
--------
此示例打印刚刚停止的资源的名称。

##### Lua 示例：
```lua
AddEventHandler('onClientResourceStop', function (resourceName)
  print('The resource ' .. resourceName .. ' has been stopped on the client.')
end)
```

##### C\# 示例：
```csharp
// In class constructor
EventHandlers["onClientResourceStop"] += new Action<string>(OnClientResourceStop);

// Delegate method
private void OnClientResourceStop(string resourceName)
{
    Debug.WriteLine($"The resource {resourceName} has been stopped on the client.");
}
```

##### JavaScript 示例：
```js
on("onClientResourceStop", (resourceName) => {
  if(GetCurrentResourceName() != resourceName) {
    return;
  }

  console.log(`The resource ${resourceName} has been stopped on the client.`)
});
```
