互联网工程任务组：IETF(The Internet Engineering Task Force)

Ajax、响应式设计、JavaScript 框架、ECMAScript Next、CSS Next、Houdini、Indexed DB、Device APIs、Web Bluetooth、Web Socket、Web Payment、[孵化](https://wicg.github.io/BackgroundSync/spec/)中的 [Background Sync API](https://huangxuan.me/2017/02/09/nextgen-web-pwa/developers.google.com/web/updates/2015/12/background-sync)、[Streams](https://streams.spec.whatwg.org/)、WebVR……开放 Web 世界 27 年来的发展以及未来的一切，都与 PWA 天作之合。

[当然，无论与不与原生应用对比，PWA 让 web 应用变得体验更好这件事本身是毋庸置疑的。](https://cloudfour.com/thinks/progressive-web-apps-simply-make-sense/?utm_source=mobilewebweekly&utm_medium=email#fn-4857-1)

[我们仍然还是需要根据自己产品与团队的情况来决定对应的技术选型与平台策略，只是 PWA 让 web 应用在面对选型考验时更加强势了而已。](https://medium.com/@owencm/the-surprising-tradeoff-at-the-center-of-question-whether-to-build-an-native-or-web-app-d2ad00c40fb2#.ym83ct2ax)



## 下一代应用模型PWA

实现 **PRPL**： Push/Preload、Render、Precache、Lazy-Load。

**Push/Preload**：推送，预加载，即，页面加载完成之后，我们希望提前加载深处的资源，减少往返，解析文档的时间。在用户需要使用时，我们可能已经加载好了文件，只需渲染即可。

**Render**：尽快的进行路由渲染，以保证尽快渲染当前页面。对于SSR来说，无需多做。

**Precache**：提前缓存，在后台预缓存我们需要的资源，需要 Service Worker，由服务端进行主动推送内容。

**LAZY-LOAD**：懒加载，

PWA 是 2016 年提出的概念，Progressive Web App，应用 Web 技术实现与原生相近的用户体验。

**安全可靠**

Service Work 技术实现即时下载，当用户打开应用后，页面资源的加载不再完全依赖于网络，而是使用 Service Work 缓存离线包存在本地，确保为用户提供即时可靠的体验。

访问更快

首屏可以部署在服务端，节省网页请求时间，加载速度更快，拥有更平滑的动态效果和快速的页面响应。

响应式界面

支持各种类型和终端的屏幕

沉浸式体验

可以直接将 webapp 放置在主屏幕上，提供沉浸式的全屏幕体验

PWA 的背后并不是某一家或两家公司，而是整个 web 社区与整个 web 规范。**正是因为这种开放与去中心化的力量，使得万维网（World Wide Web）能够成为当今世界上跨平台能力最强、且几乎是唯一一个具备这种跨平台能力的应用平台。**

## 功能模块

### 手机应用配置

(Web App Manifest)

可以通过 使用 manifest 文件以中心化地描述元数据，

### 离线加载与缓存

(Service Worker+Cache API)

可以拦截、处理、响应流经的 HTTP 请求；配合随之引入 Cache Storage API等一系列 Web 技术实现离线加载和缓存。

Service Worker 对 PWA 的重要性相当于 `XMLHTTPRequest` 之于 Ajax，媒体查询（Media Query）之于响应式设计，是支撑 PWA 作为「下一代 web 应用模型」的最核心技术。

由于 Service Worker 可以与包括 Indexed DB、Streams 在内的大部分 DOM 无关 API  进行交互，它的潜力简直无可限量。笔者几乎可以断言，Service Worker 将在未来十年里成为 web  客户端技术工程化的兵家必争之地，带来「离线优先（Offline-first）」的架构革命。

### 消息推动与通知

( Push&Notification )

Notification API 负责所有的和通知相关的机制：通知的权限管理、向操作系统发起通知、通知的类型与音效，以及提供通知被点击或关闭时的回调等等。

Push API

提供了，由服务器向浏览器推送通知的能力。它定义了 web 应用如何向推送服务发起订阅、如何响应推送消息，以及 web 应用、应用服务器与推送服务之间的鉴权与加密机制；由于 Push  API 并不依赖 web 应用与浏览器 UI 存活，所以即使是**在 web 应用与浏览器未被用户打开的时候**，**也可以通过后台进程接受推送消息**并调用  Notification API 向用户发出通知。

实现实时的消息推送与通知

## PWA实战总结

当然，我这里面只收录我认为比较重要的笔记，如果有想看的，下方有链接。

饿了吗项目不是 SPA，是 SSR，所以，在跳转页面时，会出现约一秒的白屏时间（因为浏览器会再次向服务器发起请求，哪怕被拦截，也会因为执行JS的代码，建立Vue虚拟的组件库的依赖，以及 UI 的建立上）。

原文中对这一秒左右的白屏解释为：约一半是消耗在包括 Vue 运行时、组件、库等依赖的运行上，而另一半则花在了业务组件实例化时 Vue 的启动与渲染上。

而缓存可以解决该问题——一定程度上。V8提供代码缓存，编译后，可以将编译后的机器码在本地拷贝一份，下次请求同一个脚本时，一次省略掉请求、解析、编译的所有工作。

另一个缓存功能，进退缓存，就是说，上一页的内容会被浏览器保存，如果进行回退，会直接载入已经渲染好的内容，基本可以实现瞬间加载。但是，chrome因为内存开销，多进程架构的原因，现在并不支持。对于 Chromium 内核霸占的 Android 生态来说，这事更没法指望了。

当然，不能解决问题，我们可以规避问题，使用骨架屏，进行占位。骨架屏，又不能每一个页面写一个骨架，

黄玄（饿了么的 PWA 升级实践）：https://huangxuan.me/2017/07/12/upgrading-eleme-to-pwa/

## 前端的发展

*****

**优势特性**，直接部署服务器即可使用，不需要审核过程并且可以通过技术点的升级，逐步成为一个 app，用于描述 web 应用元数据（metadata）、让 web 应用能够像原生应用一样被添加到主屏、全屏执行的 Web App  Manifest；以及进一步提高 web 应用与操作系统集成能力，让 web 应用能在未被激活时发起推送通知的 Push API 与  Notification API 等等。

甚至让 web 应用可以在离线环境使用的 Service Worker 与 Cache Storage；

**缺点**，技术不成熟，浏览器支持不够全面，依赖第三方库实现（摄像头，语言功能）客户端软件（即网页）需要下载所带来的网络延迟；与 Web 应用依赖浏览器作为入口所带来的体验问题。

基于 Chromium（谷歌的开源项目，由开源社区去维护） 开发的浏览器 Chrome 和 Opera 已经完全支持 PWA 。

互联网行业仿佛在「Web 应用 vs. 原生应用」这个问题上达成了共识：

- web 应用是鱼：迭代快，获取用户成本低；跨平台强体验弱，开发成本低。**适合拉新**。
- 原生应用是熊掌：迭代慢，获取用户成本高；跨平台弱体验强，开发成本高。**适合保活**。

PWA 的出现，让鱼与熊掌兼得变成了可能 —— 它同时具备了 web 应用与原生应用的优点，有着自己独有的先进性：「浏览器 ->  添加至主屏/安装 -> 具备原生应用体验的 PWA -> 推送通知 -> 具备原生应用体验的 PWA」，PWA  自身就包含着从拉新到保活的闭环。

> 出于安全考虑，注册 Service Worker 要求你的 web 应用部署于 HTTPS 协议下，以免利用 Service Worker 的中间人攻击。

> 参考文章：
>
> 黄玄：https://huangxuan.me/2017/02/09/nextgen-web-pwa/#service-worker

奢望着本文能对推动 PWA 的国内环境有一定的贡献。不过无论如何，PWA 在国内的春天可能的确会来得稍微晚一点了。

「[我们信仰 Web，不仅仅在于软件、软件平台与单纯的技术](https://huangxuan.me/pwa-qcon2016/#/99)，还在于[『任何人，在任何时间任何地点，都可以在万维网上发布任何信息，并被世界上的任何一个人所访问到。』而这才是 web 的最为革命之处，堪称我们人类，作为一个物种的一次进化。](http://phonegap.com/blog/2012/05/09/phonegap-beliefs-goals-and-philosophy/)」

请不要让 web 再[继续离我们远去](https://zhuanlan.zhihu.com/p/22561084)，浏览器厂商们已经重新走到了一起，而下一棒将是交到我们 web 应用开发者的手上。[乔布斯曾相信 web 应用才移动应用的未来](https://huangxuan.me/2017/02/09/nextgen-web-pwa/youtu.be/y1B2c3ZD9fk?t=1h14m48s)，那就让我们用代码证明给这个世界看吧。

**让我们的用户，也像我们这般热爱 web 吧。**