---
title: 控制台命令
weight: 260
---

客户端命令列表，可用于开发服务器或调试资源问题。可以通过资源添加其他命令；这些只是标准的FiveM命令。

这些命令可以与客户端控制台一起使用，which you can open by pressing F8. 您可以按F8打开。 您也可以根据需要安装其他工具，比如 [VConsole2][vconsole]。这使您可以在游戏外部使用客户端控制台。

### cmdlist
`cmdlist` 命令将列出在客户端（或服务器）上注册的所有命令。它还将输出通过使用`set`、`sets`和`seta`命令设置的变量。

### connect
您可以使用`connect`通过给定的IP地址和端口连接到服务器。

用法：`connect <ip:port>`

示例：`connect 127.0.0.1:30120`

### developer
为开发人员启用一些其他日志记录。 通常不适合普通用户使用。

用法：`developer <true|false>`

### disconnect
`disconnect`将断开您与所连接的当前服务器的连接，并返回到主菜单。

### doshit
内部使用，以测试一些实验功能。 不适合普通用户使用。

### invoke-levelload
`loadlevel`的别名，有关详细信息，请参见[loadlevel](#loadlevel)命令。

### list_aces
<!-- TODO: probably needs a reference to an explanation for ACL stuff -->
列出控制台中的所有ace（访问控制项）。它创建主体和对象之间的关系以及是否允许使用它们的列表。

输出示例：

```
builtin.everyone -> command.freecam = ALLOW
group.admin -> command.testbed = DENY
<rest of the aces...>
```

### list_principals
<!-- TODO: probably needs a reference to an explanation for ACL stuff -->
列出系统中的所有主体，它将打印出其他主体继承的主体的列表。

输出示例：

```
identifier.steam:110000111111111 <- group.admin
identifier.steam:110000111111112 <- group.moderator
<child> <- <parent>
```

左侧是属于右侧父节点的子节点。

### loadlevel
<!-- TODO: Needs an reference on how to use and/or setup the loadlevel command -->
从提供的名称加载级别（或通常称为地图）。

用法：`loadlevel <level_name>`

### modelviewer
允许您通过图形界面加载TXD和可绘制对象。

用法：`modelviewer <true|false>`

### net_maxPackets
一个配置标志，用于告诉客户端它应至少每秒发送多少个数据包。

默认值为50，最小值为1，最大值为每秒200。

用法：`net_maxPackets <number_of_packets>`

### net_showCommands
内部开发工具。 不适合普通用户使用。

### net_statsFile
`net_statsFile` 是用于存储 FiveM 客户端的网络使用/行为指标的命令。

它应跟踪 ping，接收到的数据包和字节，发送的数据包和字节以及路由包的数量等度量。 所有这些信息将使用 CSV 格式存储在文件中。

用法：`net_statsFile <file_name>`

示例：`net_statsFile metrics.csv` - 这将在 FiveM [application data][faq-data]文件夹中创建一个名为`metrics.csv`的 CSV 文件。

### netgraph

`netgraph` 命令将为您提供有关 FiveM 客户端网络使用情况的实时指标。
网络图由一个图和有关网络的基本信息组成：

| 字段名      | 描述                                   |
| ----------- | -------------------------------------- |
| ping        | 从服务器获得响应所需的时间（往返时间） |
| in          | 每秒接收到多少个数据包。               |
| in (bytes)  | 每秒接收多少字节。                     |
| out         | 我们每秒发送多少个数据包。             |
| out (bytes) | 我们每秒发送多少字节。                 |
| rt          | 我们收到了多少个路由数据包。           |
| rd          | 我们已发送多少个路由数据包。           |

该图表示已发送或接收了多少个数据包。

用法：`netgraph <true|false>`

### netobjviewer
启用OneSync时，显示正在通过网络同步的当前节点的列表。

用法：`netobjviewer <true|false>`

### quit
运行 `quit` 命令将强制关闭FiveM客户端。

### r_disableRendering
内部开发工具。 不适合普通用户使用，并且不能在运行时切换。

### resmon
`resmon` 命令将打开资源监视器。资源监视器监视每个资源的CPU使用率和内存使用率，并将其很好地概述。在游戏过程中遇到性能问题时派上用场。

用法：`resmon <true|false>`

### save_gta_cache
<!-- TODO: reference a guide on GTA cache and using it in a resource -->
将指定资源的缓存数据保存到AppData中的CitizenFX目录。 这用于具有大量碰撞或地图文件的资源，以加快玩家的初始加载。

用法：`save_gta_cache <resource name>`

### se_debug
`se_debug` 命令可启用详细的安全功能日志记录（例如ACL）。

用法：`se_debug <true|false>`

有助于了解为什么有些人可以访问某些命令或没有权限， 

输出示例：
```
TEST ACL [system.console -> command.resmon] ACE [system.console command] -> ALLOW
TEST ACL [system.console -> command.resmon] -> ALLOW
```

### set
在客户端上设置一个变量。

用法：`set <key> <value>`

示例：
```
set animal snail

animal
  "animal" is "snail"
  default: ""
  type: string
```

### seta
在客户端上设置一个归档变量。 当前，归档尚未实现。

用法：`seta <key> <value>`

示例：
```
seta food escargot

food
  "food" is "escargot"
  default: ""
  type: string
```

### strdbg
`strdbg` 可用于查看GTA流媒体中当前正在加载的内容，以潜在地发现流式传输某些项目的任何问题，例如，当世界停止加载时。

用法：`strdbg <true|false>`

### strlist
`strlist` 是一个图形界面，显示了在GTA流媒体中注册的条目及其当前状态。

用法：`strlist <true|false>`

### test_ace
测试是否允许委托人访问给定对象。

用法：`test_ace <principal> <object>`

示例：`test_ace group.admin command.adminstuff`

[faq-data]: /docs/support/client-faq#where-is-fivem-installed
[vconsole]: https://forum.fivem.net/t/fivem-update-may-16th-2017/20005
