---
layout:     post
title:      Web前端-Lec09 Node.js
subtitle:   Web前端笔记
date:       2023-04-17
author:     ukrys
header-img: img/post-bg-js-version.jpg
catalog: 	 true
tags:
    - Web
    - Notes
    - node
---

## Lecture9 Node.js

### 9.1 静态网页与动态网页

- 静态页面
  - 客户/消费者的观点：一个url指向同一个html文件
  - 服务器/生产者的观点：存储在Web服务器根文件夹内或子文件夹内的文件
  - HTML文件：无论何时当一个特定资源被请求的时候都返回相同的被硬编码的内容
  - 可以直接在浏览器上显示
- 动态页面
  - 客户/消费者的观点：url指的是动态html（可能每次请求都不同）
  - 服务器/生产者的观点：程序/脚本生成html
  - 它不是一个html，而是一个程序产生的html(s)，页面通常是通过将数据库的数据植入到HTML模板中的占位符中而产生的。
  - 不能直接在浏览器中显示

#### 9.1.1 服务端编程

- 服务器端页面是使用多种web编程语言/框架之一编写的程序
  - 例如：PHP，Java/JSP，Ruby on Rails，ASP.NET，Python，Perl
- 每种语言/框架都有其优点和缺点

- 服务端编程的优势
  - 信息的高效存储和传输
  - 定制用户体验
  - 控制对内容的访问
  - 存储会话和状态信息
  - 通知和通讯
  - 数据分析

### 9.2 Node.js

- Node（正式名称 Node.js）是一个开源的、跨平台的运行时环境
- 服务器Javascript：开发人员可以使用JavaScript创建各种服务器端工具和应用程序
- 事件驱动，异步I/O框架
- 性能：在v8之上的c++内核
- 在单一进程中可以最小的开销（cpu/内存）处理成千上万的并发连接
- 模块系统
- 不是一个web框架，也不是一种语言

