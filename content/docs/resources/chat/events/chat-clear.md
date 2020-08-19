---
title: chat:clear
---

## 关于
清除聊天消息/历史记录和已发送消息的历史记录缓冲区。

## 事件名称
```
chat:clear
```

参数
----------

此事件没有参数。

示例
--------
这个例子注册了一个清除聊天的 `/clear` 命令。

##### Lua 示例：
```lua
RegisterCommand('clear', function(source, args)
    TriggerEvent('chat:clear')
end, false)
```

##### C\# 示例：
```csharp
// In a method or the class constructor
RegisterCommand("clear", new Action<int, List<object>, string>(source, args, raw) =>
{
    TriggerEvent("chat:clear")
}, false);
```

##### JavaScript Example:
```javascript
RegisterCommand('clear', (source, args) => {
    emit('chat:clear');
}, false);
```
