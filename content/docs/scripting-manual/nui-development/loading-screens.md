---
title: 服务端加载界面
weight: 444
---

一个特殊的NUI帧是名为`loadingScreen`的帧，它在FiveM加载期间显示，而不是默认的
加入服务器后，客户端加载屏幕或游戏加载屏幕。

它的指定类似于在[resource manifest][resource-manifest]中使用`loadscreen`的`ui_page`：

```lua
loadscreen 'load.html'

file 'load.html'
```


```lua
loadscreen 'https://my-server.example.com/loadscreen/'
```

## Lifetime
默认情况下，加载屏幕将一直显示，直到调用{{<native_link "SHUTDOWN_LOADING_SCREEN">}}。但是，你也可以

通过在资源清单中设置`loadscreen_manual_shutdown 'yes'`指令，手动控制退出。
执行此操作时，脚本启动后（游戏加载并连接到网络后），以下本机将可用：

<!-- #GAMETODO: maybe some sort of comms during load screen would be neat? or correlation to server state? -->

* {{<native_link "SEND_LOADING_SCREEN_MESSAGE">}}
* {{<native_link "SHUTDOWN_LOADING_SCREEN_NUI">}}

这可以用来，比如说，将一个自定义淡出效果从加载屏幕添加到游戏内视图，或者集成NUI事件
与早期游戏生成选择用户界面。

[resource-manifest]: /docs/scripting-reference/resource-manifest/resource-manifest