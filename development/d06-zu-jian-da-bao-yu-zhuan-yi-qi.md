---
description: Javascript bundler and tranpiler
---

# \[D06\] 组件打包与转译器

## 前端环境的特点与挑战

### 开源生态高度分化

根据Github的统计（[来源](https://octoverse.github.com/)），截止到2019年：

* 62%的开源项目以JS作为主要语言；
* npm平台共发布了350万个包（相比pip上有75万个包）；
* 每个npm包平均只有35名直接贡献者（相比pip每个包有204名）。

可见JS包的分化程度相比其他语言来说较高：包的数量多，代码量和维护量较少。这也侧面说明许多包功能简单且很有可能缺乏维护。打包工具Rollup的作者将npm生态的这一特点归结于npm的发布门槛低，以及前端的多种应用场景所滋生的模块化思想。

尽管模块化思想是前端开发的基本原则，项目过于分化也会产生许多问题。比如小的模块化组件便于开发，但很多情况下由于文档不够完善，或后续维护更新不足，导致用户体验较差；同时平台上发布的包过多容易出现功能重叠、不易查找等问题。因此，如何在坚持模块化的同时简化开发流程和代码效率成为了一个前端生态的热点问题。

### 运行环境复杂

JS代码运行的环境相比其他语言复杂很多。从软件上来看，今天的JS代码一部分用于适配Blink为主的浏览器环境，另一部分用于适配Node为主的非浏览器（如原生app，打包器等开发工具）环境。尽管两者都以ECMA规范为标准，由于规范并不是代码标准，且开发维护的群体不同，具体实施的技术细节也会不同。因此代码在设计时需要考虑到运行环境的转化问题。比如用UMD规范 \(Universial Module Definition\) 同时适配Node和浏览器环境的模块加载： [来源](https://github.com/umdjs/umd/blob/master/templates/nodeAdapter.js)

```javascript
(function(define) {

    define(function (require, exports, module) {
        var b = require('b');

        return function () {};
    });

}( 
    typeof module === 'object' && module.exports && typeof define !== 'function' ?
        function (factory) { 
            module.exports = factory(require, exports, module); 
        } : define
));
```

由于Node和浏览器加载模块的语法不同，调用加载函数时需通过查看函数的属性判定调用的环境。

除此之外，支持不同内核/平台的浏览器也是一个重点问题。根据维基的统计（[来源](https://en.wikipedia.org/wiki/Usage_share_of_web_browsers#StatCounter_%28Jan_2009_to_October_2019%29)）截止到2019年，全世界范围内：

* 54%的流量来自移动端用户；
* 约25%的浏览器不使用Chrome内核；
* 约5%的用户使用不支持ES6的IE浏览器。

随着Web标准不断更新（CSS4、ES7等），新的语法层出不穷（JSX等），兼容性强的代码的开发成本越来越高。针对用户浏览器版本的兼容性也成为了一大难题。

## 构建打包工具 Bundler

### 让模块化开发更快更简单

构建打包工具如Webpack和Rollup很大程度上解决了开源生态分化的问题。开发过程中，大量应用npm包会产生一些问题，而打包工具帮助开发者简化了开发流程，同时对源代码进行优化，使得上线的代码不受模块化开发弊端的影响。

#### 简化包的依赖关系

npm生态上许多包之间互相依赖。一个第三方包出现问题可能导致蝴蝶效应，影响开发效率和生产安全。技术专题网站TechRepublic曾举出一个例子[（来源）](https://www.techrepublic.com/article/why-its-finally-time-for-developers-to-address-the-chaos-of-node-js-and-npm/)：2016年，一个开发者为抗议npm因法律原因下线他的包，从平台上撤下了他的所有作品；由于其中一个包在包括Babel、Node等许多重要的JS应用中被引用，此举影响甚大，以至于npm不得不强行将这个包上线，并从此以后禁止发布超过24小时的包下线。有趣的是，这个至关重要的包唯一的功能就是给代码前添加空格，使代码左端对齐。

这是一个极端的例子，但说明依赖问题至关重要。尽管npm有成熟的机制保证依赖上游的包变化不会导致应用出现问题，手动处理错综复杂的依赖关系会使开发更加困难。打包工具可以自动分析所需的依赖包，提取其中有用的部分，使输出的结果更加有效率。Tree-shaking是Rollup的原生功能；在Webpack 4里可以通过在config.js中注明`usedExports`和`sideEffect`实现。

#### 减少流量优化性能

今天，浏览器使用http/1.x时一般只允许同时保持6个tcp接口（[来源](https://hpbn.co/http1x/#domain-sharding)）。通常情况下，加载一个页面需要不止6个文件的请求，这时额外的请求就会严重降低页面的加载速度。使用打包工具可以将多个JS脚本和CSS合并成一个文件，降低需要的请求量。使用http/2.0时，浏览器采用多线程处理，理论上可以同时接受无限个请求。这时打包工具可以通过code-splitting将组件切割成几份文件以提高流量输出，或根据功能将打包的组件分类，实现动态加载。

主流打包工具一般还会内置Loader \(Webpack\) 和Plugin \(Rollup\)，对打包的JS进行预处理。这些组件可以提前编译需要转换成JS的其他语言的脚本，如TypeScript和React；可以用Babel处理ES6或其他新标准的兼容性问题；还可以打包其他类型的静态资源，如图片或者woff字体文件，让JS来重命名、压缩、并动态插入这些文件。

#### 独立开发和部署

通过解决模块化开发产生的性能和管理问题，打包工具实现了开发和部署的相对独立，使得开发者不需在编写代码时考虑代码以外产生的性能问题，例如上文提到的网络协议请求限制，或者加载多余的包函数的问题。

同时，开源打包工具作为开发流程的独立一环，本身也得益于模块化组件：Webpack的全部功能都由不同的Loader/plugin实现，也有一批开源开发者专门针对打包工具设计组件，形成了自己的开源生态。

### Webpack静态资源管理实例

这里实践了Webpack官方教程上的一个小实例（[来源](https://webpack.js.org/guides/asset-management/)）。

项目架构：

```text
  webpack-demo
  |- package.json
  |- webpack.config.js
  |- /dist
    |- bundle.js
    |- index.html
  |- /src`
    |- style.css
    |- index.js
  |- /node_modules
```

`dist/index.html`:

```markup
<html>
    <head>
        <title>Asset Management</title>
    </head>
    <body>
        <script src="bundle.js"></script>
    </body>
</html>
```

`src/style.css`

```css
.hello {color: red;}
```

`src/index.js`:

```javascript
import _ from 'lodash'; // ES6加载包语法，由Webpack打包进bundle.js
import './style.css'; // 由Webpack打包成简化的string，动态插入index.html

function component() {
    const element = document.createElement('div');
    element.innerHTML = _.join(['Hello', 'webpack'], ' ');
    element.classList.add('hello');

    return element;
}

document.body.appendChild(component());
```

用相应的`Webpack.config.js`打包并在浏览器中打开`index.html`，其中`<head>`元素中已动态插入了css中的样式：

```markup
<head>
    <title>Asset Management</title>
    <style>
    .hello {
        color: red;
    }
    </style>
</head>
```

同时bundle.js已被整合优化。

### Webpack 3 与 4 新特性

#### Webpack 3

**作用域提升 Scope Hoisting**

当Webpack从其他模块加载变量/函数时，会将每个变量/函数用一个IIFE函数包起来，通过内置的模块初始化和加载函数加载后，储存在一个数组里。这种“缓存”机制便于热替换、分段加载等功能的实施，但IIFE函数对性能消耗较大。使用作用域提升时，所有模块函数会被放在一个作用域下，通过重命名防止名称冲突，也减少声明函数的数量和组件的大小，提高性能。（[来源1](https://juejin.im/entry/59704d47f265da6c4977ba6a) [来源2](https://zhuanlan.zhihu.com/p/25954788)）比如如下模块：

```javascript
// module-a.js
export default 'module A'
// entry.js
import a from './module-a'
console.log(a)
```

未经作用域提升时打包成的代码：

```javascript
// bundle.js
// 最前面的一段代码实现了模块的加载、执行和缓存的逻辑，这里直接略过
[
  /* 0 */
  function (module, exports, require) {
    var module_a = require(1)
    console.log(module_a['default'])
  },
  /* 1 */
  function (module, exports, require) {
    exports['default'] = 'module A'
  }
]
```

作用域提升处理后：

```javascript
// bundle.js
[
  function (module, exports, require) {
    // CONCATENATED MODULE: ./module-a.js
    var module_a_defaultExport = 'module A'

    // CONCATENATED MODULE: ./index.js
    console.log(module_a_defaultExport)
  }
]
```

#### Webpack 4

**新的块拆分技术 optimization.splitChunks**

用新的块拆分技术，打包好的组件会按照以下四个原则进行拆分：（[来源](https://gist.github.com/sokra/1522d586b8e5c0f5072d7565c2bee693)）

* 拆分出来的块可以为其他块共享，或者模块来自`node_modules`
* 拆分出来的块大于30kb
* 当按需加载模块时，同时需要加载的模块不超过5个
* 当初始化加载页面时，同时需要加载的模块不超过3个

第一条主要出于缓存的考虑：共享的或第三方的模块相对不经常变化，分拆缓存可降低储存的读写量。后三条则是出于流量和请求数量的考虑：如果模块较小，分拆出去多一次请求的成本可能大于缓存变更的成本。例如：按此方法拆分的如下模块加载代码：

```javascript
// entry.js
import("./a");
import("./b");

// a.js
import "./helpers"; // helpers is 40kb in size
// ...

// b.js
import "./helpers";
import "./more-helpers"; // more-helpers is also 40kb in size
// ...
```

会将`./helpers`单独作为一块分拆，因为其为可以共享的模块，且大小大于30kb。

**新的开发选项**

* 可以选择development或production模式
* 添加默认选项，无需config.js

**其他**

* 添加WebAssembly支持，可编译非web的代码如C++，Rust等
* 支持更多的加载语法选项

[来源](https://auth0.com/blog/webpack-4-release-what-is-new/)

## 转译器 Transpilers

// TODO

