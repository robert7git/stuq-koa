## 什么是Koa？

Koa是Node.js下一代web框架

官方介绍

```
Expressive HTTP middleware for node.js to make web applications and APIs more enjoyable to write. Koa's middleware stack flows in a stack-like manner, allowing you to perform actions downstream then filter and manipulate the response upstream. Koa's use of generators also greatly increases the readability and robustness of your application.

Only methods that are common to nearly all HTTP servers are integrated directly into Koa's small ~550 SLOC codebase. This includes things like content negotiation, normalization of node inconsistencies, redirection, and a few others.

Koa is not bundled with any middleware.
```

由 Express 原班人马打造的 koa，致力于成为一个更小、更健壮、更富有表现力的 Web 框架。使用 koa 编写 web 应用，通过组合不同的 generator，可以免除重复繁琐的回调函数嵌套，并极大地提升常用错误处理效率。Koa 不在内核方法中绑定任何中间件，它仅仅提供了一个轻量优雅的函数库，使得编写 Web 应用和API变得得心应手。


Koa中间件的栈流以类似栈的方式，允许你下行执行动作，然后过滤和操作响应的upstream，这其实是和express有区别的另一个大点。

Koa 应用是一个包含一系列中间件 generator 函数的对象。 这些中间件函数基于 request 请求以一个类似于栈的结构组成并依次执行。 Koa 类似于其他中间件系统（比如 Ruby's Rack 、Connect 等）， 然而 Koa 的核心设计思路是为中间件层提供高级语法糖封装，以增强其互用性和健壮性，并使得编写中间件变得相当有趣。

Koa 包含了像 content-negotiation（内容协商）、cache freshness（缓存刷新）、proxy support（代理支持）和 redirection（重定向）等常用任务方法。 与提供庞大的函数支持不同，Koa只包含很小的一部分，因为Koa并不绑定任何中间件。

## 和Express对比

1）依赖的Node.js版本

Koa 目前需要 >=0.11.x版本的 node 环境。并需要在执行 node 的时候附带 --harmony 来引入 generators 。

express无所谓，目前0.10+都ok，甚至更低版本

2）中间件

和 express 基于的中间件Connect，使用起来差别并不大，思想都是一样的，它里面说的

    增强其互用性和健壮性
    
koa主要是通过Context来处理，避免里每个中间件传递请求和响应，整体来说更方便，而且对es6语法支持更好。

3）流程处理

提供了更丰富的流程处理，默认是generator，组合不同的 generator，可以免除重复繁琐的回调函数嵌套。koa2更是支持了ES 7 stage-3里的async/await

4）异常处理



5）大小

Koa是没有任何中间件捆绑的，连路由都没有内置，所以它更纯粹、干净一些。

Express提供了健壮的路由，集成了少量中间件（其实是独立出去的）


## Koa 1 和 Koa 2

```
➜  koa-benchmark git:(master) ✗ npm i -S koa@1
koa@1.2.0 node_modules/koa
├── error-inject@1.0.0(一样)
├── koa-compose@2.4.0（1是2.4而2是3.1）
├── escape-html@1.0.3(一样)
├── destroy@1.0.4(一样)
├── koa-is-json@1.0.0(一样)
├── fresh@0.3.0(一样)
├── vary@1.1.0(一样)
├── only@0.0.2(一样)
├── statuses@1.2.1(一样)
├── parseurl@1.3.1(一样)
├── content-type@1.0.1(一样)
├── co@4.6.0(只有1有)
├── content-disposition@0.5.1(一样)
├── delegates@1.0.0(一样)
├── http-assert@1.2.0 (deep-equal@1.0.1)(一样)
├── debug@2.2.0 (ms@0.7.1)(一样)
├── mime-types@2.1.10 (mime-db@1.22.0)(一样)
├── type-is@1.6.12 (media-typer@0.3.0)(一样)
├── http-errors@1.4.0 (inherits@2.0.1)(一样)
├── on-finished@2.3.0 (ee-first@1.1.1)(一样)
├── cookies@0.6.1 (keygrip@1.0.1, depd@1.1.0)(一样)
├── accepts@1.3.2 (negotiator@0.6.0)(一样)
└── composition@2.3.0 (any-promise@1.1.0)(只有1有)
➜  koa-benchmark git:(master) ✗ npm i -S koa@2
koa@2.0.0 node_modules/koa
├── error-inject@1.0.0(一样)
├── escape-html@1.0.3(一样)
├── destroy@1.0.4(一样)
├── koa-is-json@1.0.0(一样)
├── fresh@0.3.0(一样)
├── only@0.0.2(一样)
├── vary@1.1.0(一样)
├── statuses@1.2.1(一样)
├── parseurl@1.3.1(一样)
├── content-type@1.0.1(一样)
├── content-disposition@0.5.1(一样)
├── delegates@1.0.0(一样)
├── is-generator-function@1.0.3(只有2有)
├── depd@1.1.0(只有2有)
├── on-finished@2.3.0 (ee-first@1.1.1)(一样)
├── http-errors@1.4.0 (inherits@2.0.1)(一样)
├── type-is@1.6.12 (media-typer@0.3.0)(一样)
├── mime-types@2.1.10 (mime-db@1.22.0)(一样)
├── koa-compose@3.1.0 (any-promise@1.1.0)（1是2.4而2是3.1）
├── http-assert@1.2.0 (deep-equal@1.0.1)(一样)
├── cookies@0.6.1 (keygrip@1.0.1)(一样)
├── koa-convert@1.2.0 (co@4.6.0)(只有2有)
├── debug@2.2.0 (ms@0.7.1)(一样)
└── accepts@1.3.2 (negotiator@0.6.0)(一样)
```

差异如下


只有koa 1有
```
├── co@4.6.0(只有1有)
└── composition@2.3.0 (any-promise@1.1.0)(只有1有)
```

只有koa 2有

```
├── is-generator-function@1.0.3(只有2有)
├── koa-convert@1.2.0 (co@4.6.0)(只有2有)
```

koa 1 和 koa 2 都有，但版本不同
```
├── koa-compose@3.1.0 (any-promise@1.1.0)（1是2.4而2是3.1）
```
## 技术栈变更历史

http://stackshare.io/nodejs/in-stacks


## Why Node.js 4.x？

- es6语法特性支持支持，如generator
- koa是基于node 4+开发的，使用generator、箭头函数等特性