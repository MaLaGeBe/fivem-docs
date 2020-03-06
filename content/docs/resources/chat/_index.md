---
title: chat
hidden: false
---


## 关于
聊天资源使用基于NUI的界面为FiveM提供自定义聊天功能。
它包含在cfx服务器数据存储库中并在其中维护。

## 输出
_此资源没有任何输出功能。_

## 事件

### 客户端
- [chatMessage](./events/chatMessage) （已弃用，请使用`chat:addMessage`）
- [chat:addMessage](./events/chat-addMessage)
- [chat:addSuggestion](./events/chat-addSuggestion)
- [chat:addSuggestions](./events/chat-addSuggestions)
- [chat:removeSuggestion](./events/chat-removeSuggestion)
- [chat:addTemplate](./events/chat-addTemplate)
- [chat:clear](./events/chat-clear)

### 服务端
- [chatMessage](./events/chatMessage)
