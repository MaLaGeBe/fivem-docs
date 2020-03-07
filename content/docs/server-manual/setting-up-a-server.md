---
title: 设置服务器
weight: 310
description: >
  设置FXServer的分步指南。
---

运行FXServer
================

FXServer是当前CitizenFX服务器版本的名称。此页面显示了如何运行它。

运行服务端时遇到问题？请访问[疑难问题解答][server-issues]，使用 Discord [#fxserver-support][fxserver-support] 频道或在论坛的 [Server Discussion][fxserver-support-category] 子类别中创建主题。

Windows
-------

#### 先决条件
1. [Visual C++ Redistributable 2019][vcredist] 或最新版
2. 确保正确安装[Git][git-scm]环境。

#### 安装
1. 创建一个新目录（比如 `D:\FXServer\server`），这将用于存放服务端文件。
2. 从[构建服务器][windows-artifacts]下载适用于Windows的最新`master`分支版本。
3. 将构建解文件解压到先前创建的目录中。
  <br>3.1 使用任何压缩文件工具（例如WinRAR或7-Zip）。
4. 将 [cfx-server-data][server-data] 克隆到服务端文件夹之外的新文件夹中。例如 `D:\FXServer\server-data`。
  <br>4.1 `git clone https://github.com/citizenfx/cfx-server-data.git server-data`
5. 在 `server-data` 文件夹中创建一个 **server.cfg** 文件（将下面的[示例 server.cfg](#servercfgexample) 文件复制到该文件中）。
6. 在 <https://keymaster.fivem.net> 上生成许可证密钥。
7. 在server.cfg中设置许可证密钥至 `sv_licenseKey "licenseKeyGoesHere"`。
8. 从 `server-data` 文件夹中运行服务。在纯Windows命令提示符（cmd.exe）窗口中输入如下命令：
    ```dos
    cd /d D:\FXServer\server-data
    D:\FXServer\server\run.cmd +exec server.cfg
    ```

    （仅在将目录更改为其他驱动器上的某个位置时才需要使用 `/d` 命令）

---

Linux
-----
1. 创建一个新目录（比如 `mkdir /home/username/FXServer/server`），这将用于存放服务端文件。
2. 从[构建服务器][linux-artifacts]下载适用于Linux的最新`master`分支版本。（复制最新服务器版本的URL并使用 `wget <url>` 进行下载）。
3. 将构建解文件压缩到先前创建的目录中，使用 `cd /home/username/FXServer/server && tar xf fx.tar.xz` 解压缩（你需要 `xz` 解压缩软件，在Debian / Ubuntu上，这在 `xz-utils` 软件包中）。
4. 将 [cfx-server-data][server-data] 克隆到服务端文件夹之外的新文件夹中。
  <br>4.1 例如 `git clone https://github.com/citizenfx/cfx-server-data.git /home/username/FXServer/server-data`
5. 在 `server-data` 文件夹中创建一个 **server.cfg** 文件（将下面的[示例 server.cfg](#servercfgexample) 文件复制到该文件中）。
6. 在 <https://keymaster.fivem.net> 上生成许可证密钥。
7. 在server.cfg中设置许可证密钥至 `sv_licenseKey "licenseKeyGoesHere"`。
8. 从 `server-data` 文件夹中运行服务。
  <br>8.1 `bash /home/username/FXServer/server/run.sh +exec server.cfg`

常见问题
---------------

- 如果提示 `resources found`，并且提示 `Failed to start resource`，则你没有 `cd` 至正确的目录。
- 如果有一些关于 `citizen:/scripting/` 的错误提示，那是因为你没有正确的运行 `run.cmd`。
- 如果除了 `sending heartbeat`之外什么都没有发生，那是你没有正确的运行 `run.cmd`。 **并且** 没有 `cd` 至正确的目录。
- 如果没有资源开始启动，并且你无法成功连接，那是因为你在启动时没有加 `+exec` 命令。
- 如果提示 `no license key was specified`，总有上面某个情况适用。

<a name="servercfgexample"></a>server.cfg
----------

下面是一个示例 server.cfg 文件。

```sh
# 仅在使用具有多个网络接口的服务器时才更改IP，否则仅更改端口。
endpoint_add_tcp "0.0.0.0:30120"
endpoint_add_udp "0.0.0.0:30120"

# 这些资源将默认启动。
ensure mapmanager
ensure chat
ensure spawnmanager
ensure sessionmanager
ensure fivem
ensure hardcap
ensure rconlog
ensure scoreboard

# 这允许玩家使用基于脚本挂钩的插件，例如旧版Lambda菜单。
# 将此设置为1以允许脚本挂钩。 请注意，这并不能保证玩家将无法使用外部插件。
sv_scriptHookAllowed 0

# 取消注释，并设置密码以启用RCON。确保更改密码 - it should look like rcon_password "YOURPASSWORD"
#rcon_password ""

# 以逗号分隔的服务器标签列表。
# 例如：
# - sets tags "drifting, cars, racing"
# Or:
# - sets tags "roleplay, military, tanks"
sets tags "default"

# 服务器主要语言的有效语言环境标识符。
# 例如 "zh-CN", "zh-HK", "zh-TW", "en-US", "fr-CA", "nl-NL", "de-DE", "en-GB", "pt-BR"
sets locale "root-AQ" 
# 请务必用真实语言替换上面的root-AQ！ :)

# 设置可选的服务器信息和连接标题图像URL。
# 大小无所谓，任何横幅大小的图像都可以。
#sets banner_detail "https://url.to/image.png"
#sets banner_connecting "https://url.to/image.png"

# 设置服务器的主机名
sv_hostname "FXServer, but unconfigured"

# 嵌套的配置！
#exec server_internal.cfg

# 加载服务器图标（96x96 PNG文件）
#load_server_icon myLogo.png

# 可以在脚本中使用的convars
set temp_convar "hey world!"

# 如果您不想在服务器浏览器中展示服务器，请取消注释此行。
# 如果确实要展示服务器，请不要对其进行编辑。
#sv_master1 ""

# 添加系统管理员
add_ace group.admin command allow # 允许所有命令
add_ace group.admin command.quit deny # 但不允许退出命令
add_principal identifier.fivem:1 group.admin # 将管理员添加到组

# 在外部日志输出中隐藏玩家端点。
sv_endpointprivacy true

# 服务端玩家数量限制（除非使用OneSync，否则必须在1到32之间）
sv_maxclients 32

# Steam Web API密钥（如果要使用Steam身份验证）(https://steamcommunity.com/dev/apikey)
# -> replace "" with the key
set steam_webApiKey ""

# 服务端的许可证密钥 (https://keymaster.fivem.net)
sv_licenseKey changeme
```

之后开始做什么？
------------

- [使用服务端命令][server-commands]
- [开始编写脚本][scripting-introduction]

[windows-artifacts]: https://runtime.fivem.net/artifacts/fivem/build_server_windows/master/
[linux-artifacts]: https://runtime.fivem.net/artifacts/fivem/build_proot_linux/master/
[server-data]: https://github.com/citizenfx/cfx-server-data

[vcredist]: https://aka.ms/vs/16/release/VC_redist.x64.exe
[winrar]: https://www.rarlab.com/download.htm
[7zip]: https://www.7-zip.org/download.html
[git-scm]: https://git-scm.com/download/win

[server-issues]: /docs/support/server-issues
[server-commands]: /docs/server-manual/server-commands
[scripting-introduction]: /docs/scripting-manual/introduction

[fxserver-support]: https://discord.gg/UwvVgsJ
[fxserver-support-category]: https://forum.fivem.net/c/server-development/server-discussion
