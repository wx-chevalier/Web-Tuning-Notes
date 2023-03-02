[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![license: CC BY-NC-SA 4.0](https://img.shields.io/badge/license-CC%20BY--NC--SA%204.0-lightgrey.svg)][license-url]

<!-- PROJECT LOGO -->
<br />
<p align="center">
  <a href="https://github.com/wx-chevalier/Web-Engineering-Series">
    <img src="https://assets.ng-tech.icu/item/header.svg" alt="Logo" style="width: 100vw;height: 400px" />
  </a>

  <p align="center">
    <a href="https://ng-tech.icu/books/Web-Engineering-Series"><strong>在线阅读 >> </strong></a>
    <br />
    <br />
    <a href="https://github.com/wx-chevalier/Awesome-CheatSheets">速览手册</a>
    ·
    <a href="https://github.com/wx-chevalier">代码实践</a>
    ·
       <a href="https://github.com/wx-chevalier/Awesome-Lists">参考资料</a>
    ·
    <a href="./README.en.md">English Version</a>

  </p>
</p>

<!-- ABOUT THE PROJECT -->

# Introduction | 前言

> 本篇承接自《[Web-Series](https://github.com/wx-chevalier/Web-Series?q=)》，想要了解 Web 开发基础知识请移步。

从桌面浏览器到移动互联网的时代，用户体验毫无疑问都是重中之重，而 Web 页面的性能则是整体体验的基础。所谓高性能的网站，直观来说，即是用户能够快速打开页面展示网页内容，并能流畅的浏览网页，同时尽可能地降低页面资源占用。移动端的硬件条件，网络条件相对于桌面端，会复杂的多，设备类型多样，硬件配置参差不齐，分辨率碎片化，网络状况在移动过程中稳定性，速率都会变化，而对于一个页面到达用户的终端展示，会经过，用户发起请求，服务端接受请求，服务端处理请求，返回响应内容，在用户终端的浏览器展示内容，用户操作页面发起其他页面时间，而这个过程中任何一个环节的延迟都会造成性能瓶颈，降低用户继续访问的可能性，所以我们在服务器端，浏览器端，网络加载，多个方面做了一系列的优化工作。

![Web 性能调优思维脑图](https://i.postimg.cc/Hxsn6grJ/Web-Tuning.png)

随着应用复杂度的不断增加，我们发现脚本解析与处理的瓶颈在于脚本的下载与 CPU 执行这两个阶段：而当 CPU 忙于执行 JavaScript 的时候，自然会难以及时响应用户的操作，从而造成卡顿的感觉。因此，这个阶段我们优化的重点就是网络下载以及脚本执行。

- 对于降低下载时间，保持 JavaScript 包的小巧，特别是对于移动设备。小型捆绑包可提高下载速度，降低内存使用率并降低 CPU 成本。避免只有一个大捆; 如果捆绑超过~50-100 kB，则将其拆分为单独的较小捆。通过 HTTP/2 多路复用，可以同时传输多个请求和响应消息，从而减少额外请求的开销。在移动设备上，你会希望运输更少，特别是因为网络速度，但也保持低内存使用率。

- 对于脚本执行效率的优化，避免长期任务可以使主线程保持忙碌，并可以推断出页面交互的时间。下载后，脚本执行时间现在是主要成本。避免使用大型内联脚本（因为它们仍然在主线程上进行了解析和编译）。一个好的经验法则是：如果脚本超过 1 kB，请避免内联（也因为 1 kB 是代码缓存为外部脚本启动时）。

总的优化策略会从资源请求与缓存、关键渲染路径、图片优化、脚本解析与执行、页面布局与渲染策略、交互与动画、移动端优化、PWA 等几个角度进行考虑。如果您想尽快了解优化清单，请参阅《[Awesome-CheatSheets/Web-Tuning-CheatSheet](https://github.com/wx-chevalier/Awesome-CheatSheets?q=)》

# Links

- https://zhuanlan.zhihu.com/p/66398148
- https://mp.weixin.qq.com/s/vEO4r3-pSROgBzOQjzjV3A 深度解读当代前端架构进化史，下一个趋势在哪？

## Nav | 关联导航

# About | 关于

<!-- CONTRIBUTING -->

## Contributing

Contributions are what make the open source community such an amazing place to be learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<!-- ACKNOWLEDGEMENTS -->

## Acknowledgements

- [Awesome-Lists](https://github.com/wx-chevalier/Awesome-Lists): 📚 Guide to Galaxy, curated, worthy and up-to-date links/reading list for ITCS-Coding/Algorithm/SoftwareArchitecture/AI. 💫 ITCS-编程/算法/软件架构/人工智能等领域的文章/书籍/资料/项目链接精选。

- [Awesome-CS-Books](https://github.com/wx-chevalier/Awesome-CS-Books): :books: Awesome CS Books/Series(.pdf by git lfs) Warehouse for Geeks, ProgrammingLanguage, SoftwareEngineering, Web, AI, ServerSideApplication, Infrastructure, FE etc. :dizzy: 优秀计算机科学与技术领域相关的书籍归档。

## Copyright & More | 延伸阅读

笔者所有文章遵循[知识共享 署名 - 非商业性使用 - 禁止演绎 4.0 国际许可协议](https://creativecommons.org/licenses/by-nc-nd/4.0/deed.zh)，欢迎转载，尊重版权。您还可以前往 [NGTE Books](https://ng-tech.icu/books-gallery/) 主页浏览包含知识体系、编程语言、软件工程、模式与架构、Web 与大前端、服务端开发实践与工程架构、分布式基础架构、人工智能与深度学习、产品运营与创业等多类目的书籍列表：

[![NGTE Books](https://s2.ax1x.com/2020/01/18/19uXtI.png)](https://ng-tech.icu/books-gallery/)

# Links

- [支付宝前端应用架构的发展和选择](https://github.com/sorrycc/blog/issues/6)

<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->

[contributors-shield]: https://img.shields.io/github/contributors/wx-chevalier/Web-Engineering-Series.svg?style=flat-square
[contributors-url]: https://github.com/wx-chevalier/Web-Engineering-Series/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/wx-chevalier/Web-Engineering-Series.svg?style=flat-square
[forks-url]: https://github.com/wx-chevalier/Web-Engineering-Series/network/members
[stars-shield]: https://img.shields.io/github/stars/wx-chevalier/Web-Engineering-Series.svg?style=flat-square
[stars-url]: https://github.com/wx-chevalier/Web-Engineering-Series/stargazers
[issues-shield]: https://img.shields.io/github/issues/wx-chevalier/Web-Engineering-Series.svg?style=flat-square
[issues-url]: https://github.com/wx-chevalier/Web-Engineering-Series/issues
[license-shield]: https://img.shields.io/github/license/wx-chevalier/Web-Engineering-Series.svg?style=flat-square
[license-url]: https://github.com/wx-chevalier/Web-Engineering-Series/blob/master/LICENSE.txt
