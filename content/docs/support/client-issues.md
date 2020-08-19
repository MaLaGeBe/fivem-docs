---
title: 客户端问题
weight: 830
---

游戏崩溃了？不能启动FiveM？或者可能会遇到一些更模糊的问题？在这里找到最常见的问题。

我在某个服务器上玩的时候游戏崩溃了。
--------------------------------
游戏崩溃通常与服务器特定的问题有关。要确保崩溃与特定服务器无关，建议加入[vanilla FiveM服务器][vanilla-server]。如果服务器在没有你的问题的情况下工作，我们建议您与发生崩溃的服务器的服务器所有者联系。 否则，请继续阅读。

我在服务器上被封禁了
----------------------------
FiveM不对您在服务器上的操作负责，或者服务器管理员对你做了什么。如果你觉得自己被误封了，请与服务器所有者联系。FiveM不能也不会为此事提供支持。

我被FiveM全球封禁
------------------------------------
真很不幸，千万别作弊。如果你觉得你被误封了，请通过[support@fivem.net][email]联系我们，并提供可能被误封的潜在原因。<br />
**请注意，FiveM论坛版主或FiveM discord的工作人员 _不能_ 协助您撤销此禁令。**
<!-- 这里需要重新翻译 -->
That's unfortunate, don't cheat.
If you believe you've been falsely banned, you can fill out the ban report at https://forum.cfx.re/w/ban-report. This is **not a ban appeal**, but this data is used for structured collection of potential 'false positive' bans.<br />
**Please note that you may not get a response and that FiveM forum/Discord moderators can _not_ assist you with your ban.**

找不到游戏可执行文件
------------------------------
<!-- https://media.discordapp.net/attachments/455024366091108352/479263072276578324/unknown.png -->
<!--<img src="/static/could-not-find-game-exec-error.png">-->
在 [FiveM应用程序数据目录][where-is-fivem-installed] 文件夹找到`CitizenFX.ini`文件，并确保它指向正确的GTAV路径。使用文本编辑器（如记事本）打开文件，必要时重新编辑GTA V安装的路径。

提示已安装FiveM（FiveM is already installed）
--------------------------
<!-- https://media.discordapp.net/attachments/455024366091108352/479267390836834306/unknown.png -->
安装FiveM之后，就不需要再使用同一个FiveM.exe文件了。使用Windows“开始”菜单中的快捷方式。按任务栏上的“开始”按钮，在那里查找FiveM的快捷方式。

如果通过删除快捷方式卸载FiveM，您可能必须正确 [卸载][uninstalling] FiveM。

游戏缓存已过期（Game cache outdated）
-------------------
<!-- https://media.discordapp.net/attachments/455024366091108352/479268603510652946/unknown.png -->
<!-- https://vgy.me/JJJzfI.png -->
如果提示 `Do you wish to continue?`请按 `确认`。如果出现类似 `DLC files are missing` 的错误，按照对话框中的说明确保您的游戏是最新的。另外，确保 `CitizenFX.ini` 指向正确的GTA V安装。你可以在 [FiveM应用程序数据目录][where-is-fivem-installed] 找到这个文件。

生成ROS授权令牌时出错
--------------------------------------
<!-- https://i.imgur.com/IAobS5M.png -->
已知某些杀毒软件供应商出于未知原因阻止FiveM。
请[禁用防病毒程序][disabling-antivirus]，然后重试。

加载组件 `xyz.dll` 出错
-------------------------------
从[FiveM应用程序数据目录][where-is-fivem-installed]文件夹中删除 caches.xml
如果没有这样的文件，删除整个应用程序数据文件夹并再次运行FiveM。有关 `adhesive.dll` 的信息，请参见下文。

加载组件 `adhesive.dll` 出错
-------------------------------
您的Windows 10安装已过时。请将其更新到至少1703版。要检查当前版本，打开命令提示符并键入`winver`。

打开数据库(privcache:/)失败：IO错误：无法锁定文件
------------------------------
你的私有缓存被破坏了。请从[FiveM应用程序数据目录][where-is-fivem-installed]文件夹中的缓存（cache）文件夹中删除“priv”文件夹

Opening database (privcache:/) failed: IO error: could not lock file
------------------------------
你的私有缓存被破坏了。请从[FiveM应用程序数据目录][where-is-fivem-installed]文件夹中的缓存（cache）文件夹中删除“priv”文件夹

未找到入口点(Entry Point Not Found)
------------------------------
如果在你的 `C:\Windows\system32` 文件夹中可以找到 `v8.dll`、`v8_libbase.dll` 和 `v8_libplatform.dll` ，请删除他们。这些是来自其他应用程序的（剩余）文件，这些应用程序错误地使用 `system32` 来放置这些文件。
FiveM会先从 `system32` 加载dll，导致这些不正确的DLL被加载。

移动 xyz.exe 失败(err = 32)  Moving of xyz.exe failed (err = 32)
------------------------------
首先检查任务管理器中现有的fivem进程，如果您看到它们关闭了它们，如果这不能解决问题，试试[禁用防病毒程序][disabling-antivirus].

卡在 'We're getting there and it will be worth the wait'
------------------------------------------------------------
<!-- https://prnt.sc/kj02oo -->
通常由防病毒程序引起。请[禁用防病毒程序][disabling-antivirus]，然后重试。

卡在进服加载界面
---------------------------------
删除 `%appdata%\citizenfx\ros_id.dat` 文件和 `%localappdata%\digitalentitlements`文件夹。

卡在黑屏上
-----------------------
这是某些NVIDIA驱动程序导致的常见问题。保持耐心，通常需要一分钟的时间。这也经常发生在其他游戏中。

卡在彩色背景但没有菜单
------------------------------
这种情况发生在特定的老式AMD笔记本电脑GPU上。不幸的是，这是由CEF引起的，不是由FiveM引起的。一旦CEF解决了这个问题，FiveM也会更新。论坛版主创建了一个可能纠正此问题的主题。[点击这里][discrete-gpu]获取更多信息。

FVEM在运行后自行卸载了！
-----------------------------------------
这很可能是你的杀毒软件删除了FiveM。不幸的是一些杀毒软件供应商错误地标记了FiveM，并删除一些（甚至全部）FiveM文件作为预防措施。你可以安全地忽略任何关于这个的警告。<br />
[单击此处][disabling-antivirus]获取有关如何禁用防病毒的详细信息。

需要帮助！我在这里找不到我的问题！
---------------------------------
我们非常乐意帮助你！如果你遇到崩溃或停止运行的情况。请将您的问题发表在我们的[论坛][forum]上。提供尽可能多的细节，这会让大家更容易帮助你。
对于所有其他问题，我们非常欢迎你加入我们的[Discord][discord]和我们一起聊天。

[where-is-fivem-installed]: /docs/support/client-faq#where-is-fivem-installed
[disabling-antivirus]: /docs/client-manual/disabling-antivirus
[email]: mailto:support@fivem.net
[forum]: https://forum.cfx.re
[discord]: https://discord.gg/fivem
[vanilla-server]: https://servers.fivem.net/#/servers/detail/198.27.79.239:30120
[uninstalling]: /docs/client-manual/installing-fivem#uninstalling
[discrete-gpu]: https://forum.cfx.re/t/217731
