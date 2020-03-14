---
title: onResourceStarting
weight: 548
---

在资源启动之前调用。可以取消此事件以阻止此资源启动。

参数
----------

```
string resourceName
```

- resourceName: 试图启动的资源的名称。

示例
--------
此示例阻止任何名为 'pineapple' 的资源启动。

##### Lua 示例：
```lua
AddEventHandler('onResourceStarting', function(resourceName)
  if resourceName == 'pineapple' then
    CancelEvent()
  end
end)
```

##### C\# 示例：
```csharp
// in the class constructor
EventHandlers["onResourceStarting"] += new Action<string>(OnResourceStarting);

// delegate method
private void OnResourceStarting(string resourceName)
{
  if (resourceName == "pineapple")
  {
    CancelEvent();
  }
}
```

##### JavaScript 示例：
```js
on("onResourceStarting", (resourceName) => {
  if (resourceName === "pineapple") {
    CancelEvent();
  }
});
```
