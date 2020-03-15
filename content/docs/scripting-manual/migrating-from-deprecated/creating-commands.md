---
title: 创建命令
weight: 432
---

<!--
## The `chatMessage` method (deprecated)
In the past, people have used the `chatMessage` event to detect when a chat message is being sent. After that, they would use a string split method to see if the first argument in that table (of split strings) contained a command.

### Example
```lua
AddEventHandler("chatMessage", function(source, name, message)
    if string.sub(message, 1, 1) == "/" then
        sm = stringsplit(message, " ")
        if sm[1] == "/commandName" then
            print("Command was entered.")
        end
    end
end)

function stringsplit(inputstr, sep)
    if sep == nil then
        sep = "%s"
    end

    local t = {}
    for str in string.gmatch(inputstr, "([^" .. sep .. "]+)") do
        t[i] = str
        i = i + 1
    end
    return t
end
```
-->

## RegisterCommand

建议**一直**使用此功能(而不是 `chatMessage`!)，因为它允许使用集成的ACL系统以及其他核心功能（自动完成，控制台使用等）。 这个本地包括3个参数(`commandName`[string], `handler`[func] 和 `restricted`[boolean]).

### Example
```lua
RegisterCommand("commandName", function(source --[[ this is the player ID (on the server): a number ]], args --[[ this is a table of the arguments provided ]], rawCommand --[[ this is what the user entered ]])
    if source > 0 then
        print("You are not console.")
    else
        print("This is console!")
    end
end, true) -- 此值表示用户无法执行命令，除非他们的标识符具有 'command.commandName'  ACL对象。
```

可以在相应的文档找到更多示例 [Lua](../../introduction/creating-your-first-script) 和 [C#](../../introduction/creating-your-first-script-csharp) 的介绍.
