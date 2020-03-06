---
title: 游戏标签
weight: 760
---

![All flags enabled](/HeadDisplayExample2.png "All flags enabled")

**Gamer tag** (also known as **head display**) - 是玩家角色上方的一个UI元素，可以显示文本和各种图标。通过启用部件来执行控制。通常用来显示玩家的名字。

对于每个组件，您可以：显示/隐藏，更改不透明度，更改颜色。

标签组件列表
---------------

| ID  | 名称                      |
|-----|---------------------------|
| 0   | GAMER\_NAME               |
| 1   | CREW\_TAG                 |
| 2   | healthArmour              |
| 3   | BIG\_TEXT                 |
| 4   | AUDIO\_ICON               |
| 5   | MP\_USING\_MENU           |
| 6   | MP\_PASSIVE\_MODE         |
| 7   | WANTED\_STARS             |
| 8   | MP\_DRIVER                |
| 9   | MP\_CO\_DRIVER            |
| 10  | MP\_TAGGED                |
| 11  | GAMER\_NAME\_NEARBY       |
| 12  | ARROW                     |
| 13  | MP\_PACKAGES              |
| 14  | INV\_IF\_PED\_FOLLOWING   |
| 15  | RANK\_TEXT                |
| 16  | MP\_TYPING                |
| 17  | MP\_BAG\_LARGE            |
| 18  | MP\_TAG\_ARROW            |
| 19  | MP\_GANG\_CEO             |
| 20  | MP\_GANG\_BIKER           |
| 21  | BIKER\_ARROW              |
| 22  | MC\_ROLE\_PRESIDENT       |
| 23  | MC\_ROLE\_VICE\_PRESIDENT |
| 24  | MC\_ROLE\_ROAD\_CAPTAIN   |
| 25  | MC\_ROLE\_SARGEANT        |
| 26  | MC\_ROLE\_ENFORCER        |
| 27  | MC\_ROLE\_PROSPECT        |
| 28  | MP\_TRANSMITTER           |
| 29  | MP\_BOMB                  |

简单用法
------------
### Lua
有关更完整的示例，请参阅服务器软件包中包含的`playernames`资源，或该资源的文档。

``` lua
local mpGamerTags = {}

for i = 0, 255 do
  if NetworkIsPlayerActive(i) and i ~= PlayerId() then
    local ped = GetPlayerPed(i)

    -- change the ped, because changing player models may recreate the ped
    if not mpGamerTags[i] or mpGamerTags[i].ped ~= ped then
      local nameTag = ('%s [%d]'):format(GetPlayerName(i), GetPlayerServerId(i))

      if mpGamerTags[i] then
        RemoveMpGamerTag(mpGamerTags[i].tag)
      end

      mpGamerTags[i] = {
        tag = CreateMpGamerTagForNetPlayer(i, nameTag, false, false, '', 0, 0, 0, 0),
        ped = ped
      }
    end

    SetMpGamerTagVisibility(mpGamerTags[i].tag, 4, NetworkIsPlayerTalking(i))
  elseif mpGamerTags[i] then
    RemoveMpGamerTag(mpGamerTags[i].tag)

    mpGamerTags[i] = nil
  end
end
```

例子
-------

### Lua

``` lua
-- 创建玩家信息
local gamerTagId = CreateMpGamerTagForNetPlayer(
  ped, -- Ped to which gamer info will be assigned
  "User name", -- String to display for flag ""
  false, -- pointedClanTag
  false, -- Is R* clan
  "", -- Clantag
  0, -- Clantag flags
  0, -- red
  0, -- green
  0 -- blue
)
```

### C\#

``` csharp
 创建玩家信息
// 假设使用静态 CitizenFX.Core.API;
int gamerTagId = CreateMpGamerTagForNetPlayer(
  ped.Handle, // Ped to which gamer info will be assigned
  "User name", // String to display for flag ""
  false, // pointedClanTag
  false, // Is R* clan
  clanTag,
  0, // Clantag flags
  0, // red
  0, // green
  0  // blue
);
```



切换标志
--------------

### Lua

``` lua
-- 切换组件
SetMpGamerTagVisibility(
  gamerTagId,
  component,
  bool -- Toggle
)
```

### C\#

``` csharp
// 切换标志
SetMpGamerTagVisibility(
  gamerTagId,
  component,
  toggle
);
```



更改标志颜色
---------------------

### Lua

``` lua
-- 更改组件颜色
SetMpGamerTagColour(
  gamerTagId,
  component,
  colour -- 0 - 255
)
```

### C\#

``` csharp
// 更改组件颜色
Function.Call(
  (Hash)0x613ED644950626AE,
  (int)gamerTagId,
  (int)component,
  (int)colour // 0 - 255
);
```



更改标志的不透明度
----------------------

### Lua

``` lua
-- 更改组件的不透明度
SetMpGamerTagAlpha(
  gamerTagId,
  component,
  opacity -- 0 - 255
)
```

### C\#

``` csharp
// 更改标志的不透明度
Function.Call(
  (Hash)0xD48FE545CD46F857,
  (int)gamerTagId,
  (int)component,
  (int)opacity // 0 - 255
);
```


特殊标志控件
----------------------

### Wanted level

对于**WantedStar**标志，您可以设置将在星形图标内部显示的数字：### Lua

``` lua
-- 设置将在想要的星形图标内设置的数字
SetMpGamerTagWantedLevel(
  gamerTagId,
  wantedLevel -- 0 - 5
)
```

### C\#

``` csharp
// 设置将在想要的星形图标内设置的数字
Function.Call(
  Hash._SET_HEAD_DISPLAY_WANTED,
  (int)gamerTagId,
  (int)wantedLevel // 0 - 5
);
```

### Health bar colour

默认情况下，健康栏的不透明度为0。 运行状况栏的颜色使用其自己的本机更改：### Lua

### Lua

``` lua
-- 更改健康栏颜色
SetMpGamerTagHealthBarColor(
  gamerTagId,
  colour -- 0 - 255
)
```

### C\#

``` csharp
// 更改健康栏颜色
Function.Call(
  (Hash)0x3158C77A7E888AB4,
  (int)gamerTagId,
  (int)colour // 0 - 255
);
```
