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

## Handover data
Server scripts can specify data pairs to send to the client loading screen using the `handover` function in the playerConnecting
event. This data will be passed to the loading screen in the `window.nuiHandoverData` property.

In addition to data specified by the server, a field named `serverAddress` is also added with the current IP/port used for
the client->server connection.

### Example
```lua
-- Server script
AddEventHandler('playerConnecting', function(_, _, deferrals)
    local source = source

    deferrals.handover({
        name = GetPlayerName(source)
    })
end)
```

```html
<!-- loading screen page -->
<h1 id="namePlaceholder">Welcome, <span></span></h1>

<script type="text/javascript">
window.addEventListener('DOMContentLoaded', () => {
    console.log(`You are connecting to ${window.nuiHandoverData.serverAddress}`);

    // a thing to note is the use of innerText, not innerHTML: names are user input and could contain bad HTML!
    document.querySelector('#namePlaceholder > span').innerText = window.nuiHandoverData.name;
});
</script>
```

## Lifetime
By default, the loading screen will show until {{% native_link "SHUTDOWN_LOADING_SCREEN" %}} is called. However, you can also
manually control exit lifetime by setting the `loadscreen_manual_shutdown 'yes'` directive in your resource manifest.

通过在资源清单中设置`loadscreen_manual_shutdown 'yes'`指令，手动控制退出。
执行此操作时，脚本启动后（游戏加载并连接到网络后），以下本机将可用：

* {{% native_link "SEND_LOADING_SCREEN_MESSAGE" %}}
* {{% native_link "SHUTDOWN_LOADING_SCREEN_NUI" %}}

这可以用来，比如说，将一个自定义淡出效果从加载屏幕添加到游戏内视图，或者集成NUI事件
与早期游戏生成选择用户界面。

[resource-manifest]: /docs/scripting-reference/resource-manifest/resource-manifest