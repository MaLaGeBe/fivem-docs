---
title: chatMessage
---

## 关于
此事件在客户端和服务器中均可用。
在客户端中，此事件 **已弃用**！请使用 [chat:addMessage](../chat-addMessage) 代替。
在客户端中触发此事件使您可以向该客户端发送聊天消息。
在服务器中侦听此事件使您可以读取/记录/回复消息。

## 事件名称
```
chatMessage
```

参数
----------

##### 客户端：
```
string author, array color, string text
```
- **author**: 发送消息的玩家名称。
- **color**: 颜色数组。 颜色语法：`{255, 255, 255} ( {r, g, b} )`
- **text**: 消息内容

##### 服务端：
```
source, string author, string text
```
- **source**: The source of the chat message
- **author**: 发送消息的玩家名称。
- **text**: 消息内容


示例
--------

##### 服务端 JS 示例：
```javascript
onNet('chatMessage', (src, author, text)=>{
    // Log the message
    let ts = new Date().toLocaleString();
    console.log(`[${ts}] ${author}: ${text}`);

    //Check for '/ping' and reply with 'Pong!'
    if(src && text.startsWith('/ping')){
        setImmediate(()=>{
            emitNet('chat:addMessage', src, {
                color: [255, 20, 147],
                args: ["Server", "Pong!"]
            });
        })
    }
})
```
**注意：** 我们使用的是`setImmediate()`，否则该回复(`Pong!`)将在命令(`/ping`)之前显示在聊天框中
