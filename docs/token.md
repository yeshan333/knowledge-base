# 术语大锅烩

>目前，大部分内容来源于网络，如有侵权请告知

## 花里胡哨之道

### SPA

spa？

>**single-page application(SPA，单页应用)**
>只有一张Web页面的应用，是一种从Web服务器加载的富客户端，单页面跳转仅刷新局部资源 ，公共资源(js、css等)仅需加载一次，常用于PC端官网、购物等网站。

[前端：你要懂的单页面应用和多页面应用](https://juejin.im/post/5a0ea4ec6fb9a0450407725c)

[一种SPA（单页应用）架构](https://github.com/livoras/blog/issues/3)

### SSR

>**Server-Side Rendering(SSR，又称同构应用)**
>通常来说web页面的数据渲染都是由客户端或者浏览器端来完成的，先从服务器请求，然后到页面，再通过ajax请求到页面数据，之后把相应的数据填充到template模板形成完整的页面来呈现给用户。服务端渲染把数据的ajax请求放在了服务端，然后服务端把数据填充到template模板形成完整的页面，由服务端把渲染的完整的页面吐给客户端。这样减少了一次客户端到服务端的http请求，加快了相应速度，一般用于首屏的性能优化。
>当前对于单页应用(SPA)，搜索引擎并不能收录到 ajax 爬取数据之后然后再动态 js 渲染出来的页面。用SSR，Debug有点伤😟

[Vue SSR指南](https://ssr.vuejs.org/zh/)

[精读前后端渲染之争](https://github.com/camsong/blog/issues/8)

[Redux 服务端渲染](https://www.redux.org.cn/docs/recipes/ServerRendering.html)

### PWA

>**Progressive web apps，渐进式 Web 应用**
>PWA应用是指那些使用指定技术和标准模式来开发的web应用，这将同时赋予它们web应用和原生应用的特性。Web应用易于访问，原生应用（Native）可与操作系统完美整合，为用户提供无缝的用户体验（UX）。

[MDN web docs：渐进式 web 应用介绍](https://developer.mozilla.org/zh-CN/docs/Web/Progressive_web_apps/Introduction)

[service-worker](https://developers.google.com/web/fundamentals/primers/service-workers)

### TDD

>Test-Driven Development，测试驱动开发

功能测试(functional tests)：用户角度，从外部测试应用。

单元测试(unittest)：开发者角度，从内部测试应用。单元测试由功能测试驱动，最少的代码干掉失败测试。

### Pipe and Filter

### 领域模型 & 业务模型

## UX/UI

## Hybrid