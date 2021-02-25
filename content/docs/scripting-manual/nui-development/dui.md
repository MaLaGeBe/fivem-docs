---
title: 直接渲染的UI
weight: 442
---

在FiveM中，您还可以将NUI渲染到运行时纹理，该纹理称为“直接NUI”的DUI。 请参考以下帮助
有了这个：

* {{% native_link "CREATE_DUI" %}}
* {{% native_link "CREATE_RUNTIME_TEXTURE_FROM_DUI_HANDLE" %}}
* {{% native_link "DESTROY_DUI" %}}
* {{% native_link "GET_DUI_HANDLE" %}}
* {{% native_link "IS_DUI_AVAILABLE" %}}
* {{% native_link "SEND_DUI_MESSAGE" %}}
* {{% native_link "SEND_DUI_MOUSE_DOWN" %}}
* {{% native_link "SEND_DUI_MOUSE_MOVE" %}}
* {{% native_link "SEND_DUI_MOUSE_UP" %}}
* {{% native_link "SEND_DUI_MOUSE_WHEEL" %}}
* {{% native_link "SET_DUI_URL" %}}

本机文档包含有关每一项的信息，但是这里有一些创造性的用例：

* Rendering in 2D space using {{% native_link "DRAW_SPRITE" %}}
* Rendering to a game render target object using similar natives.
* Rendering arbitrarily in world space using a specialized Scaleform.
  [Forum topic](https://forum.cfx.re/t/131208)

这可用于使电影屏幕，异步游戏内提示叠加等变得非常简单。