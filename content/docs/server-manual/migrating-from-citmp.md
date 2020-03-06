---
title: 从CitizenMP.Server迁移
weight: 360
description: >
  有一些古老的服务端？ 这是有关迁移老服务端的指南。
---

### Loading Scripts

`require`不再存在，任何脚本/库都应使用资源清单中的`server_script`指令加载。

例如:

``` lua
server_script "my_script.lua" -- load script
server_script "my_lib.net.dll" -- load a particular assembly into the .net appdomain
server_script "@resource_name/script.lua" -- load a script from another resource
```

要在运行时加载文件，可以使用 [LOAD\_RESOURCE\_FILE]({{<native "LOAD_RESOURCE_FILE">}}) (`LoadResourceFile("resource_name", "file_name")`), 如果它是一个Lua文件，则可以使用。

``` lua
load(...)
```

加载Lua代码，如以下示例所示：

``` lua
function loadLuaFile(resource, file)
    return load(LoadResourceFile(resource, file), file)()
end
```

### String Splitting

`str:Split` 不再存在，您应该为此使用适当的Lua函数。 对于通常复制粘贴的 `stringsplit` 函数，它是：

``` lua
function stringsplit(inputstr, sep)
    if sep == nil then
        sep = "%s"
    end
    local t={} ; i=1
    for str in string.gmatch(inputstr, "([^"..sep.."]+)") do
        t[i] = str
        i = i + 1
    end
    return t
end
```

### Bitwise Operations

Lua 5.3已弃用`bit32`，而CfxLua运行时未启用它。 像大多数其他编程语言一样，按位运算现在也可以使用普通运算符（`＆`，`|`，...）来工作。

### CLR

NeoLua不再使用，因此`clr`命名空间不再存在。 如果需要运行C \＃代码，请使用正常的.NET运行时和服务器导出。

### TempIDs

如果您在执行“ playerConnecting”期间进行了任何特定的按位运算，则假设“ source”值大于0x10000，那么在“ playerConnecting”期间使用函数就不再需要了。
