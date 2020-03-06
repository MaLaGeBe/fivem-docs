---
title: chat:addSuggestion
---

## 关于
触发此事件可使您向聊天框添加命令建议。

## 事件名称
```
chat:addSuggestion
```

参数
----------

```
string commandName, string commandDescription, object commandParameters
```

示例
--------
T他的示例为`/command`命令添加了命令建议。

##### Lua 示例：
```lua
-- Note, the command has to start with `/`.
TriggerEvent('chat:addSuggestion', '/command', 'help text', {
    { name="paramName1", help="param description 1" },
    { name="paramName2", help="param description 2" }
})
```

##### C\# 示例：
```csharp
TriggerEvent("chat:addSuggestion", "/command", "help text", new[]
{
    new { name="paramName1", help="param description 1" },
    new { name="paramName2", help="param description 2" }
});
```

##### JS 示例：
```js
setImmediate(() => {
  emit('chat:addSuggestion', '/command', 'help text', [
    {name:"paramName1", help:"param description 1"},
    {name:"paramName1", help:"param description 2"}
  ]);
});
```

## 示例结果：
![screenshot-1](/chat_addSuggestion.png)
