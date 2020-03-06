---
title: chat:removeSuggestion
---

## 关于
触发此操作可以删除指定命令的所有现有命令建议。

## 事件名称
```
chat:removeSuggestion
```

参数
----------

```
string commandName
```

示例
--------
本示例删除了通过[chat:addSuggestion](../chat-addSuggestion)示例创建的建议。

##### Lua 示例：
```lua
TriggerEvent('chat:removeSuggestion', '/command')
```

##### C\# 示例：
```csharp
TriggerEvent("chat:removeSuggestion", "/command");
```
