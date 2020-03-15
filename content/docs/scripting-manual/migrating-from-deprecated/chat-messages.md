---
title: 创建聊天消息
weight: 431
---

通常在教程和较旧的资源中找到，`chatMessage`事件用于创建聊天消息。 现在不建议使用此方法，建议人们使用`chat:addMessage` 事件。

## chatMessage (The deprecated method)
旧的`chatMessage`事件具有3个参数(`author`[string], `color`[array] 和 `text`[string])

### Example
```lua
TriggerEvent("chatMessage", GetPlayerName(PlayerId()), {255, 255, 255}, "Hello, this is the message that will show in chat.")
```

## `chat:addMessage` (The recommended method)
此事件的对象参数包含3个属性 (`color`[array], `multiline`[boolean] 和 `args`[array])

### Example
```lua
TriggerEvent("chat:addMessage", {
    color = {255, 255, 255},
    multiline = true,
    args = { GetPlayerName(PlayerId()), "Hello, this is the message that will show in chat" }
})
```

有关此事件的更多文档，请看 [`chat:addMessage` section](../../../resources/chat/events/chat-addMessage).
