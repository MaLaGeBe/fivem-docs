---
title: onClientResourceStart
weight: 545
---

在资源启动后调用。

参数
----------

```
string resourceName
```

- resourceName: 启动的资源的名称。

示例
--------
此示例在启动时打印它所在的资源的名称。

##### Lua 示例：
```lua
AddEventHandler('onClientResourceStart', function (resourceName)
  if(GetCurrentResourceName() ~= resourceName) then
    return
  end
  print('The resource ' .. resourceName .. ' has been started on the client.')
end)
```

##### C\# 示例：
```csharp
// In class constructor
EventHandlers["onClientResourceStart"] += new Action<string>(OnClientResourceStart);

// Delegate method
// - assuming `using static CitizenFX.Core.Native.API`
private void OnClientResourceStart(string resourceName)
{
    if(GetCurrentResourceName() != resourceName) return;

    Debug.WriteLine($"The resource {resourceName} has been started on the client.");
}
```

##### JavaScript 示例：
```js
on("onClientResourceStart", (resourceName) => {
  if(GetCurrentResourceName() != resourceName) {
    return;
  }
  console.log(`The resource ${resourceName} has been started on the client.`)
});
```
