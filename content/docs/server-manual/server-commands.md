---
title: 服务端命令
weight: 330
description: >
  在服务端控制台中运行的命令列表。
---

<!-- TODO: format this like client commands? -->

可以使用RCon工具直接从服务器控制台GUI（服务器配置）执行控制台命令文件，或者（如果ACE允许资源）[ExecuteCommand]({{<native "EXECUTE_COMMAND">}})函数。

添加自定义RCon命令可以通过使用 [RegisterCommand]({{<native "REGISTER_COMMAND">}})函数来完成。
服务器，或（旧版）`rconCommand`事件。

### `start [resourceName]`

启动参数中指定的资源（如果已停止）。

示例：

    start lambda-menu

### `stop [resourceName]`

停止参数中指定的资源（如果已启动）。

示例：

    stop mymode

### `ensure [resourceName]`

重新启动参数中指定的资源（如果已启动）。 如果不是，则启动参数中指定的资源。

示例：

    ensure my-testing-resource

### `restart [resourceName]`

重新启动参数中指定的资源（如果已启动）。

示例：

    restart lambda-menu

### `refresh`

重新扫描*resources*文件夹并加载其中的所有\_\_resource.lua文件，使新资源可用于使用 [start](#start "wikilink")开始。

示例：

    refresh


### `status`

{{% alert theme="info" %}}这是由 **rconlog** 资源提供的。{{% /alert %}}

显示具有其主要标识符，服务器ID，名称，端点和ping的玩家列表。

示例：

    status

### `sv_maxClients [newValue]`

一个控制台变量，它指定服务器通常可以拥有的最大客户端数，为1到64之间的整数。

### `sv_endpointPrivacy [newValue]`

一个布尔变量，如果为true，则从服务器输出的公共报告中隐藏玩家IP地址。

### `sv_hostname [newValue]`

包含服务器主机名的字符串变量。

### `sv_authMaxVariance [newValue]`

**Variance** 是针对给定提供者（即“ steam”，“ ip”或“ ros”）的用户ID更改的可能性。

一个控制台变量，为1-5的整数（默认值1）； 从最小到最有可能改变。

### `sv_authMinTrust [newValue]`

**信任**是指用户的身份 _不太可能_ 被恶意客户端欺骗。

一个控制台变量，它是1-5之间的整数（默认值为5）；从最不可信到最可信（5是外部三方身份验证等方法）。

### `clientkick [id] [reason]`

{{% alert theme="info" %}}这是由**rconlog**资源提供的。{{% /alert %}}

基于指定的原因，从服务器中踢出具有指定服务器ID（如[status](#status "wikilink")中所示）的客户端。

示例：

    clientkick 43 You're a superstitious idiot!

### `say [message]`

{{% alert theme="info" %}}这是由 **chat** 提供的资源. {{% /alert %}}

在聊天室中以 *控制台* 形式发送消息。

示例：

    say Hi, everybody!


### `load_server_icon [fileName.png]`

加载指定的图标并将其设置为服务器图标。该图标必须是96x96 PNG文件。

示例：

```toml
load_server_icon "my-server.png"
```

### `add_ace [principal] [object] [allow|deny]`

将访问控制条目添加到服务器的访问控制列表中。

示例：

```
add_ace group.admin command.potato allow
add_ace identifier.steam:110000112345678 command.apple deny
```

### `add_principal [child_principal] [parent_principal]`

设置一个要从另一个主体继承的主体。

示例：
```toml
# makes identifier.steam:110000112345678 inherit from group.admin
add_principal identifier.steam:110000112345678 group.admin
```

### `remove_ace [principal] [object] [allow|deny]`

从服务器的访问控制列表中删除指定的ACE。

示例：

```
remove_ace identifier.steam:110000112345678 command.apple deny
```

### `remove_principal [child_principal] [parent_principal]`

删除指定的主体继承项。

示例：
```
remove_principal identifier.steam:110000112345678 group.admin
```

### `test_ace [principal] [object]`
测试是否允许委托人访问给定对象。

示例： `test_ace group.admin command.adminstuff`
