---
title: onResourceStart
weight: 547
---

在资源启动时调用。

参数
----------

```
string resourceName
```

- resourceName: 启动的资源的名称。

示例
--------
此示例在启动时打印当前资源的名称。

##### Lua 示例：
```lua
AddEventHandler('onResourceStart', function(resourceName)
  if (GetCurrentResourceName() ~= resourceName) then
    return
  end
  print('The resource ' .. resourceName .. ' has been started.')
end)
```

##### C\# 示例：
```csharp
// in the class constructor
EventHandlers["onResourceStart"] += new Action<string>(OnResourceStart);

// delegate method
private void OnResourceStart(string resourceName)
{
  if (GetCurrentResourceName() != resourceName) return;

  Debug.WriteLine($"The resource {resourceName} has been started.");
}
```

##### JavaScript 示例：
```js
on("onResourceStart", (resourceName) => {
  if(GetCurrentResourceName() != resourceName) {
    return;
  }

  console.log(`The resource ${resourceName} has been started.`)
});
```
