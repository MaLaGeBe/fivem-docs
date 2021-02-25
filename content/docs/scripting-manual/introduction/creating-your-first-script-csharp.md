---
title: 用C＃创建您的第一个脚本
weight: 412
---

鉴于种类繁多的可能性和文档稀疏，您可能在FiveM脚本编写时可能有点不知所措。而在这个快速而简单的指南中，我们将尝试向您展示如何开始使用C＃中的快速资源。 我们将通过命令实现汽车的生成。

## Prerequisites
在使用C＃创建第一个脚本之前，你需要了解以下内容。

* [Creating a C# project and setup your environment](/docs/scripting-manual/runtimes/csharp)
* [Understanding of resources and manifest files](/docs/scripting-reference/resource-manifest/resource-manifest)

### Writing code
现在，您已经设置了C＃项目和环境，您将拥有两个项目。 `MyResourceNameClient` 和 `MyResourceNameServer`.

任何处理FiveM脚本相关事件的C＃类都必须继承自`BaseScript`类。 让我们通过在客户端项目中访问`Class1.cs`来实现。 同时，我们还将定义一个构造函数，我们将在以后使用它。 确保您对`CitizenFX.Core`具有using指令。
```csharp
using CitizenFX.Core;

namespace MyResourceNameClient
{
    public class Class1 : BaseScript
    {
        public Class1()
        {

        }
    }
}
```

容易吧？ 但是增加的功能呢？ 我们将从使用各种FiveM脚本概念添加命令开始。

```csharp
using System;
using System.Collections.Generic;
using CitizenFX.Core;
using static CitizenFX.Core.Native.API;

namespace MyResourceNameClient
{
    public class Class1 : BaseScript
    {
        public Class1()
        {
            EventHandlers["onClientResourceStart"] += new Action<string>(OnClientResourceStart);
        }

        private void OnClientResourceStart(string resourceName)
        {
            if (GetCurrentResourceName() != resourceName) return;

            RegisterCommand("car", new Action<int, List<object>, string>((source, args, raw) =>
            {
                // TODO: make a vehicle! fun!
                TriggerEvent("chat:addMessage", new
                {
                    color = new[] {255, 0, 0},
                    args = new[] {"[CarSpawner]", $"I wish I could spawn this {(args.Count > 0 ? $"{args[0]} or" : "")} adder but my owner was too lazy. :("}
                });
            }), false);
        }
    }
}
```

这时您可能不知所措，但是不用担心。 我们将一点一点地解释所有的步骤。

```csharp
EventHandlers["onClientResourceStart"] += new Action<string>(OnClientResourceStart);
```
在构造函数中，我们为[onClientResourceStart](/docs/scripting-reference/events/list/onClientResourceStart/) 事件添加了事件处理程序。 这需要一个论点。 一个字符串，其中包含已启动资源的名称。 它还有一个委托方法`OnClientResourceStart`，我们在构造函数下定义了该方法。 资源启动后，FiveM将触发此事件并调用该方法。

```csharp
if (GetCurrentResourceName() != resourceName) return;
```
这个if语句使用了本地的`GetCurrentResourceName()`。 简而言之，与土著人民无关的_natives_实际上是“游戏定义的脚本功能”的R *标签。 我们可以通过`CitizenFX.Core.Native.API`类访问这些本地用户。 稍后会在生成车辆时使用其他本地人。 在此代码段中，`GetCurrentResourceName()`返回脚本正在运行的资源的名称。 我们将其与`resourceName`参数进行比较，以确保仅调用该方法的其余部分一次。 如果我们不执行此检查，则每次启动任何资源时，其余方法将运行。

```csharp
RegisterCommand("car", new Action<int, List<object>, string>((source, args, raw) =>
{
    // TODO: make a vehicle! fun!
    TriggerEvent("chat:addMessage", new
    {
        color = new[] {255, 0, 0},
        args = new[] {"[CarSpawner]", $"I wish I could spawn this {(args.Count > 0 ? $"{args[0]} or" : "")} adder but my owner was too lazy. :("}
    });
}), false);
```
首先，我们看到一个对函数的调用。 我们没有定义该功能。 好吧，（就像FiveM团队一样）做了，但是当引导读者这个奇妙的书面指南奇迹时，却没有。 这意味着它必须来自其他地方！

And, guess what, it's actually {{% native_link "REGISTER_COMMAND" %}}! Click that link, and you'll be led to the documentation for this native. It looks a bit like this:

```c
// 0x5fa79b0f
// RegisterCommand
void REGISTER_COMMAND(char* commandName, func handler, BOOL restricted);
```

我们主要关心第二行的名称(上面的C＃代码中使用的，`RegisterCommand`)和参数。

如您所见，第一个参数是 **command name**。 第二个参数是**function**（在我们的示例中由Action委托表示），它是命令处理程序，第三个参数是**boolean**，它指定是否应该将其作为受限命令。

该函数本身会获得一个名为`source`的参数，该参数仅在您在服务器上运行时才真正重要（它将是输入命令的播放器的客户端ID，这是非常有用的东西），并且 `args`，基本上是您在像`/car zentorno`这样的命令之后输入的内容，使得args最终成为`new List<object>{ "zentorno" }`或`/car zentorno unused`成为`new List<object>{ "zentorno", "unused" }`.。

但是`TriggerEvent()`呢？ 这也由_us_定义。 它用于调用事件`chat:addMessage`，它是[chat](/docs/resources/chat/events/chat-addMessage/)资源的一部分。 在我们的书面示例中，我们以红色发送作者姓名`[CarSpawner]`，并发送一条消息作为参数。

此时，您可以构建您的客户端项目，将其添加/移动到您的资源中并运行它。 在聊天框中输入`/car`时，您将看到我们的命令返回我们定义的聊天消息。![screenshot-1](/csharp-tut-6.png)
嘿! 在聊天框中抱怨您懒得实现它。 我们将向他们展示您绝对不是“懒惰”，并立即实施此操作。

### Implementing a car spawner
您可能已经按照Lua教程创建了第一个脚本，并记住那里有很多样板代码可能看起来很压倒性的。 不用担心，FiveM提供了易于使用的C＃包装器，它使我们可以减少代码。

```csharp
RegisterCommand("car", new Action<int, List<object>, string>(async (source, args, raw) =>
{
    // account for the argument not being passed
    var model = "adder";
    if (args.Count > 0)
    {
        model = args[0].ToString();
    }

    // check if the model actually exists
    // assumes the directive `using static CitizenFX.Core.Native.API;`
    var hash = (uint) GetHashKey(model);
    if (!IsModelInCdimage(hash) || !IsModelAVehicle(hash))
    {
        TriggerEvent("chat:addMessage", new 
        {
            color = new[] { 255, 0, 0 },
            args = new[] { "[CarSpawner]", $"It might have been a good thing that you tried to spawn a {model}. Who even wants their spawning to actually ^*succeed?" }
        });
        return;
    }

    // create the vehicle
    var vehicle = await World.CreateVehicle(model, Game.PlayerPed.Position, Game.PlayerPed.Heading);
    
    // set the player ped into the vehicle and driver seat
    Game.PlayerPed.SetIntoVehicle(vehicle, VehicleSeat.Driver);

    // tell the player
    TriggerEvent("chat:addMessage", new 
    {
        color = new[] {255, 0, 0},
        args = new[] {"[CarSpawner]", $"Woohoo! Enjoy your new ^*{model}!"}
    });
}), false);
```

这使用了一些本机和C＃包装器方法。 我们将链接其中的一些内容并解释其中的难点。

#### Step 1: Validation
我们从检查模型开始。 我们将其设置为 `adder`。 如果有任何参数，我们将模型设置为第一个参数，并将其强制转换为字符串。

Then, we check if the vehicle is in the CD image using {{% native_link "IS_MODEL_IN_CDIMAGE" %}}. This basically means 'is this registered with the game'. We also check if it's a vehicle using {{% native_link "IS_MODEL_A_VEHICLE" %}}. If either check fails, we tell the player and return from the command.

这里可能有C＃包装器，但是重要的是要重新使用本机，因为编写脚本时会大量使用它们。 确保您的类中具有`using static CitizenFX.Core.Native.API;`指令。

#### Step 2: Creating the vehicle
通过使用客户端C＃包装器类`World`，我们调用`CreateVehicle`方法，该方法将模型，`Vector3`位置和`float`标题作为参数。 这是C＃的伟大之处。 您可以访问 _us_ 提供的方法，从而不必像在Lua中那样请求和加载模型。 这个方法返回一个`Vehicle`对象。 如果您有使用*ScriptHookV.NET*的经验，则可以识别这些类。 FiveM的C＃包装器非常相似。

#### Step 3: Setting the player into the vehicle
现在我们有了角色模型和车辆，可以使用带有`Game.PlayerPed`对象的C＃包装器，将自己放置在车辆的驾驶员座椅上。

### Running this
生成您的项目，并确保最新的`MyResourceNameClient.net.dll`位于资源的文件夹中。 在服务器控制台中，键入`restart mymode`（或任何您命名的资源名称），然后在游戏客户端中尝试 `/car voltic2`（现在应该很无聊了）。 您现在将拥有自己的Rocket Voltic！

## Server scripts
您可能还需要编写与服务器交互的脚本。 本节尚待编写。 :-(
