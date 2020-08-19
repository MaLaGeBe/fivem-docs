---
title: 服务端调试
weight: 840
---

创建完全转储
-------

本节将解释如何创建有用的调试转储（称为.dmp文件），以帮助进行故障排除。如果遇到崩溃，请设置环境以在下次发生时捕获。

**注意**：创建完全转储仅适用于Windows服务器。Linux当前不支持此方法。

#### 先决条件
1. [ProcDump v9.0][procdump] 或更新的.

#### 用法
1. 确保服务器正在运行。
2. 打开将procdump解压到的命令提示符。为此**使用 ELEVATED 命令提示符** (标题栏上应该写“管理员”).
3. 键入以下命令：
    ```dos
    procdump64.exe -accepteula -i
    ```
    这将procdump注册为调试器以捕获某些崩溃。
4. 打开任务管理器，单击`详细信息`。*定位到* `FXServer.exe`。应该有一个`"PID`列。记下号码。
5. 返回命令提示符并键入：
    ```dos
    procdump64.exe -accepteula -e -h -mp pidhere
    ```
    其中 `pidhere` 是您先前记下的数字。如果出现错误，请确保`"PID"`正确。
6. 等待服务器崩溃。当它崩溃时，它会将一个大的.dmp文件写入procdump文件夹。
7. 压缩此文件（例如`.zip`），并将其上载到 [DropMeFiles][dropmefiles] 或等效文件。
8. 完成后，在命令提示符中运行以下命令以注销调试器：
    ```dos
    procdump64.exe -accepteula -u
    ```

现在可以分析转储文件（使用VS2019+，单击“仅使用本机调试”并加载 [symbols][symbols]）或将其提供给任何请求它的人。如果你确定你发现了一个bug，尽可能详细地在我们的[社区](https://forum.cfx.re/c/general-discussion/bug-reports)或Discord [#server-bugs][discord]频道中报告。使用OneSync？请在[此处](https://forum.cfx.re/c/general-discussion/1s-reports)报告OneSync错误。

[procdump]: https://docs.microsoft.com/en-us/sysinternals/downloads/procdump
[discord]: https://discord.gg/fivem
[dropmefiles]: https://dropmefiles.com/
[symbols]: https://runtime.fivem.net/client/symbols/