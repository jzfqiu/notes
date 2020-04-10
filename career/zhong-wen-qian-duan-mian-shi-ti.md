# 中文前端面试题

* 统计文章中出现次数最多的单词
  * 哈希表 Hash Table
* 快排时间复杂度，为什么会出现最差情况，怎么解决
  * `O(nlogn)` 
* 域名解析方式
  * [https://www.jianshu.com/p/7ff02b89d909](https://www.jianshu.com/p/7ff02b89d909)
  * A记录（对应IP），MX记录（mail excahnge，指向mail server），CNAME记录（Canonical Name，别名解析）
* 递归式说一下
  * 代入法
* 304状态
* 强缓存和协商缓存的区别
  * [https://github.com/amandakelake/blog/issues/41](https://github.com/amandakelake/blog/issues/41)
* js事件循环机制
* 宏任务和微任务
  * [https://juejin.im/post/5b73d7a6518825610072b42b](https://juejin.im/post/5b73d7a6518825610072b42b)
  * Microtask queue vs 
* 正则表达式
  * [https://en.wikipedia.org/wiki/Regular\_expression](https://en.wikipedia.org/wiki/Regular_expression)
* 匹配QQ号
* es6说一下有那些内容
  * Promise
  * Class \(syntax sugar\)
  * Arrow function （this指代与一般function不同）
  * let, const（与var相比，let不会溢出define的作用域）
* 怎么看待前端这个职务
* 为什么会选择前端这个学习方向
* 平时是怎么学习前端的
  * （问题导向为主，MDN上查，偶尔看youtube教程）
* Object.defineProperty\(\)这个方法有哪些缺点？
* 订阅发布者模式和观察者模式的区别
* this的优先级
* 扩展到 object.create\(\) 原理 ，讲清楚其原理，手写模拟实现它
  * using an existing object as the prototype of the newly created object.
* new 的实现原理，手写模拟实现它
  * The new operator lets developers create an instance of a user-defined object type or of one of the built-in object types that has a constructor function.
* 原型链，原型链原理，手写实现一个
  * .\_\_proto\_\_
* 闭包是什么？你怎么理解的？举个栗子
  * A **closure** is the combination of a function bundled together \(enclosed\) with references to its surrounding state \(the **lexical environment**\). In other words, a closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.
* UDP和TCP是什么？ 它们的区别
  * [https://www.geeksforgeeks.org/differences-between-tcp-and-udp/](https://www.geeksforgeeks.org/differences-between-tcp-and-udp/)
* UDP在什么场景会用到？
  * 直播吧
* 进程和线程是什么?你是怎么理解的?
  * Both processes and threads are independent sequences of execution. The typical difference is that threads \(of the same process\) run in a shared memory space, while processes run in separate memory spaces.
* 说说block元素和in-line元素？ 二者的不同点和特征有哪些?
  * An inline element has no line break before or after it, and it tolerates HTML elements next to it. 不能设置height和width
  * A block element has some whitespace above and below it and does not tolerate any HTML elements next to it.
* 可替换元素/不可替换元素
  * [https://segmentfault.com/a/1190000006835284](https://segmentfault.com/a/1190000006835284)
  * 可替换元素就是浏览器根据元素的标签和属性，来决定元素的具体显示内容。

    > 例如浏览器会根据`<img>`标签的`src`属性的值来读取图片信息并显示出来，而如果查看`(x)html`代码，则看不到图片的实际内容；又例如根据`<input>`标签的`type`属性来决定是显示输入框，还是单选按钮等。
* 怎么实现0.5px的线
  * [https://juejin.im/post/5ab65f40f265da2384408a95](https://juejin.im/post/5ab65f40f265da2384408a95)
* scale\(0.5\) scale\(2\) scale\(1\) 分别是怎么样的 ，那scale\(-1\)呢
  * When a coordinate value is outside the \[-1, 1\] range, the element grows along that dimension; when inside, it shrinks. If it is negative, the result a [point reflection](https://en.wikipedia.org/wiki/Point_reflection) in that dimension. A value of 1 has no effect.
* flex方法
* float和position，清除浮动的多种方法
* Event bubbling
  * When an event happens on an element, it first runs the handlers on it, then on its parent, then all the way up on other ancestors.
* viewport各个属性值的意义，以及如何实现不用viewport控制用户不能缩放，回答用js监听屏幕宽度。
  * [https://www.w3schools.com/css/css\_rwd\_viewport.asp](https://www.w3schools.com/css/css_rwd_viewport.asp)
* 设计弹出层的具体过程
* css水平垂直居中
  * [https://www.jianshu.com/p/79fb64506fb1](https://www.jianshu.com/p/79fb64506fb1)
  * 水平：块状元素：`margin: auto;` 行内元素：`text-align: center;`
  * 垂直：块级元素`absolute + margin:auto`
* css透明度
* 点透问题。为什么会有点透现象。
  * PC网页上的大部分操作都是用鼠标的，即响应的是鼠标事件，包括`mousedown`、`mouseup`、`mousemove`和`click`事件。一次点击行为，事件的触发过程为：`mousedown` -&gt; `mouseup` -&gt; `click` 三步。
* http缓存机制
* 五星好评点几颗星亮几颗，用css
* 实现查询字符串中出现最多次数的字符，用js写代码
  * 
* tcp三次握手四次挥手
  * [https://zhuanlan.zhihu.com/p/53374516](https://zhuanlan.zhihu.com/p/53374516)
* tcp如何保证有效传输及拥塞控制原理
  * 和性增长/乘性降低 [https://en.wikipedia.org/wiki/Additive\_increase/multiplicative\_decrease](https://en.wikipedia.org/wiki/Additive_increase/multiplicative_decrease)
* https具体流程
  * [https://www.jianshu.com/p/650ad90bf563](https://www.jianshu.com/p/650ad90bf563)
* 并发并行
  * 你吃饭吃到一半，电话来了，你一直到吃完了以后才去接，这就说明你不支持并发也不支持并行。 你吃饭吃到一半，电话来了，你停了下来接了电话，接完后继续吃饭，这说明你支持并发。 你吃饭吃到一半，电话来了，你一边打电话一边吃饭，这说明你支持并行。

跨域，实现jsonp。

网络攻防xss。

cookie与session的区别。

微信小程序生命周期

一段js代码判断哪个先输出。

关于js请求需要时间的问题。

深克隆问题。

vue双向数据绑定

this指向问题，改进，用了箭头函数与call，随后让写call的实现

第二个问题是关于栈，手写实现1秒输出1，2秒输出3，4秒输出2

第三个问题就是谈到我自己动手做的小作品了，rem啦，vue在移动端为什么会有滚动失效的原因，这个我没回答出来，忘了。还有音乐播放器的具体实现。

接着就问我一般如何学习。

