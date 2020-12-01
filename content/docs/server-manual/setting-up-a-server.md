---
title: 设置服务器
weight: 310
description: >
  设置FXServer的分步指南。
---


FXServer是当前CitizenFX服务器版本的名称。此页面显示了如何运行它。

运行服务端时遇到问题？请访问[疑难问题解答][server-issues]，使用 Discord [#fxserver-support][fxserver-support] 频道或在论坛的 [Server Discussion][fxserver-support-category] 子类别中创建主题。

## 开始之前
Make sure you have registered a license key on the [Cfx.re Keymaster](https://keymaster.fivem.net/) service. You need to have the IP match the IP on which you're going to *first* use the key. Afterwards, the key can be used on any IP, but only on one server at a time.

## 传统安装步骤

### Windows

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
    D:\FXServer\server\FXServer.exe +exec server.cfg
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
- 如果没有资源开始启动，并且你无法成功连接，那是因为你在启动时没有加 `+exec` 命令。
- 如果提示 `no license key was specified`，总有上面某个情况适用。

<a name="servercfgexample"></a>

## server.cfg

下面是一个示例 server.cfg 文件。

{{< code file="/static/examples/config/server.cfg" language="sh" >}}

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
[fxserver-support-category]: https://forum.cfx.re/c/server-development/server-discussion
