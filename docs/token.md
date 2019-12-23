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

>功能测试(functional tests)：用户角度，从外部测试应用。

>单元测试(unittest)：开发者角度，从内部测试应用。单元测试由功能测试驱动，最少的代码干掉失败测试。

![http://www.obeythetestinggoat.com/book/chapter_philosophy_and_refactoring.html#_recap_the_tdd_process](_media/TDD.png)

### Pipe and Filter

### 领域模型 & 业务模型

## UX/UI

![UI/UX Designer](https://img.vim-cn.com/fb/de0173478bfa210942fc057dfd54ff8ed74017.png)

![Design Principles](https://img.vim-cn.com/5d/140f4e4fe5718d19aa5d1611851833c511ce75.jpg)

![Creative UX Process](https://img.vim-cn.com/ac/ee0a1f1c717ee1be4b9896d48715edc441b751.jpg)


- [7 steps to become a UI/UX designer](https://blog.nicolesaidy.com/7-steps-to-become-a-ui-ux-designer-8beed7639a95)

- [Principles of Design Quick Reference Poster](https://paper-leaf.com/blog/2012/10/principles-of-design-quick-reference-poster/)

- [GOodUI](https://goodui.org/#ideas-1)

### PPI

>每英寸像素（PPI，Pixels Per Inch），又称像素密度。1 英寸(in)= 2.54 厘米(cm)。PPI是一个表示打印图像或者显示器单位面积上像素数量的指数。一般用来计量电脑显示器，电视机和手持电子设备屏幕的精细程度。通常情况下，每英寸像素值越高，屏幕能显示的图像也越精细。电脑与手机屏幕的每英寸像素值取决于尺寸和分辨率，通常指的就是每英寸上的像素点数。

$$ PPI = \frac{\sqrt{w_p^2 + h_p^2}}{d_i} $$

其中：

- $ d_i $ 为屏幕对角线长度，单位英寸
- $ w_p $ 为屏幕横向分辨率
- $ h_p $ 为屏幕纵向分辨率

例如一台屏幕尺寸为 $ 4 $ 英寸，分辨率为 $ 1136\times640 $ 的phone的PPI为

$$ PPI = \frac{\sqrt{1136^2 + 640^2}}{4}=326 $$

### Web Design

[如何还原像素级别的设计稿](https://yujiangshui.com/how-to-restore-the-design-draft-pixel-level/#%E4%BD%BF%E7%94%A8%E9%A9%AC%E5%85%8B%E9%B3%97%E9%87%8F%E5%8F%96%E7%B2%BE%E5%87%86%E5%B0%BA%E5%AF%B8)

## Hybrid