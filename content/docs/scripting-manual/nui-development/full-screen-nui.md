---
title: 全屏NUI
weight: 441
---

NUI的最常见用例是全屏“ UI页面”，该页面覆盖在游戏顶部，可能有也可能没有
输入焦点。 目前，FiiveM和RedM都支持这些功能，它们是基本CitizenFX框架级别的一部分
支持。

以下本机与使用全屏NUI有关：

* {{% native_link "SEND_NUI_MESSAGE" %}}
* {{% native_link "SET_NUI_FOCUS" %}}

## Setting up a fullscreen NUI page
要将全屏NUI页面分配给资源，当前，您需要在页面中指定单个`ui_page`
[resource manifest][resource-manifest] 用于包含UI页面的资源，如下所示：

```lua
-- specify the root page, relative to the resource
ui_page 'main.html'

-- every client-side file still needs to be added to the resource packfile!
files {
    'main.html'
}
```

## Referencing other assets
{{% alert title="Warning" color="warning" %}}
请注意，NUI资源引用**要求**您的资源名称要小写！ 这是由于DNS名称
限制。
{{% /alert %}}

NUI系统为资源文件注册一个`nui://`协议范围。 因此，您可以引用资源中的文件
如下：

```html
<script type="text/javascript" src="nui://my-resource/production.js" async></script>
```

## Developer tools
只要游戏运行，CEF远程调试工具就会在[http://localhost:13172/](http://localhost:13172/)上公开
运行。 您可以使用任何基于Chromium的浏览器轻松访问这些工具。

Alternately, it can be opened using the `nui_devTools` command in the game's <kbd>F8</kbd> console.

## NUI focus
There's a limited focus stack for NUI resources, you can set focus to the **current** resource using the
{{% native_link "SET_NUI_FOCUS" %}} native, which will set keyboard focus and/or mouse cursor focus depending on the
provided arguments.

最近关注的资源将在焦点堆栈的顶部排序，并且当前已实现资源
作为全屏iframe：这意味着没有跨资源点击。

## NUI messages
You can send a [message][mdn-messages] to the current resource's NUI page using <span class="l-no-lua">the {{% native_link "SEND_NUI_MESSAGE" %}}
native</span><span class="l-raw">, or if using Lua, </span><span class="l-lua">the convenience wrapper
[SendNUIMessage][send-nui-message] which encodes a JSON string for you.</span><span class="l-no-raw l-no-lua">.</span>

例如:

<div class="l-lua">

```lua
-- Lua
SendNUIMessage({
    type = 'open'
})
```

</div>

<div class="l-js">

```js
// JS
SendNuiMessage(JSON.stringify({
    type: 'open'
}))
```

</div>

<div class="l-cs">

```csharp
// C#, assumes Newtonsoft.Json PCL version is referenced
SendNuiMessage(JsonConvert.SerializeObject(new
{
    type = "open"
}));
```

</div>

```js
// browser side
window.addEventListener('message', (event) => {
    if (event.data.type === 'open') {
        doOpen();
    }
});
```

[mdn-messages]: https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage#The_dispatched_event
[send-nui-message]: /docs/scripting-reference/runtimes/lua/functions/SendNUIMessage
[resource-manifest]: /docs/scripting-reference/resource-manifest/resource-manifest
