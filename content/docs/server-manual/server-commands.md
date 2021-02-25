---
title: 服务端命令
weight: 330
description: >
  在服务端控制台中运行的命令列表。
---

<!-- TODO: format this like client commands? -->

Console commands can be executed either using an RCon tool, directly from the server console interface, a server configuration
file, the server command line, or (if a resource is allowed by the ACL) the [ExecuteCommand]({{% native "EXECUTE_COMMAND" %}}) function.

Adding a custom RCon command can be done using the [RegisterCommand]({{% native "REGISTER_COMMAND" %}}) function on the
server, or the (legacy) `rconCommand` event.

## Resource commands

### `start [resourceName]`

Starts the resource specified in the argument, if it was stopped. It is also possible to specify a category name, such as `start [cars]`.

示例：

    start lambda-menu
    start [cars]

### `stop [resourceName]`

Stops the resource specified in the argument, if it was started. As with `start`, one can also specify a category name.

示例：

    stop mymode

### `ensure [resourceName]`

重新启动参数中指定的资源（如果已启动）。 如果不是，则启动参数中指定的资源。

As with `start` and `stop`, one can also specify a category name.

Example:

    ensure my-testing-resource

### `restart [resourceName]`

Restarts the resource specified in the argument, if it was started. Also supports category names.

示例：

    restart lambda-menu

### `refresh`

Rescans the *resources* folder and loads all resource manifests in them, also making new resources available to start using [start](#start-resourcename "wikilink").

示例：

    refresh

## Global commands

### `exec [filename]`

Runs the commands specified in the filename. Commonly seen as `FXServer.exe +exec server.cfg`.

Example:

    exec server_nested.cfg

## Management commands

### `status`

{{% alert theme="info" %}}这是由 **rconlog** 资源提供的。{{% /alert %}}

显示具有其主要标识符，服务器ID，名称，端点和ping的玩家列表。

示例：

    status

### `clientkick [id] [reason]`

{{% alert theme="info" %}}This is provided by the **rconlog** resource. {{% /alert %}}

Kicks the client with the specified server ID (as seen in [status](#status "wikilink")) from the server, for the stated reason.

Example:

    clientkick 43 You're a superstitious idiot!

### `say [message]`

{{% alert theme="info" %}}This is provided by the **chat** resource. {{% /alert %}}

Sends a message in the chat as *console*.

Example:

    say Hi, everybody!

### `svgui`

Opens or closes the server debug GUI.

## Configuration variables

### `onesync [on/off/legacy]`

Defines which mode of state awareness to use.

* **Off**: No state awareness at all, clients will use the standard GTA/RAGE P2P networking model, and the server will only function as a relay.
* **On**: Full state awareness and server-determined entity routing.
* **Legacy**: Compatibility mode for scripts that expect all players to exist on each client. Not recommended due to performance issues and graphical glitches.

### `sv_maxClients [newValue]`

A console variable that specifies the maximum amount of clients that the server can normally have, as an integer from 1 to 1024.

Values starting at 32 will require `onesync` to be set to `on` or `legacy`, and values above 64 will require `onesync` to be set to `on`.

### `sv_endpointPrivacy [newValue]`

A boolean variable that, if true, hides player IP addresses from public reports output by the server.

### `sv_hostname [newValue]`

A string variable that contains the server host name.

### `sv_authMaxVariance [newValue]`

**Variance** is how likely the user's id will change for a given provider (i.e. 'steam', 'ip', or 'license').

A console variable as an integer from 1-5 (default 1); from least to most likely to change.

### `sv_authMinTrust [newValue]`

**Trust** is how _unlikely_ it is for the user's identity to be spoofed by a malicious client.

A console variable as an integer from 1-5 (default 5); from least to most trustworthy (5 being a method such as external three-way authentication).

### `load_server_icon [fileName.png]`

A console command which loads a specfied icon and sets it as the server icon. The icon needs to be a 96x96 PNG file.

示例：

```toml
load_server_icon "my-server.png"
```

### `rcon_password [password]`

Sets the RCon password. This being unset means RCon is disabled.

### `steam_webApiKey [key]`

Sets a [Steam Web API key](https://steamcommunity.com/dev/apikey), which is required to allow for Steam identifiers to be returned by the server.

## Access control commands

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
