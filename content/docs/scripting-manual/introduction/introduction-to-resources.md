---
title: 资源介绍
weight: 411
---

服务器运行在一个资源集合上。**资源** 是文件的集合 - 例如客户端脚本、服务器脚本和流媒体资源 - 它可以随时启动、停止和重新启动。

资源目录
--------------------

在服务器中，资源是从服务器数据目录中名为`resources/`的文件夹中加载的。`resources/` 文件夹中的任何文件夹都被解析为资源，除了`[括号]`之间属于类别的文件夹之外，其中可以包含多个资源文件夹。

每个资源文件夹还必须包含一个名为 `fxmanifest.lua`（或之前的`__resource.lua`）的[资源清单][manifest-reference] 引用，以正确地解析为资源。

请参阅以下示例目录树：

```
server                                  #服务端
└── resources                           #资源目录
    ├── [category]                      #资源分类
    │   ├── [another]                   #其他分类
    │   │   └── thing                   #某某资源目录
    │   │       └── fxmanifest.lua      #某某资源清单文件
    │   └── resource-1                  #某某某资源目录
    │       └── fxmanifest.lua          #某某某资源清单文件
    └── main                            #某资源目录
        └── fxmanifest.lua              #某资源清单文件
```

在此列表树中，存在以下资源：

-   main
-   resource-1
-   thing

资源清单
---------------------

每个资源都必须包含一个名为`fxmanifest.lua`的资源清单，该清单定义了该资源使用的文件/脚本。一个简单的清单示例如下：

{{< code file="/static/examples/manifest/fxmanifest.lua" language="lua" >}}

有关更多详细信息，请参见[资源清单参考][manifest-reference]。

标准资源
------------------

安装服务器后，您会注意到您已经有很多资源。这些是FiveM运行和维护的标准资源。建议不要更改它们，除非您知道自己在做什么。这些资源中的许多资源都为服务器提供了有用的功能。

有关标准资源的更多信息，请参见[资源目录][resource-catalog]。

[manifest-reference]: /docs/scripting-reference/resource-manifest/resource-manifest/
[resource-catalog]: /docs/resources