[![pSuaXxs.png](https://s1.ax1x.com/2023/01/12/pSuaXxs.png)](https://imgse.com/i/pSuaXxs)

| ![image-20230112165204946](C:\Users\94327\AppData\Roaming\Typora\typora-user-images\image-20230112165204946.png) | [![pSudFG4.png](https://s1.ax1x.com/2023/01/12/pSudFG4.png)](https://imgse.com/i/pSudFG4) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |

#### 9.2.1 Node.js 事件循环

不惜一切代价避免同步代码，因为它会阻塞事件循环。这意味着：回调、回调和更多回调

[![pSuwYp4.png](https://s1.ax1x.com/2023/01/12/pSuwYp4.png)](https://imgse.com/i/pSuwYp4)

- 事件驱动模型：由一个事件收集器、一个事件发送器和一个事件处理器组成。

| ![image-20230112165903116](C:\Users\94327\AppData\Roaming\Typora\typora-user-images\image-20230112165903116.png) |
| :----------------------------------------------------------: |
| [![pSuwrtO.png](https://s1.ax1x.com/2023/01/12/pSuwrtO.png)](https://imgse.com/i/pSuwrtO) |

#### 9.2.2 Node.js 支持 JavaScript

- 这是 Node.js 能够发展壮大的⼀个非常重要的间接原因。
  - 首先，Javascript 作为前端⼯程师的主力语言，在技术社区中有相当的号召力。而且，随着 Web 技术的不断发展，特别是前端的重要性增加，不少前端工程师开始试水”后台应用“，在许多采用 Node.js 的企业中，⼯程师都表示因为习惯了 Javascript，所以选择 Node.js。 
  - 其次，Javascript 的匿名函数和闭包特性非常适合**事件驱动**、**异步编程**。 
  - 有 Google V8 引擎的加持，Node.js 的性能也是受益其中。

- 同步 vs 异步

  | 同步                                 | 异步                                   |
  | ------------------------------------ | -------------------------------------- |
  | 等待每个操作完成，然后执行下一个操作 | 从不等待每个操作完成，一次执行所有操作 |
  | 一步一步执行                         | 回调，用于处理结果                     |

  - 同步式I/O 和 异步式I/O 的特点

    | 同步式 I/O (阻塞式)                  | 异步式 I/O (非阻塞式)      |
    | ------------------------------------ | -------------------------- |
    | 利⽤多线程提供吞吐量                 | 单线程即可实现高吞吐量     |
    | 通过时间片分割和线程调度利用多核CPU  | 通过功能划分利用多核CPU    |
    | 需要由操作系统调度多线程使用多核 CPU | 可以将单进程绑定到单核 CPU |
    | 难以充分利用 CPU 资源                | 可以充分利用 CPU 资源      |
    | 内存轨迹大 ，数据局部性弱            | 内存轨迹小，数据局部性强   |
    | 符合线性的编程思维                   | 不符合传统编程思维         |

- 阻塞 vs 非阻塞

  阻塞 是指在 Node.js 程序中，其它 JavaScript 语句的执⾏， 必须等待⼀个非 JavaScript 操作完成。这是因为当阻塞发生时，事件循环无法继续运行 JavaScript。

  在 Node.js 中，JavaScript 由于执行 CPU 密集型操作，而不是等待⼀个非 JavaScript 操作（例如 I/O）而表现不佳，通常不被称为阻塞。在 Node.js 标准库中使用 libuv 的同步方法是最常用的阻塞操作。原生模块中也有阻塞方法。

  在Node.js标准库中的所有I/O方法都提供异步版本，非阻塞， 并且接受回调函数。某些方法也有对应的阻塞版本，名字以 Sync 结尾。

  | 示例：从文件中读取数据并显示数据<br />![pSu0xsA.png](https://s1.ax1x.com/2023/01/12/pSu0xsA.png)	](https://imgse.com/i/pSu0xsA) |
  | ------------------------------------------------------------ |

  - 阻塞

    - 同步 文件读取

      - 从文件读取数据；显示数据；完成其他任务

      ```javascript
      var data = fs.readFileSync("test.txt");
      console.log(data);
      console.log("Do other tasks");
      ```

  - 非阻塞

    - 异步：

      - 从文件中读取数据：当读取数据完成时，显示数据

    - 完成其他任务

      ```javascript
      fs.readFile("test.txt", function(err, data){
          console.log(data);
      })
      ```

#### 9.2.3 Node Package Manager (NPM)

- www.npmjs.org

- 1450.000+ modules

- package.json 文件 (npm init)

- npm install <module.name> --save

  ```
  npm install echarts
  * 会把echarts包安装到node_modules目录中
  * 不会修改package.json
  * 之后运行npm install命令时，不会自动安装echarts
  ```

  ```
  npm install echarts --save
  * 会把echarts包安装到node_modules目录中
  * 会在package.json的dependencies属性下添加echarts
  * 之后运行npm install命令时，会自动安装echarts到node_modules目录中
  * 之后运行npm install –production或者注明NODE_ENV变量值为production时，会自动安装echarts到node_modules目录中
  ```

  ```
  npm install echarts --save-dev
  * 会把echarts 包安装到node_modules目录中
  * 会在package.json的devDependencies属性下添加echarts
  * 之后运行npm install命令时，会自动安装echarts 到node_modules目录中
  * 之后运行npm install –production或者注明NODE_ENV变量值为production时，不会自动安装echarts 到node_modules目录中
  ```

##### 9.2.3.1 package.json

- 项目信息
  - `name` 项目名称
  - `version` 项目的版本号
  - `description` 项目的描述信息
  - `entry point` 项目的入口文件
  - `test command` 项目启动时脚本命令
  - `git repository` 如果你有Git地址，可以将这个项目放到你的Git仓库里
  - `keywords` 关键词
  - `author` 作者名字
  - `license` 项目要发行的时候需要的证书，平时玩玩忽略即可

#### 9.2.4 Node.js API

- Without DOM manipulation

[![pSuDPmR.png](https://s1.ax1x.com/2023/01/12/pSuDPmR.png)](https://imgse.com/i/pSuDPmR)

#### 9.2.5 Node.js 流行模块

- Express.js 由核心Node 项⽬团队的成员之⼀ TJ Holowaychuk 构建。大型社区支持此框架，因此具有不断更新和改革所有核心功能的优势。这是⼀个极简主义的框架， 用于构建 mobile 应用程序和 API。

  Koa 由创建 Express.js 的同⼀团队开发，通常被称为下⼀代 NodeJS 框架。 Koa 的独特之处在于它使用了⼀些非常酷的 ECMAScript （ES6）方法 ，使你无需回调即可工作，同时极大地扩展了错误处理。

  Hapi 是⼀个强大且健壮的框架，用于开发API。完善的插件系统和各种关键功能（例如输入验证、基于配置的功能、实现缓存、错误处理、日志记录等）使 Hapi 成为最受欢迎的框架之⼀。它用于构建有用的应用，并通为 PayPal，Disney 等多个大型网站提供技术解决方案。Hapi 以最小的开销构建安全、强大、可扩展的开箱即用的功能。

  Socket.io用于构建实时 Web 应用。这是⼀个 Javascript 库，可在 Web 客户端和服务器之间进行双向数据通信。 异步数据 I/O、⼆进制流和即时消息传递是此框架最重要的功能。

  Meteor.JS 是最常用的 NodeJS 框架之⼀。 NodeJS 的全栈框架，允许用户构建实时应用程序。它用于创建基于移动和基于 Web 的 javascript 应用。

- 两种模块，不兼容
  - ES6 模块，简称 ESM
  - Node.js 专用的 CommonJS 模块， 简称 CJS

>  [模块化（CommonJS、ES6中的模块化）](https://blog.csdn.net/smx_123/article/details/128290002?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EAD_ESQUERY%7Eyljh-1-128290002-blog-126417920.pc_relevant_landingrelevant&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EAD_ESQUERY%7Eyljh-1-128290002-blog-126417920.pc_relevant_landingrelevant&utm_relevant_index=2)

##### 9.2.5.1 ES6模块与CommonJS模块的差异

- 语法：

  - CommonJS 模块使用 require()加载和module.exports输出

    ```javascript
    var http = require('http');
    var fs = require('fs');
    var express = require('express');
    ```

  - ES6 模块使用import和export

    ```javascript
    // profile.js
    var firstName = 'Michael';
    var lastName = 'Jackson';
    var year = 1958;
    export {firstName, lastName, year};
    
    // main.js
    import {firstName, lastName, year} from './profile';
    console.log(firstName, lastName); // Michael Jackson
    ```
    
    ``` javascript
    /* as */
    
    // main.js
    import {lastName as surname} from './profile';
    console.log(surname);	// Jackson
    
    // profile.js
    export {firstName as name}
    ```
    
    ```javascript
    /* export default */
    
    // default.js
    function add(a, b){
        return a+b;
    }
    export default add;
    /* 实际上 */
    export {add as default};
    
    // main.js
    import add from './default'
    /* 实际上add名字可以随便起 */
    import {default as add} from './default'
    ```

- 差异：

  - CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用
  - CommonJS 模块是运行时加载，ES6 模块是编译时输出接口。
    - CommonJS 加载的是一个对象（即module.exports属性），该对象只有在脚本运行完才会生成。
    - ES6 模块不是对象，它的对外接口只是一种静态定义，在代码解析阶段就会生成。

- 模块加载的实质：

  ```javascript
  /* CommonJS */
  
  // lib.js
  var counter = 3;
  function incCounter(){
      counter++;
  }
  module.exports = {
      counter: counter,
      incCounter: incCounter,
  };
  
  // main.js
  var mod = require('./lib');
  
  console.log(mod.counter);	// 3
  mod.incCounter();
  console.log(mod.counter); 	// 3
  ```

  ```javascript
  /* ES6 */
  
  // lib.mjs
  export let counter = 3;
  export function incCounter(){
      counter++;
  }
  
  // main.mjs
  import {counter, incCounter} from './lib.mjs';
  console.log(counter);	// 3
  incCounter();
  console.log(counter);	// 4
  ```

##### 9.2.5.2 Node.js的区分

- Node.js 要求 ES6 模块采用 `.mjs`后缀文件名
  - 只要脚本文件里面使用import或者export命令，那么就必须采用.mjs后缀名。 Node.js 遇到.mjs文件，就认为是 ES6 模块，默认启⽤严格模式，不必在每个模块文件顶部指定"use strict"。
  - 如果不希望将后缀名改成.mjs，可以在项⽬的package.json⽂件中，指定type字段为module。
- `.cjs` 文件总是以 CommonJS 模块加载
  - 如果没有type字段，或者type字段为commonjs，则.js脚本会被解释成 CommonJS 模块。
- `.js` 文件的加载取决于package.json里面type字段的设置
- 注意，ES6 模块与 CommonJS模块尽量不要混用！！！
  - require命令不能加载.mjs⽂件，会报错，只有import命令才可以加载.mjs⽂件。
  - 反之，.mjs⽂件⾥⾯也不能使⽤require命令，必须使⽤import。

##### 9.2.5.3 同时支持两种格式的模块

- 如果原始模块是 ES6 格式，那么需要给出⼀个整体输出接⼝，比如 export default obj，使得 CommonJS 可以用import()进行加载。

- 如果原始模块是 CommonJS 格式，那么可以加⼀个包装层。

  ```javascript
  import cjsModule from '../index.js';
  export const foo = cjsModule.foo;
  ```

- 可以把这个文件的后缀名改为.mjs，或者放在⼀个子目录，再在这个子目录里面放⼀个单独的package.json文件，指明{ type: "module" }。

- 另⼀种做法是在package.json⽂件的exports字段，指明两种格式模块各自的加载入口。

  ```javascript
  "exports":{
      "require": "./index.js",
      "import": "./esm/wrapper.js"
  }
  ```

| require方法查找策略<br />[![pSK9tGn.png](https://s1.ax1x.com/2023/01/13/pSK9tGn.png)](https://imgse.com/i/pSK9tGn) |
| :----------------------------------------------------------: |
| [![pSKCizq.png](https://s1.ax1x.com/2023/01/13/pSKCizq.png)](https://imgse.com/i/pSKCizq) |

- 循环加载

  ```javascript
  /* CommonJS */
  
  // a.js
  exports.done = false;
  var b = require('./b.js');// 注意，此时a.js代码就停在这里，等待b.js执行完毕，再往下执行。
  console.log('在a.js之中，b.done = %j', b.done);
  exports.done = true;
  console.log('a.js 执行完毕');
  
  // b.js
  exports.done = false;
  var a = require('./a.js');
  console.log('在 b.js 之中，a.done = %j', a.done);
  exports.done = true;
  console.log('b.js 执⾏完毕');
  
  // main.js
  var a = require('./a.js');
  var b = require('./b.js');
  console.log('在 main.js 之中, a.done=%j, b.done=%j',a.done, b.done);
  
  /*  result:
   * 	在 b.js 之中，a.done = false
   *	b.js 执行完毕
   *	在 a.js 之中，b.done = true
   *	a.js 执行完毕
   *	在 main.js 之中, a.done=true, b.done=true
   */ 
  ```

  ```javascript
  /* ES6 */
  
  // a.mjs
  import {bar} from './b.mjs';	// 开始编译b模块，代码停留在这里
  console.log('a.mjs');
  console.log(bar);
  export let foo = 'foo';
  
  // b.mjs
  import {foo} from './a.mjs';	// a模块还在编译阶段
  console.log('b.mjs');
  console.log(foo);				// foo未被初始化 报错
  export let bar = 'bar';
  
  /*  
   *  $ node --experimental-modules a.mjs
   *	b.mjs
   *	ReferenceError: Cannot access 'foo' beforeinitialization
   */
  ```

  ```javascript
  /* ES6 */
  
  // a.mjs
  import {bar} from ‘./b.mjs’;
  console.log('a.mjs');
  console.log(bar());
  function foo() { return 'foo' }
  export {foo};
  
  // b.mjs
  import {foo} from ‘./a.mjs';
  console.log('b.mjs');
  console.log(foo());
  function bar() { return 'bar' }
  export {bar};
  
  /*  
   *  $ node --experimental-modules a.mjs
   *	b.mjs
   *	foo
   *	a.mjs
   *	bar
   */
  ```

#### 9.2.6 Node.js 版本

- LTS 和 Current 其实并不是版本，而是同一个主版本号的不同阶段
  - LTS：Long Term Support。该版本进⼊了漫长的维护期。它又分为两个阶段：Active LTS和Maintenance LTS。 从以往的发布历史看，LTS至少会被跟进2年时间，按照最新的官方网站的说法，Active LTS持续12个月，Maintenance LTS将会被持续维护18个月的时间。Nodejs 12之前，active阶段持续18个月，maintenance阶段持续12个月。
  - Current：一个新主版本号release后，先进入Current阶段，该阶段持续6个月，目的是给各个库（library）的作者时间来支持新版。偶数版本在Current阶段后进入LTS阶段，而奇数版本则终结不再维护。
- 奇偶版本号
  - Nodejs主版本号（semver-major）奇数版本和偶数版本有不同的生命周期
  - 每隔6个月，社区会从Nodejs master分支拉出一个分支作为主版本的release。偶数版本在4月发版，奇数版本则在10月。
  - 奇数版本发版时，上一个偶数版本会进入LTS阶段，而奇数版本则只持续6个月的事件，则终结不再维护。

### 9.3 MEAN

​	MEAN 是一个 Javascript 平台的现代Web开发框架总称

- **M**ongoDB 是一个使用 JSON风格存储的数据库，非常适合Javascript。（JSON是JS数据格式）
- **E**xpressJS 是一个Web应用框架，提供有帮助的组件和模块帮助建立一个网站应用。
- **A**ngularJS 是一个前端MVC框架。
- **N**ode.js 是一个并发 异步 事件驱动的Javascript服务器后端开发平台。

[![pSKnhLj.png](https://s1.ax1x.com/2023/01/13/pSKnhLj.png)](https://imgse.com/i/pSKnhLj)

#### 9.3.1 Web 框架

| 框架名称             | 特性                             | 点评                                                         |
| -------------------- | -------------------------------- | ------------------------------------------------------------ |
| Express              | 简单、实用、路由中间件等五脏俱全 | 最著名的Web框架                                              |
| Derby.js  &&  Meteor | 同构                             | 前后端都放到一起，模糊了开发便捷，看上去更简单，实际上对开发来说要求更高 |
| Sails 、Total        | 面向其他语言，Ruby、PHP等        | 借鉴业界优秀实现，也是Node.js 成熟的一个标志                 |
| MEAN.js              | 面向架构                         | 类似于脚手架，又期望同构，结果只是蹭了热点                   |
| Hapi 和 Restfy       | 面向Api && 微服务                | 移动互联网时代Api的作用被放大，故而独立分类。尤其是对于微服务开发更是利器 |
| ThinkJS              | 面向新特性                       | 借鉴ThinkPHP，并慢慢走出自己的一条路，对于Async函数等新特性支持，无出其右 |
| Koa                  | 专注于异步流程改进               | 下一代Web框架                                                |

#### 9.3.2 NodeJS 框架的优势

现在 NodeJS 框架正在成为最常用的构建 Web 应⽤前后端的开发框架。这是自定义 Web 开发的首4选环境。让我们检查⼀些主要的NodeJS框架的优点：

- 实时工作环境、简单的编码经验、无缝数据流、在整个开发过程中使用相同的代码模式、方便易用

#### 9.3.3 框架选型

- 业务场景、特点
- 自身团队能力、喜好，有时候技术选型决定团队氛围的，需要平衡激进与稳定
- 熟悉程度
- 个人学习求新，企业架构求稳，无非喜好与场景而已

**预处理器：**

| 名称        | 实现                           | 描述                                                 |
| ----------- | ------------------------------ | ---------------------------------------------------- |
| 模板引擎    | art\mustache\ejs\hbs\j ade …   | 上百种之多，自定义默认，编译成html，继而完成更多操作 |
| css预处理器 | less\sass\scss\rework \postcss | 自定义语法规则，编译成css                            |
| js友好语言  | coffeescript、 typescript      | 自定义语法规则、编译成js                             |

**跨平台：**

| 平台     | 实现                                                    | 点评                                                         |
| -------- | ------------------------------------------------------- | ------------------------------------------------------------ |
| Web/H5   | 纯前端                                                  |                                                              |
| PC客户端 | nw.js 和 electron                                       | 尤其是atom和vscode编辑器最为著名，像钉钉PC端，微信客户端、微信小程序IDE等都是这样的，通过web技术来打包成PC客户端 |
| 移动端   | cordova（旧称 PhoneGap），基于 cordova的 ionicframework | 这种采用h5开发，打包成ipa或apk的应用，称为Hybrid开发 （混搭），通过webview实现所谓的跨平台，应用的还是非常广泛的 |

**其他：**

| 用途           | 说明                                                         | 前景 |
| -------------- | ------------------------------------------------------------ | ---- |
| 爬虫           | 抢了不少Python的份额，整体来说简单，实⽤                     | 看涨 |
| 命令行工具     | 写⼯具、提⾼效率，node+npm                                   | 看涨 |
| 微服务与RPC    | Node做纯后端不好做，但在新项⽬和微服务架构下，必有⼀席之地   | 看涨 |
| 微信公众号开发 | 已经⽕了2年多了，尤其是付费阅读领域，还会继续⽕下去，gitchat就是使⽤ Node.js做的 | 看涨 |
| 反向代理       | Node.js可以作为nginx这样的反向代理，⽐如node-http-proxy和anyproxy等， 其实使⽤Node.js做这种请求转发是⾮常简单的 | 看涨 |

