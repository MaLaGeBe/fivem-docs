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

{{% alert theme="info" %}}This is provided by the **rconlog** resource. {{% /alert %}}

Shows a list of players with their primary identifier, server ID, name, endpoint, and ping.

Example:

    status

### `sv_maxClients [newValue]`

A console variable that specifies the maximum amount of clients that the server can normally have, as an integer from 1 to 64.

### `sv_endpointPrivacy [newValue]`

A boolean variable that, if true, hides player IP addresses from public reports output by the server.

### `sv_hostname [newValue]`

A string variable that contains the server host name.

### `sv_authMaxVariance [newValue]`

**Variance** is how likely the user's id will change for a given provider (i.e. 'steam', 'ip', or 'ros').

A console variable as an integer from 1-5 (default 1); from least to most likely to change.

### `sv_authMinTrust [newValue]`

**Trust** is how _unlikely_ it is for the user's identity to be spoofed by a malicious client.

A console variable as an integer from 1-5 (default 5); from least to most trustworthy (5 being a method such as external three-way authentication).

### `clientkick [id] [reason]`

{{% alert theme="info" %}}This is provided by the **rconlog** resource. {{% /alert %}}

Kicks the client with the specified server ID (as seen in [status](#status "wikilink")) from the server, for the stated reason.

Example:

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
