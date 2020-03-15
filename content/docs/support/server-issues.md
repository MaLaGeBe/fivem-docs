---
title: 服务端问题
weight: 840
---

我的服务器未显示在服务器列表中
---------------------------------------------

发生这种情况时，请确保其他人可以使用“直接连接”连接到您的服务器。此问题通常是由于端口转发错误或某些防火墙问题造成的。请确保您的网络配置正确。

服务器配置也很重要。如果使用 [默认的 server.cfg 示例][servercfg]，则服务器将列在服务器列表中。您可能已经删除了server.cfg中下面一行前面的 `#`。

```yaml
#sv_master1 ""
```

请确保在该行前面添加 `#`，如上面的示例所示。如果此`#`已添加到行前面，请尝试以下步骤。

#### 检查服务器是否可访问

1. 确保服务器正在运行
2. 在浏览器中， 转到 http://ip:port/info.json (填写您的ip和端口) - 例如 http://127.0.0.1:30120/info.json
3. 检查是否解析，显示有关服务器的信息

或者使用 [canyouseeme.org](http://canyouseeme.org)。只有在Windows服务器或带有图形用户界面的Linux计算机上才能工作。

1. 在浏览器中，访问 [canyouseeme.org](http://canyouseeme.org)
2. 填写服务器端口（默认值：30120）
3. 检查您的端口

##### Could it see the service?

- 初次启动后，服务器可能需要8分钟才能显示在服务器列表中，如果没有其他心跳信号。请耐心点。
- 在极少数情况下，服务器列表服务可能会打不开，请耐心点，很有可能我们的团队已经在努力解决这个问题。
- 您可能正在使用一个NAT/网关来屏蔽UDP源端口。以下是一些针对某些防火墙应用程序解决此问题的指南：
  - [pfSense][pfsensenat]

##### Could it NOT see your service?

可能会有很多不同的问题，很可能与以下一项（或两者）有关：

- 您的端口未正确转发。
- 你有一个防火墙（或 安全软件）阻止（外部）连接。

我的服务器不能使用64、128或超过32个玩家数量
---------------------------------

使用超过32个玩家数量需要OneSync。OneSync支持的最大玩家数为128个。OneSync于2018年4月作为早期访问公开发布，并于2019年6月向所有人开放。然而，32+玩家数的支持还没有离开早期访问。
因此，你仍然需要积极的加入Patreon赞助者以获取FiveM Element Club Argentum或者更高等级，或是手动授予的OneSync EAP的一部分。

要使用32个以上的玩家数支持，请执行以下步骤。

1. 对OneSync访问使用许可证密钥
2. 使用最新的 [服务端构建版本][setting-up-server]
3. 激活OneSync - 在你的 server.cfg 添加 `onesync_enabled 1` 
4. 在server.cfg中将 `sv_maxclients` 设置为大于32的值
5. 重新启动服务器

如果在服务器列表中没有看到更改，耐心等待服务器列表更新。您将在Direct Connect中看到这些更改。

我的服务器名称没有颜色
---------------------------------

你可能在不同的情况下会遇到这种情况。例如，服务器颜色显示在Direct Connect中，但不在服务器列表上。或者根本不显示。这可能有几个原因。

1. 没有从[Patreon][patreon]赞助我们，要求最低级别 - FiveM Element Club Argentum 💿 或者更高
2. 错误使用 [服务器名称格式][chat-formatting]
3. 未保存和/或重新启动服务器
4. 服务器列表缓存尚未更新，请耐心等待

需要帮助！我在这里找不到我的问题！
---------------------------------

我们非常乐意帮助你！如果你遇到崩溃或停止运行的情况。请将您的问题发表在我们的[论坛][forum]上。提供尽可能多的细节，这会让大家更容易帮助你。
对于所有其他问题，我们非常欢迎你加入我们的[Discord][discord]和我们一起聊天。

[patreon]: https://patreon.com/fivem
[forum]: https://forum.fivem.net/
[discord]: https://discord.gg/GtvkUsc
[pfsensenat]: https://www.netgate.com/docs/pfsense/nat/static-port.html
[servercfg]: /docs/server-manual/setting-up-a-server/#a-name-servercfgexample-a-server-cfg
[chat-formatting]: https://forum.fivem.net/t/chat-formatting-colors-bold-underline/67641
[setting-up-server]: /docs/server-manual/setting-up-a-server