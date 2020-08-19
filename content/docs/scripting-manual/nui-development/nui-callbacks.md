---
title: NUI callbacks
weight: 443
---

NUI还可以使用所谓的'NUI 回调'将调用发送回游戏。目前只有在
Lua，可以使用其他语言，但需要一些[tricky workaround][workaround]，因为这些是预先设置的函数
codegen中的引用。

<!-- #GAMETODO: actually fix that? -->

{{% alert theme="warning" %}}注意，NUI回调**要求**您的资源名称小写！这是由于DNS
名称限制。{{% /alert %}}

通常，您将在Lua中使用[RegisterNUICallback][registernuicallback]函数，
{{<native_link "REGISTER_NUI_CALLBACK_TYPE">}}本机以及其他语言的事件处理程序。

两者的工作原理非常相似，我们将在下面描述两者：

## Registering a NUI callback in Lua
```lua
RegisterNUICallback('getItemInfo', function(data, cb)
    -- POST数据自动解析为JSON
    local itemId = data.itemId

    if not itemCache[itemId] then
        cb({ error = 'No such item!' })
        return
    end

    -- 回调响应数据也是
    cb(itemCache[itemId])
end)
```

## Registering a NUI callback in C#/JS
```js
// JS
RegisterNuiCallbackType('getItemInfo') // 注册类型

// 注册事件名称
on('__cfx_nui:getItemInfo', (data, cb) => {
    const itemId = data.itemId;

    if (!itemCache[itemId]) {
        cb({ error: 'No such item!' });
        return;
    }

    cb(itemCache[itemId]);
});
```

```csharp
// C#
RegisterNuiCallbackType("getItemInfo"); // 注册类型

// register the event handler with manual marshaling
EventHandlers["__cfx_nui:getItemInfo"] += new Action<IDictionary<string, object>, CallbackDelegate>((data, cb) =>
{
    // 从对象获取itemId
    // 或者，您可以使用“dynamic”并依赖于DLR
    if (data.TryGetValue("itemId", out var itemIdObj))
    {
        cb(new 
        {
            error = "Item ID not specified!"
        });

        return;
    }

    // cast away
    var itemId = (itemIdObj as string) ?? "";

    // same as above
    if (!ItemCache.TryGetValue(itemId, out Item item))
    {
        cb(new 
        {
            error = "No such item!"
        });

        return;
    }

    cb(item);
});
```

## Invoking the NUI callback
```js
// browser-side JS
fetch(`https://${GetParentResourceName()}/getItemInfo`, {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json; charset=UTF-8',
    },
    body: JSON.stringify({
        itemId: 'my-item'
    })
}).then(resp => resp.json()).then(resp => console.log(resp));
```

为了防止请求暂停，您**必须**始终返回回调-即使只包含一个空的
对象，或`{"ok":true}`，或类似的。

[registernuicallback]: /docs/scripting-reference/runtimes/lua/functions/RegisterNUICallback/
[workaround]: https://github.com/citizenfx/fivem/blob/d911ecf638337c7c61fc6728110c92d84a217156/data/shared/citizen/scripting/lua/scheduler.lua#L958
