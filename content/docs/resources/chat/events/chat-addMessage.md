---
title: chat:addMessage
---

## 关于
触发此事件使您可以向此客户端发送聊天消息。
消息对象结构：

```lua
message = {
  template = template,
  color = color,
  multiline = true,
  args = {author, otherArgs...}
}
```

## 事件名称
```
chat:addMessage
```

参数
----------

```
object message
```

示例
--------

本示例从客户端脚本向本地玩家发送聊天消息（只有执行客户端会看到此消息）。

##### Lua 示例：
```lua
TriggerEvent('chat:addMessage', {
  color = { 255, 0, 0},
  multiline = true,
  args = {"Me", "Please be careful to not step on too many snails!"}
})
```

##### C\# 示例：
```csharp
TriggerEvent("chat:addMessage", new
{
    color = new[] {255, 0, 0},
    multiline = true,
    args = new[] {"Me", "Please be careful to not step on too many snails!"}
});
```

### 示例结果：
![screenshot-1](/chat_addMessage.png)
