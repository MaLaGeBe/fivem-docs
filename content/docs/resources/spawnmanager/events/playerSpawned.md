---
title: playerSpawned
---

参数
----------

```
object spawnInfo
```

- **spawnInfo**: 包含以下信息的对象：
    - **(float) x**: 生成玩家位置的x坐标。
    - **(float) y**: 生成玩家位置的y坐标。
    - **(float) z**: 生成玩家位置的z坐标。
    - **(float) heading**: 生成时玩家时面向位置。
    - **(int) idx**: 生成点索引。
    - **(Hash) model**: 生成玩家的ped模型哈希值。
    - **(bool) skipFade**: 玩家生成时是否跳过淡入淡出。

示例
--------

```js
{
    z: 111.5291,
    y: 197.7201,
    x: 466.8401,
    heading: 291.71,
    idx: 6,
    model: 1631478380
}
```
