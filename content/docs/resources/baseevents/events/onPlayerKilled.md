---
title: onPlayerKilled
---

事件名称
----------
```
baseevents:onPlayerKilled
```

参数
----------

```
player killerID, array deathData
```

- **killerID**: 杀死玩家的玩家客户端ID
- **deathData**: 一个包含以下内容的数组：
    - **(int) killerType**: 杀死玩家的ped的pedType。 （有关可能的pedType值，请参见下面的屏幕截图。）
    - **(hash) weaponHash**: 杀死玩家的武器哈希值。
    - **(bool) killerInVeh**: 一个布尔值，指示凶手是否在车上。
    - **(int) killerVehSeat**: 凶手所在的座位号。
    - **(string) killerVehName**: 凶手所在的车辆的显示名称（例如：'Adder'）。
    - **(array) deathCoords**: 包含玩家死亡地点的x、y、z坐标的数组。

##### Ped types
![](/ped_types.png)

示例
--------

TODO


<!-- TriggerEvent('baseevents:onPlayerKilled', killerid, {killertype=killertype, weaponhash = killerweapon, killerinveh=killerinvehicle, killervehseat=killervehicleseat, killervehname=killervehiclename, killerpos=table.unpack(GetEntityCoords(ped))}) -->