# Chrome 多进程架构

不同的浏览器使用不同的架构，下面主要以 Chrome 为例，介绍浏览器的多进程架构。在 Chrome 中，主要的进程有 4 个：

| 进程     | 负责的工作                                                                                                                               |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| Browser  | 负责浏览器的“Chrome”部分，包括导航栏，书签，前进和后退按钮。同时这个进程还会控制那些我们看不见的部分，包括网络请求的发送以及文件的读写。 |
| Renderer | 负责 tab 内和网页展示相关的所有工作。                                                                                                    |
| Plugin   | 控制网页使用的所有插件，例如 flash 插件。                                                                                                |
| GPU      | 负责独立于其它进程的 GPU 任务。它之所以被独立为一个进程是因为它要处理来自于不同 tab 的渲染请求并把它在同一个界面上画出来。               |

![Chrome 多进程间构成](https://s1.ax1x.com/2020/11/06/BWTrTO.md.png)

首先，当我们是要浏览一个网页，我们会在浏览器的地址栏里输入 URL，这个时候 Browser Process 会向这个 URL 发送请求，获取这个 URL 的 HTML 内容，然后将 HTML 交给 Renderer Process，Renderer Process 解析 HTML 内容，解析遇到需要请求网络的资源又返回来交给 Browser Process 进行加载，同时通知 Browser Process，需要 Plugin Process 加载插件资源，执行插件代码。解析完成后，Renderer Process 计算得到图像帧，并将这些图像帧交给 GPU Process，GPU Process 将其转化为图像显示屏幕。

![Chrome 多进程间通信](https://s1.ax1x.com/2020/11/06/BWHDiD.md.png)

除了上面列出来的进程，Chrome 还有很多其他进程在工作，例如扩展进程（Extension Process）和工具进程（utility process）。如果你想看一下你的 Chrome 浏览器现在有多少个进程在跑可以点击浏览器右上角的更多按钮，选择更多工具和任务管理器。

## 多进程架构的好处

当今 Web 应用中，HTML，JavaScript 和 CSS 日益复杂，这些跑在渲染引擎的代码，频繁的出现 BUG，而有些 BUG 会直接导致渲染引擎崩溃，多进程架构使得每一个渲染引擎运行在各自的进程中，相互之间不受影响，也就是说，当其中一个页面崩溃挂掉之后，其他页面还可以正常的运行不收影响。

![各进程间独立](https://s1.ax1x.com/2020/11/06/BWq1gJ.md.png)

更高的安全性和沙盒性（sanboxing）。渲染引擎会经常性的在网络上遇到不可信、甚至是恶意的代码，它们会利用这些漏洞在你的电脑上安装恶意的软件，针对这一问题，浏览器对不同进程限制了不同的权限，并为其提供沙盒运行环境，使其更安全更可靠

更高的响应速度。在单进程的架构中，各个任务相互竞争抢夺 CPU 资源，使得浏览器响应速度变慢，而多进程架构正好规避了这一缺点。

## 浏览器的进程模式与网站隔离（Site Isolation）

为了节省内存，Chrome 提供了四种进程模式（Process Models），不同的进程模式会对 tab 进程做不同的处理。

- **Process-per-site-instance** (default) - 同一个 **site-instance** 使用一个进程
- **Process-per-site -** 同一个 **site** 使用一个进程
- **Process-per-tab -** 每个 tab 使用一个进程
- **Single process -** 所有 tab 共用一个进程

这里需要给出 site 和 site-instance 的定义：

- **site** 指的是相同的 registered domain name(如：google.com，bbc.co.uk)和 scheme (如：https://)。比如 a.baidu.com 和 b.baidu.com 就可以理解为同一个 site（注意这里要和 Same-origin policy 区分开来，同源策略还涉及到子域名和端口）。

- **site-instance** 指的是一组 **connected pages from the same site**，这里 **connected** 的定义是 **can obtain references to each other in script code** 怎么理解这段话呢。满足下面两中情况并且打开的新页面和旧页面属于上面定义的同一个 site，就属于同一个 **site-instance**

  - 用户通过`<a target="_blank">`这种方式点击打开的新页面
  - JS 代码打开的新页面（比如 `window.open`)

首先是 Single process，顾名思义，单进程模式，所有 tab 都会使用同一个进程。接下来是 Process-per-tab，也是顾名思义，每打开一个 tab，会新建一个进程。而对于 Process-per-site，当你打开 a.baidu.com 页面，在打开 b.baidu.com 的页面，这两个页面的 tab 使用的是共一个进程，因为这两个页面的 site 相同，而如此一来，如果其中一个 tab 崩溃了，而另一个 tab 也会崩溃。

Process-per-site-instance 是最重要的，因为这个是 Chrome 默认使用的模式，也就是几乎所有的用户都在用的模式。当你打开一个 tab 访问 a.baidu.com，然后再打开一个 tab 访问 b.baidu.com，这两个 tab 会使用两个进程。而如果你在 a.baidu.com 中，通过 JS 代码打开了 b.baidu.com 页面，这两个 tab 会使用同一个进程。

Process-per-site-instance 兼容了性能与易用性，是一个比较中庸通用的模式。相较于 Process-per-tab，能够少开很多进程，就意味着更少的内存占用；相较于 Process-per-site，能够更好的隔离相同域名下毫无关联的 tab，更加安全。
