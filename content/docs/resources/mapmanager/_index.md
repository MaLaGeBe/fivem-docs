---
title: mapmanager
---

Mapmanager
------
Mapmanager是随附的citizenfx资源，用于处理地图更改，游戏类型以及游戏类型与地图之间的兼容性。




资源结构
------

### 客户端脚本

- mapmanager_client.lua

### 服务端脚本

- mapmanager_server.lua

## 共享脚本

- mapmanager_shared.lua

输出
------

使用 `exports["mapmanger"]:exportname(args)` 调用输出


### getCurrentGameType

返回当前的游戏类型。

参数：
无

```lua
-- mapmanager_server.lua

function getCurrentGameType()
    return currentGameType
end
```

### getCurrentMap

返回当前地图。

参数：
无


```lua
-- mapmanager_server.lua

function getCurrentMap()
    return currentMap
end
```

### changeGameType

更改当前的游戏类型。

参数：
gameType

```lua
-- mapmanager_server.lua

function changeGameType(gameType)
    if currentMap and not doesMapSupportGameType(gameType, currentMap) then
        StopResource(currentMap)
    end

    if currentGameType then
        StopResource(currentGameType)
    end

    StartResource(gameType)
end
```

### changeMap

更改当前地图

参数：
map

```lua
-- mapmanager_server.lua


function changeMap(map)
    if currentMap then
        StopResource(currentMap)
    end

    StartResource(map)
end
```

### doesMapSupportGameType

返回有关地图是否支持游戏类型的布尔变量。

参数：
gameType
map

```lua
-- mapmanager_server.lua

function doesMapSupportGameType(gameType, map)
    if not gametypes[gameType] then
        return false
    end

    if not maps[map] then
        return false
    end

    if not maps[map].gameTypes then
        return true
    end

    return maps[map].gameTypes[gameType]
end
```

### getMaps

返回所有可用地图的表格。

参数：
None

```lua
-- mapmanager_server.lua

function getMaps()
    return maps
end
```

### roundEnded

将结束一个回合。

参数：
None


```lua
-- mapmanager_server.lua

function roundEnded()
    SetTimeout(50, handleRoundEnd)
end
```
