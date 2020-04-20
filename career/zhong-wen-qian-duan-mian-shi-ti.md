# Front-end Notes

## 学习资源

### 技术专题总结

* [https://github.com/amandakelake/blog](https://github.com/amandakelake/blog)
* [https://markyun.github.io/2015/Front-end-Developer-Questions/](https://markyun.github.io/2015/Front-end-Developer-Questions/)
* [http://todomvc.com/](http://todomvc.com/)

### 面试官perspective

* [https://div.io/topic/744](https://div.io/topic/744)



## 问题分类

### 算法

* 统计文章中出现次数最多的单词
  * 哈希表 Hash Table
* 快排时间复杂度，为什么会出现最差情况，怎么解决
  * `O(nlogn)`
* 递归式
  * 代入法
* 正则表达式
  * [https://en.wikipedia.org/wiki/Regular\_expression](https://en.wikipedia.org/wiki/Regular_expression)

### 架构

#### 网络/浏览器

* 域名解析方式
  * [https://www.jianshu.com/p/7ff02b89d909](https://www.jianshu.com/p/7ff02b89d909)
  * A记录（对应IP），MX记录（mail excahnge，指向mail server），CNAME记录（Canonical Name，别名解析）
* **缓存**：强缓存和协商缓存的区别
  * [https://github.com/amandakelake/blog/issues/41](https://github.com/amandakelake/blog/issues/41)
* UDP和TCP是什么？ 它们的区别
  * [https://www.geeksforgeeks.org/differences-between-tcp-and-udp/](https://www.geeksforgeeks.org/differences-between-tcp-and-udp/)
* UDP在什么场景会用到？
  * 视频流量，streaming
  * Protocols: DCHP, DNS
* tcp三次握手四次挥手
  * [https://zhuanlan.zhihu.com/p/53374516](https://zhuanlan.zhihu.com/p/53374516)
* tcp如何保证有效传输及拥塞控制原理
  * 和性增长/乘性降低 [https://en.wikipedia.org/wiki/Additive\_increase/multiplicative\_decrease](https://en.wikipedia.org/wiki/Additive_increase/multiplicative_decrease)
* https具体流程
  * [https://www.jianshu.com/p/650ad90bf563](https://www.jianshu.com/p/650ad90bf563)
* 跨域，实现jsonp
* cookie与session的区别
* 网络攻防xss

#### OS/其他

* 进程和线程是什么?你是怎么理解的?
  * Both processes and threads are independent sequences of execution. The typical difference is that threads \(of the same process\) run in a shared memory space, while processes run in separate memory spaces
* 并发&并行（parallelism vs concurrency）
  * 你吃饭吃到一半，电话来了，你一直到吃完了以后才去接，这就说明你不支持并发也不支持并行。 你吃饭吃到一半，电话来了，你停了下来接了电话，接完后继续吃饭，这说明你支持并发。 你吃饭吃到一半，电话来了，你一边打电话一边吃饭，这说明你支持并行。

### 前端

#### HTML

* 可替换元素/不可替换元素
  * [https://segmentfault.com/a/1190000006835284](https://segmentfault.com/a/1190000006835284)
  * 可替换元素就是浏览器根据元素的标签和属性，来决定元素的具体显示内容。例如浏览器会根据`<img>`标签的`src`属性的值来读取图片信息并显示出来，而如果查看`(x)html`代码，则看不到图片的实际内容；又例如根据`<input>`标签的`type`属性来决定是显示输入框，还是单选按钮等。
* Doctype作用？严格模式与混杂模式如何区分？它们有何意义?
  * Its sole purpose is to prevent a [browser](https://developer.mozilla.org/en-US/docs/Glossary/browser) from switching into so-called [“quirks mode”](https://developer.mozilla.org/en-US/docs/Quirks_Mode_and_Standards_Mode) when rendering a document; that is, the "`<!DOCTYPE html>`" doctype ensures that the browser makes a best-effort attempt at following the relevant specifications, rather than using a different rendering mode that is incompatible with some specifications.
  * 严格模式（standard mode）按照现代标准parse html
  * 混杂模式（quirk mode）兼容旧浏览器（IE5之类）
* HTML5 为什么只需要写 &lt;!DOCTYPE HTML&gt;？
  * HTML5基于[DTD](https://en.wikipedia.org/wiki/Document_type_definition)。之前版本的HTML基于[SGML](https://en.wikipedia.org/wiki/Standard_Generalized_Markup_Language)，需要按照其标准写
* 行内元素（inline-level element）有哪些？块级元素（block-level element）有哪些？ 空（void）元素有那些？
  * [https://developer.mozilla.org/en-US/docs/Web/HTML/Inline\_elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Inline_elements)
  * H5已经不再用这两种分类，mostly used historically
  * 行内元素：`img`（MDN上是inline）`a`, `strong`,`input`,`select`,`iframe`...
  * 块级元素：`div`, `span`, `ul ol il`, `form`...
  * MDN上没有关于void元素的介绍？
* 页面导入样式时，使用link和@import有什么区别？
  * `@import` blocks parallel downloads, meaning that the browser will wait for the imported file to finish downloading before it starts downloading the rest of the content. [https://stackoverflow.com/questions/7199364/import-vs-link](https://stackoverflow.com/questions/7199364/import-vs-link)
  * 一般推荐使用`<link>`
* 常见的浏览器内核有哪些？
  * Chrome: Blink
  * IE: Trident
  * Firefox: Gecko
  * Safari: Webkit
* html5有哪些新特性、移除了那些元素？如何处理HTML5新标签的浏览器兼容问题？如何区分 HTML 和 HTML5？
  * New tags
    * `nav`, `section`, `footer`...
  * New APIs:
    * Local Storage: accessed via `Window.localStorage`
    * Web Worker: run scripts in background threads
* 简述一下你对HTML语义化的理解？
  * Semantic HTML: more readable tag names, like python
* HTML5的离线储存怎么使用，工作原理能不能解释一下？
  * Web Storage API: `localStorage` \(persist when browser is closed\) and `sessionStorage` \(reset when browser is closed\)
  * Cookie \(not H5\)
  * IndexDB
* iframe有那些缺点？
* Label的作用是什么？是怎么用的？
* HTML5的form如何关闭自动完成功能？
* 如何实现浏览器内多个标签页之间的通信? 
  * Modern way: [broadcast channel](https://developer.mozilla.org/en-US/docs/Web/API/Broadcast_Channel_API)
  * Primitive way: `localStorage`
  * Chrome Extension???
* 如何在页面上实现一个圆形的可点击区域？
* 网页验证码是干嘛的，是为了解决什么安全问题？
* tite与h1的区别、b与strong的区别、i与em的区别？
* XML与HTML
  * XML和HTML的最大区别就在于 XML的标签是可以自己创建的，数量无限多，而HTML的标签都是固定的而且数量有限。

#### JS

* js事件循环机制
* 宏任务和微任务
  * [https://juejin.im/post/5b73d7a6518825610072b42b](https://juejin.im/post/5b73d7a6518825610072b42b)
  * Microtask queue vs task queue
* es6说一下有那些内容
  * Promise
  * Class \(syntax sugar\)
  * Arrow function （this指代与一般function不同）
  * let, const（与var相比，let不会溢出define的作用域）
* Object.defineProperty\(\)这个方法有哪些缺点？
* object.create\(\) 原理 ，讲清楚其原理，手写模拟实现它
  * using an existing object as the prototype of the newly created object.
* this的优先级
* new 的实现原理，手写模拟实现它
  * The new operator lets developers create an instance of a user-defined object type or of one of the built-in object types that has a constructor function.
* 原型链，原型链原理，手写实现一个
  * .\_\_proto\_\_
* 闭包是什么？你怎么理解的？举个栗子
  * A **closure** is the combination of a function bundled together \(enclosed\) with references to its surrounding state \(the **lexical environment**\). In other words, a closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.
* Event bubbling
  * When an event happens on an element, it first runs the handlers on it, then on its parent, then all the way up on other ancestors.
* 点透问题。为什么会有点透现象。
  * PC网页上的大部分操作都是用鼠标的，即响应的是鼠标事件，包括`mousedown`、`mouseup`、`mousemove`和`click`事件。一次点击行为，事件的触发过程为：`mousedown` -&gt; `mouseup` -&gt; `click` 三步。
* 介绍JavaScript的基本数据类型。
  * Object and primitives \(number, string, boolean, undefined, null\)
* JavaScript原型，原型链 ? 有什么特点？
  * 
* JavaScript有几种类型的值？你能画一下他们的内存图吗？
  * 堆（heap）：原始数据类型
  * 栈（call stack）：引用数据类型
* Javascript如何实现继承？
* Javascript创建对象的几种方式？
* Javascript作用链域?
* 谈谈This对象的理解。
* 什么是window对象? 什么是document对象?
* null，undefined的区别？
* 写一个通用的事件侦听器函数\(机试题\)。
* \[“1”, “2”, “3”\].map\(parseInt\) 答案是多少？
* 如何阻止冒泡？
* 什么是闭包（closure），为什么要用它？
* javascript 代码中的”use strict”;是什么意思 ? 使用它区别是什么？
* 如何判断一个对象是否属于某个类？
* new操作符具体干了什么呢?
* 用原生JavaScript的实现过什么功能吗？
* Javascript中，有一个函数，执行时对象查找时，永远不会去查找原型，这个函数是？
* 对JSON的了解？
* js延迟加载的方式有哪些？
* Ajax 是什么? 如何创建一个Ajax？
* 同步和异步的区别?
* 如何解决跨域问题?
  * CORS \(Cross-origin resource sharing\): **CORS** \(Cross-Origin Resource Sharing\) is a system, consisting of transmitting [HTTP headers](https://developer.mozilla.org/en-US/docs/Glossary/Header), that determines whether browsers block frontend JavaScript code from accessing responses for cross-origin requests.
  * Preflight: When performing certain types of cross-domain Ajax requests, modern browsers that support CORS will insert an extra "preflight" request to determine whether they have permission to perform the action.
* 页面编码和被请求的资源编码如果不一致如何处理？
* 模块化开发怎么做？
* AMD（Modules/Asynchronous-Definition）、CMD（Common Module Definition）规范区别？
* requireJS的核心原理是什么？（如何动态加载的？如何避免多次加载的？如何 缓存的？）
* 让你自己设计实现一个requireJS，你会怎么做？
* 谈一谈你对ECMAScript6的了解？
* ECMAScript6 怎么写class么，为什么会出现class这种东西?
* 异步加载的方式有哪些？
* document.write和 innerHTML的区别?
  * `document.write` in [deferred](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script#attr-defer) or [asynchronous](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script#attr-async) scripts will be ignored
  * In general, user `innerHTML`
* DOM操作——怎样添加、移除、移动、复制、创建和查找节点?
  * 添加：`parent.appendChile(child)`
  * 移除：`element.remove()`
  * 移动：
  * 复制：
  * 创建：`document.createElement`
  * 查找：`document.getElementById()`
* .call\(\) 和 .apply\(\) 的含义和区别？
* 数组和对象有哪些原生方法，列举一下？
* JS 怎么实现一个类。怎么实例化这个类
* JavaScript中的作用域与变量声明提升？
* 如何编写高性能的Javascript？
* 那些操作会造成内存泄漏？
* 需求：实现一个页面操作不会整页刷新的网站，并且能在浏览器前进、后退时正确响应。给出你的技术实现方案？
* 如何判断当前脚本运行在浏览器还是node环境中？（阿里）
* 移动端最小触控区域是多大？
* 把 Script 标签 放在页面的最底部的body封闭之前 和封闭之后有什么区别？浏览器会如何解析它们？
* 移动端的点击事件的有延迟，时间是多久，为什么会有？ 怎么解决这个延时？（click 有 300ms 延迟,为了实现safari的双击事件的设计，浏览器要知道你是不是要双击操作。）
* 知道各种JS框架\(Angular, Backbone, Ember, React, Meteor, Knockout…\)么? 能讲出他们各自的优点和缺点么?
* Node.js的适用场景？
* 什么是“前端路由”?什么时候适合使用“前端路由”? “前端路由”有哪些优点和缺点?
* 知道什么是webkit么? 知道怎么用浏览器的各种工具来调试和debug代码么?
* 检测浏览器版本版本有哪些方式？
* 我们给一个dom同时绑定两个点击事件，一个用捕获，一个用冒泡，你来说下会执行几次事件，然后会先执行冒泡还是捕获

#### CSS

* 说说block元素和in-line元素？ 二者的不同点和特征有哪些?
  * An inline element has no line break before or after it, and it tolerates HTML elements next to it. 不能设置height和width
  * A block element has some whitespace above and below it and does not tolerate any HTML elements next to it.
* 怎么实现0.5px的线
  * [https://juejin.im/post/5ab65f40f265da2384408a95](https://juejin.im/post/5ab65f40f265da2384408a95)
* scale\(0.5\) scale\(2\) scale\(1\) 分别是怎么样的 ，那scale\(-1\)呢
  * When a coordinate value is outside the \[-1, 1\] range, the element grows along that dimension; when inside, it shrinks. If it is negative, the result a [point reflection](https://en.wikipedia.org/wiki/Point_reflection) in that dimension. A value of 1 has no effect.
* flex方法
* float和position，清除浮动的多种方法
* viewport各个属性值的意义，以及如何实现不用viewport控制用户不能缩放，回答用js监听屏幕宽度。
  * [https://www.w3schools.com/css/css\_rwd\_viewport.asp](https://www.w3schools.com/css/css_rwd_viewport.asp)
* 设计弹出层的具体过程
* css水平垂直居中
  * [https://www.jianshu.com/p/79fb64506fb1](https://www.jianshu.com/p/79fb64506fb1)
  * 水平：块状元素：`margin: auto;` 行内元素：`text-align: center;`
  * 垂直：块级元素`absolute + margin:auto`
* css透明度
* 介绍一下标准的CSS的盒子模型？与低版本IE的盒子模型有什么不同的？
* CSS选择符有哪些？哪些属性可以继承？
  * Selector Combinators: decedent \(space\), children \(&gt;\), siblings \(+, ~\)
  * 可继承：color...
  * 不可继承：border, margin...
* CSS优先级算法如何计算？
  * element &lt; class/attribute selector/pseudo class &lt; id &lt; inline style &lt; `!important`
* CSS3新增伪类有那些？
  * [https://www.cnblogs.com/sklthegoodman/p/css3.html](https://www.cnblogs.com/sklthegoodman/p/css3.html)
  * element: nth-child\(3\) {/\* 第n个元素 \*/}
  * element: only-child {/\* 当父元素只有一个 \*/}
* 如何居中div？如何居中一个浮动元素？如何让绝对定位的div居中？
  * `margin: 0 auto;`
* display有哪些值？说明他们的作用。
  * inline: can't set top/bottom margin or width/height, no line break 
  * block: can set margin and width/height, force line break
  * inline-block: can set margin, no line break
  * flex
  * none
* position的值relative和absolute定位原点是？
  * relative: where the element should be
  * absolute: the ancestor
  * static
  * sticky
* CSS3有哪些新特性？
  * new selectors: `E[attribute=”value”]`, `E[attribute^=”value”]`
* 请解释一下CSS3的Flexbox（弹性盒布局模型）,以及适用场景？
  * 
* 用纯CSS创建一个三角形的原理是什么？
* 一个满屏 品 字布局 如何设计?
* 常见兼容性问题？
* li与li之间有看不见的空白间隔是什么原因引起的？有什么解决办法？
* 经常遇到的浏览器的兼容性有哪些？原因，解决方法是什么，常用hack的技巧 ？
* 为什么要初始化CSS样式。
* absolute的containing block计算方式跟正常流有什么不同？
* CSS里的visibility属性有个collapse属性值是干嘛用的？在不同浏览器下以后什么区别？
* position跟display、margin collapse、overflow、float这些特性相互叠加后会怎么样？
* 对BFC规范\(块级格式化上下文：block formatting context\)的理解？
* 请解释一下为什么会出现浮动和什么时候需要清除浮动？清除浮动的方式
* 移动端的布局用过媒体查询吗？
* 使用 CSS 预处理器吗？喜欢那个？
* CSS优化、提高性能的方法有哪些？
* 浏览器是怎样解析CSS选择器的？
* 在网页中的应该使用奇数还是偶数的字体？为什么呢？
* margin和padding分别适合什么场景使用？
* 抽离样式模块怎么写，说出思路，有无实践经验？
* 元素竖向的百分比设定是相对于容器的高度吗？
* 全屏滚动的原理是什么？用到了CSS的那些属性？
* 什么是响应式设计？响应式设计的基本原理是什么？如何兼容低版本的IE？
* 视差滚动效果，如何给每页做不同的动画？（回到顶部，向下滑动要再次出现，和只出现一次分别怎么做？）
* ::before 和 :after中双冒号和单冒号 有什么区别？解释一下这2个伪元素的作用。
  * pseudo class \(单引号\) vs pseudo element \(双引号\)
* 如何修改chrome记住密码后自动填充表单的黄色背景 ？
* 你对line-height是如何理解的？
* 设置元素浮动后，该元素的display值是多少？（自动变成display:block）
* 怎么让Chrome支持小于12px 的文字？
* 让页面里的字体变清晰，变细用CSS怎么做？（-webkit-font-smoothing: antialiased;）
* font-style属性可以让它赋值为“oblique” oblique是什么意思？
* position:fixed;在android下无效怎么处理？
* 如果需要手动写动画，你认为最小时间间隔是多久，为什么？（阿里）
* display:inline-block 什么时候会显示间隙？\(携程\)
* overflow: scroll时不能平滑滚动的问题怎么处理？
* 有一个高度自适应的div，里面有两个div，一个高度100px，希望另一个填满剩下的高度。
* png、jpg、gif 这些图片格式解释一下，分别什么时候用。有没有了解过webp？
* 什么是Cookie 隔离？（或者说：请求资源的时候不要让它带cookie怎么做）
* style标签写在body后与body前有什么区别？

### Behavior

* 怎么看待前端这个职务
* 为什么会选择前端这个学习方向
* 平时是怎么学习前端的
  * （问题导向为主，MDN上查，偶尔看youtube教程）









