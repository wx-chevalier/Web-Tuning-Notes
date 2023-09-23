> [原文地址](https://mp.weixin.qq.com/s?__biz=MjM5MTg2NDA3MQ==&mid=2651937086&idx=1&sn=fdfe9777cf41d266836dcbf98c21afa1&chksm=bd4afd568a3d7440ec1fd999a7022653269f34a9e387eab510704d6764f5e8aa73e2584539b1&scene=27)

# Web Vitals —— 谷歌的新一代 Web 性能体验和质量指标

> 推荐：Google 开发了许多实用指标和工具，帮助衡量用户体验和质量，从而发掘优化点。一项名为 Web Vitals 的计划降低了学习成本，为网站体验提供了一组统一的质量衡量指标 -- Core Web Vitals，其中包括加载体验、交互性和页面内容的视觉稳定性，构成了 2020 年核心 Web 健康指标的基础。本文详细的介绍了每个指标及其使用方式，推荐了用于测量这些指标的实用工具，快来一起看看吧～

![图片](https://mmbiz.qpic.cn/mmbiz_png/Xn6nDZ2tCE03GN5C3DoW4oMr1qgmicxicyeqQ0Lic2yjsiceazzTAlhCA6hny1NbuhVSomaHQI2JC0tmObsjyYziaiaw/640.png?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

Nathan Dumlao 摄影作品（发表于 Unsplash）

有很多方法可以优化网站的用户体验。若能预先了解最佳的优化衡量方法，可以大大节省时间和成本。

Google 在 2020 年 5 月 5 日提出了新的用户体验量化方式 Web Vitals 来衡量网站的用户体验，并将这些衡量结果用作其排名算法的一部分。为了更好的理解这些内容，让我们来看看这些重要指标是什么。

![图片](https://mmbiz.qpic.cn/mmbiz_png/Xn6nDZ2tCE19oQoHYGMNGUcyM9qsCGib3vNHczoPzCZzvreSo3bqyrSwT0pFF0az0YvJ7v3Pjzw7moARibnYGRtQ/640.png?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

Google 在使用者体验量化发展的相关成果

# **01**

# **Core Web Vitals 与 Web Vitals**

什么是 Web Vitals，Google 给出的定义是**一个良好网站的基本指标**（Essential metrics for a healthy site），过去要衡量一个网站的好坏，需要使用的指标太多了，Web Vitals 可以简化指标的学习曲线，只需聚焦于 Web Vitals 指标的表现即可。

“你不需要成为任何领域的专家就可以了解 Web Vitals。它们很简单，比如移动友好性、浏览安全性、HTTPS、交互性、视觉稳定性、加载时间等。”

在这些 Web Vitals 中，Google 确定了三个主要衡量指标，即**在所有类型的网站中通用的 Core Web Vitals[1]：**

（[1]Core Web Vitals 是应用于所有 Web 页面的 Web Vitals 的子集，是其最重要的核心）

![图片](https://mmbiz.qpic.cn/mmbiz_png/Xn6nDZ2tCE03GN5C3DoW4oMr1qgmicxicyHAkl8Rx0Qib4UibxevUBeTbsQXUiaq6Lr9TBtqx9ibjib4aOribHskshNMSw/640.png?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

Core Web Vitals 与 Web Vitals

- **加载性能（LCP）** -- 显示最大内容元素所需时间
- **交互性（FID）** -- 首次输入延迟时间
- **视觉稳定性（CLS）** -- 累积布局配置偏移

这三个指标已经经过了一段时间的验证，如 LCP 在 WICG 已经孵化至少 1 年以上，FID 在 Google Chrome Labs 上已经实施 2 年以上，LCP 和 CLS（相关 Layout Instability API）已于今年入 W3C 草拟标准。

让我们一起详细了解下 Core Web Vitals。

### **1. LCP -- 最大内容绘制**

### **加载性能**

![图片](https://mmbiz.qpic.cn/mmbiz_png/Xn6nDZ2tCE03GN5C3DoW4oMr1qgmicxicy567r7XDtzvekLuZBLIpd6pc0ibFJOFH13FAfmEky7jyf0RzHY2siaSUg/640.png?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

LCP 的基准时间

**LCP**（Largest Contentful Paint）**用于衡量加载体验，**从真实用户的角度衡量网页的加载速度。它是**从页面刚开始加载到呈现出所有内容时的持续时间。**

“换句话说，LCP 是度量网页上可见区域加载时间的方法”

让我们比较一下有图像和没有图像的媒体文章的 LCP。

![图片](https://mmbiz.qpic.cn/mmbiz_png/Xn6nDZ2tCE03GN5C3DoW4oMr1qgmicxicyWib1BZl1wW7rV3iabh3IgPZfJDia6nBsq3IEYXA78zQkBJA8Fnd0568fg/640.png?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

LCP 对比

有图片的文章用了 3.57 秒加载，而没有图片的文章只用了 2.32 秒载入。

“谷歌坚称，所有开发者和产品所有者都会定期测量其应用程序的 Core Web Vitals，并提供工具来辅助测量。”

### **2. FID -- 首次输入延迟**

### **交互行为**

![图片](https://mmbiz.qpic.cn/mmbiz_png/Xn6nDZ2tCE03GN5C3DoW4oMr1qgmicxicymHJ2MibPVhhx9ibKRzuVb8x1MKYtAjkDmhtPfoSMnH1Lja5kNBibGLGzA/640.png?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

FID 的基准时间

**FID**（First Input Delay）涉及到用户与 web 页面之间的交互性，用于衡量网站操作的顺畅程度。它**测量了用户第一次产生交互行为，**到浏览器响应该用户操作的持续时间。这些用户交互行为可以是单击按钮、点击链接或任何基于 JavaScript 的自定义控件。

![图片](https://mmbiz.qpic.cn/mmbiz_png/Xn6nDZ2tCE3hY4bxicIWnQ5gA81kK0wIaNY1ySJa1nBEn5h7YoxEUZmksPvTMt0ApoRoMhSybpTJy8TO3ZXmJcw/640.png?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在 TTI 的时间内第一个互动事件的开始时间与浏览器回应事件的时间差

为什么要取在 TTI[2] 发生的第一次的操作事件，Google 给的理由有以下三点：

- 使用者的第一次互动体验印象相当重要；
- 当今网页最大的互动性问题通常发生在一开始载入时；
- 页面载入完后的第二次操作事件延迟，有其他专门的改善解决建议。

（[2]互动时间 TTI 是衡量负载响应能力的重要实验室指标。它有助于确定页面看起来是交互式但实际上不是交互式的情况。快速的 TTI 有助于确保页面可用。TTI 度量标准衡量的是从页面开始加载到页面主要子资源加载之间的时间，它能够快速可靠地响应用户输入。）

“根据 Google 的基准测试，交互的最佳持续时间应该在 100ms 以下，而任何超过 300ms 的时间都被认为是较差的。”

人们可能会说这些时间间隔很小，调整几百毫秒也没什么区别。但实际上，这些微小的变化可能会对最终用户产生重大影响。

### **3. CLS -- 累计布局偏移**

### **视觉稳定性**

![图片](https://mmbiz.qpic.cn/mmbiz_png/Xn6nDZ2tCE03GN5C3DoW4oMr1qgmicxicy4TtA9CqOX0EB01lIu2QoyhowyvtpkzghrWVYC2qcP1icz7kxdWpic5Pw/640.png?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

CLS 的基准时间

你可能已经注意到某些时候网页中的元素在加载时出现移动，我敢肯定这不是用户期待的优秀体验。在这样的场景中，**CLS**（Cumulative Layout Shift）**测量在页面的整个生命周期中发生的每个意外的样式移动的所有单独布局更改得分的总和，可以方便地用来度量 web 页面的视觉表现。**布局的移动可能发生在可见元素从一帧到下一帧改变位置的任何时候。为了提供良好的用户体验，网站应努力使 CLS 分数小于 0.1。

“CLS 显示页面加载时组件移动的次数。正如大家所理解的，CLS 需要尽可能少地次数来实现良好的用户体验。”

下图显示了 medium.com 和视觉不稳定网站之间的 CLS 差异。

![图片](https://mmbiz.qpic.cn/mmbiz_png/Xn6nDZ2tCE03GN5C3DoW4oMr1qgmicxicylSNMmAyzLFCGRkb2ozZmtib5MyibYv0F3icZibJ5ulXXhu0Pgic8QDhMGjQ/640.png?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

视觉稳定性测量

在上面的例子中，medium.com 网站显示其 CLS 为 0.097。

“这是不是意味着 medium.com 网站加载时主页移动了 0.097 次？→ 不是！！”

计算此值时要考虑视窗大小以及两个渲染帧之间视窗中不稳定元素的移动。

**布局偏移系数**（Layout Shift Score） = **影响范围系数**（Impact Fraction） x **移动距离系数**（Distance Fraction）

CLS 值（布局偏移系数）可以使用上述公式轻松计算。此公式中的影响系数是指不稳定元素对视窗的影响，而距离系数是指不稳定元素移动的距离。

例如，假设一个不稳定的元素覆盖了总窗口大小的 40%，当页面加载时它向下移动了 20%。在这种情况下，因为不稳定元素占用了总窗口的 60%，影响系数将为 0.6。又由于不稳定元素向下移动了 20%，因此距离系数将为 0.2。

因此，**最终布局偏移系数 = 0.6 x 0.2 = 0.12**

![图片](https://mmbiz.qpic.cn/mmbiz_png/Xn6nDZ2tCE3hY4bxicIWnQ5gA81kK0wIaDSvA7YPxIkuZ7ReIAyYPMaWibCicABhNpR2iacyiaIa50AqTonhW51pAaA/640.png?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如上图的实例，影响范围（红色区域）占比总窗口 75% ，箭头（紫色）移动占总窗口高度的 25%，故 0.75 x 0.25 = 0.1875。

**提示：使用 Bit（于 Github 里）可在项目之间共享可复用组件。**

Bit 使得在项目之间共享、记录和复用独立组件变得简单。使用它可以最大限度地复用代码，能够保持设计一致、帮助团队协作、加快交付并构建可扩展的应用程序。

Bit 支持 Node，TypeScript，React，Vue，Angular 等。

![图片](https://mmbiz.qpic.cn/mmbiz_gif/Xn6nDZ2tCE03GN5C3DoW4oMr1qgmicxicyFrUy4u3JvRFKXZeme55cUvbe3iciaS2lfWYfN3nfibOzia0JVHY9ibtduHA/640.png?wx_fmt=gif&wxfrom=5&wx_lazy=1)

示例：探索在 Bit.dev 上共享的可复用的 React 组件

我觉得现在你应该已经很好地理解了 Core Web Vitals 和它们的职责。所以，现在是时候学习如何测量了。

**02**

# **测量 Web Vitals 比你想象的要容易得多**

正如我开始提到的，测量 Web Vitals 是一个简单的过程，任何人都可以做到。实际有很多工具可以用来测量 Web 的重要信息，包括一些浏览器插件。

“Lighthouse、Chrome DevTools、PageSpeed Insights、Chrome UX Report 和 Web Vitals Extension 位列榜首。”

虽然这些工具的用途相同，但可以进一步分为实验室测试工具和现场测试工具两类。

#### **1. 实验室测试工具**

实验室测试工具的主要目的是 在开发过程中测试性能，以确保在发布之前达到所需的标准。ChromeDevTools 和 Lighthouse 可用于在开发环境中测量 Core Web Vitals。

“但是这些实验室测试工具无法测量 FID，因为没有用户来计算其交互性。但是，这些工具使用了一种称为 Total Blocking Time（TBT）的等效测量方法。”

下图显示了使用 Lighthouse 的网页的性能测试结果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/Xn6nDZ2tCE03GN5C3DoW4oMr1qgmicxicy0WdbGib8NEfkLCpf7FoAQJJRMv0W66AYkV8e78m3kAwutaSxoMszNZw/640.png?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

使用 Lighthouse 测量 Core Web Vitals

#### **2. 现场测试工具**

**实验室测试工具的结果不是 100% 准确的，因为没有真正的用户试用网页。**现场测试工具可以用来填补这个漏洞。此外，与实验室测试工具不同的是，现场测试工具可以按原样测量所有 3 个 Core Web Vitals。

**PageSpeed Insights、Chrome UX Report** 和 **Web Vitals Extension** 是一些现场测试工具，我们可以使用这些工具在真实用户交互时测量 Core Web Vitals。这些现场测试工具匿名地从网页上收集实时数据，使我们无需手动运行任何操作即可检查 Vitals。

![图片](https://mmbiz.qpic.cn/mmbiz_png/Xn6nDZ2tCE03GN5C3DoW4oMr1qgmicxicyiceJQSkl2FPibFv5WiaG3stV7ncYBsYqLyyyeNrNBr6C8k5BEVK6GkoFA/640.png?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

使用 Lighthouse 测量 Core Web Vitals

让我们假设你已经测量了网站的 Core web Vitals，而结果并不符合预期。那么，做什么能提高这些分数呢？

# **03**

# **改善 Web Vitals 的步骤**

既然你现在知道如何测量 Web Vitals，那么让我们看看如果存在问题，如何改进你的网站。

众所周知，对于性能相关问题的技术修复并不是那么简单。大多数时候它们非常复杂耗时。但是，可以遵循一些通用的指导方法来改进这些 Core Web Vitals。

**1. 可以通过以下方式改进网站的 LCP：**

- 删除或避免使用消耗太多时间加载的大型页面元素。通过分析前面讨论的测量工具结果，可以很容易地发现这些元素及其影响；

![图片](https://mmbiz.qpic.cn/mmbiz_png/Xn6nDZ2tCE03GN5C3DoW4oMr1qgmicxicyVkZoI9UlFtfPxtQFxldPcbY1I8ibgLwLfIaVbt9S4ux7UV5uFbhNIAw/640.png?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

Lighthouse 分析结果

- 避免不必要的第三方 JavaScript 库。下面的分析表明，使用第三方库已将主线程阻塞 2700 毫秒；

![图片](https://mmbiz.qpic.cn/mmbiz_png/Xn6nDZ2tCE03GN5C3DoW4oMr1qgmicxicymjib3ib2Ol42sEdmVImcNub1GH626sDKa3D8lhccCRFQzZT9QJNoxmdQ/640.png?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

Lighthouse 分析结果

- 设置延迟加载和延迟加载图像；
- 减少服务器响应时间。

**2. 与 LCP 类似，可以遵循以下几点来提高网站的 FID 值：**

- 使用高效的缓存策略更快地加载页面内容；
- 与 LCP 类似，可以通过提交不必要的 JavaScript 库来增强 FID 值；
- 最小化将提高页面加载时间，用户将能够立即与页面交互。

![图片](https://mmbiz.qpic.cn/mmbiz_png/Xn6nDZ2tCE03GN5C3DoW4oMr1qgmicxicypjacnXCQpkJ71CTtPtlwOn2NQjiaFQMz9IG3taGV8IRfsvpHZ0mlWCQ/640.png?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

Lighthouse 分析结果

**3. Core Web Vitals 最终测量的是 CLS，可以通过以下方式提高 CLS 分数：**

- 对图像和视频使用固定尺寸；
- 如果网站存在广告显示，一定要为他们留下必要的空间。

# **结论**

我希望你们已经明白了维护优秀网站的重要性。这些测量方法为保持网站的用户体验友好性提供了有力支持。

尽管这些测量方法非常有前途，但在某些情况下，也需要临时修改这些测量方法来确保良好的用户体验。所以请保持注意。
