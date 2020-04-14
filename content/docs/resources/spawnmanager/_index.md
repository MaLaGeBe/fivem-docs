---
title: spawnmanager
---

## 关于
spawnmanager是一个基本资源，用于处理生成玩家。它允许你选择何时何地生成玩家，也可以控制他们如何重生。

Spawnmanager包含在 [cfx-server-data](https://github.com/citizenfx/cfx-server-data) 存储库中并进行维护。

Map resources for  will have their spawnpoints loaded and usable in spawnmanager, as long as they are started *after* spawnmanager. 

## Exports

### Client
- [spawnPlayer](./functions/spawnPlayer)
- [addSpawnPoint](./functions/addSpawnPoint)
- [removeSpawnPoint](./functions/removeSpawnPoint)
- [loadSpawns](./functions/loadSpawns)
- [setAutoSpawn](./functions/setAutoSpawn)
- [setAutoSpawnCallback](./functions/setAutoSpawnCallback)
- [forceRespawn](./functions/forceRespawn)

## Events

### Client
- [playerSpawned](./events/playerSpawned)