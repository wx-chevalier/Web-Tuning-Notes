# Edge 多进程体系结构

Edge 的进程主要划分为以下类别：

- 浏览器进程（Browser process）：这是主要的进程，它帮助管理窗口和标签，并控制浏览器框架，如地址栏和前进和后退按钮。它还可以对网络请求和文件访问等实用程序的特权访问进行路由。

- 渲染进程（Renderer processes）：这些控件通过执行网站提供的代码来控制网站如何在标签页中渲染。它们处理 HTML、CSS、JavaScript、图像等。每个渲染器进程的资源使用情况都取决于所托管的内容。

- GPU 进程（GPU process）：该进程负责与 GPU（图形处理单元）进行通信并处理所有 GPU 任务。GPU 是一种硬件，可以快速执行与图形相关的计算，并将输出发送到显示器以进行显示，现代浏览器使用 GPU 来快速渲染网页。

- 实用程序进程（Utility processes）：音频播放、网络服务、视频采集、数据解码、收藏管理器都由这些进程来处理，这样 Microsoft Edge 就可以控制和审核这些资源的访问，协调全局系统资源的使用。

- 插件进行和扩展程序进程（Plug-in processes and extension processes）：插件进程包含活动插件，例如 Adobe Flash，而扩展进程包含活动扩展。每个进程执行由插件或扩展提供的代码，每个进程的资源使用情况根据所提供的代码而不同。每个进程也有允许插件或扩展与浏览器和渲染器进程通信的代码。

- Crashpad 处理程序进程（Crashpad handler process）：这可以跟踪 Microsoft Edge 中不同进程的健康状况。如果 Microsoft Edge 崩溃，这个过程将帮助浏览器捕获并将崩溃报告传输到微软服务器，我们使用这些崩溃报告来寻找和修复崩溃。

现在我们已经介绍了每个进程的作用，让我们来看看一个进程的例子，它将为一个打开了一个标签页并在 Microsoft Edge 中打开了两个扩展的用户运行。

![浏览器实例，其中一个选项卡已打开，两个扩展已打开](https://s1.ax1x.com/2020/10/18/0j12Wj.png)

在此示例中，用户将看到九个进程正在运行：

- 浏览器框架的浏览器进程
- 一个帮助显示图形的 GPU 进程
- 一个正在运行示例网站提供的代码的渲染器进程
- 网络服务实用程序进程，帮助处理网络请求
- 音频服务实用程序进程，可帮助播放音频
- 运行 Flash 提供的代码的插件进程
- 两个扩展进程，每个扩展进程一个，运行扩展提供的代码
- 一个监控 Microsoft Edge 健康状况的 crashpad 处理程序

所有这些过程一起写作，给你今天使用的浏览体验。

现在让我们来看另一个例子。在下一个示例中，用户打开了四个选项卡，并启用了两个扩展（图 2）。每个标签都有一个广告（两个来自一个来源，两个来自另一个来源）。

![浏览器实例打开了四个选项卡，并且打开了两个扩展](https://s1.ax1x.com/2020/10/18/0j1qfJ.png)

在此示例中，如果用户打开任务管理器，他们将看到 14 个进程正在运行：

- 浏览器框架的浏览器进程
- 一个帮助显示图形的 GPU 进程
- 六个渲染器进程：

  - 四个标签页的渲染器进程，每个标签页都有自己的渲染器进程，并运行网站提供的代码。有时，来自同一域的选项卡将共享一个进程。
  - 两个广告的渲染器进程。来自同一域名的广告将共享一个进程，并将运行广告提供的代码。在本例中，第一个来源的两个广告将共享一个进程，第二个来源的两个广告将共享一个单独的进程。这些广告使用称为子帧的东西嵌入网页中。（稍后我们将详细讨论子帧。）

- 网络服务实用程序进程，帮助处理网络请求
- 音频服务实用程序进程，可帮助播放音频
- 一个正在运行 Flash 的插件进程
- 两个扩展进程，每个扩展进程一个，运行扩展提供的代码
- 一个监控 Microsoft Edge 健康状况的 crashpad 处理程序

一些例子更加复杂。您可能会看到对您不可见的子框架的其他进程，或者您可能会看到项目(如 service workers 人员或 web workers)与选项卡或子框架共享进程。service workers 和 web workers 是在后台运行的脚本，以提高性能，并允许您在没有互联网连接的情况下使用一些网站和应用程序。
