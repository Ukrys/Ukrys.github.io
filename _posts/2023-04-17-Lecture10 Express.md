---
layout:     post
title:      Web前端-Lec10 Express
subtitle:   Web前端笔记
date:       2023-04-17
author:     ukrys
header-img: img/post-bg-js-version.jpg
catalog: 	 true
tags:
    - Web
    - Notes
    - express
---

## Lecture10 Express

### 10.1 Express简介

- Express是最流行的node web框架，它是许多其他流行的节点web框架的底层库。它提供了机制：
  - 在不同的URL路径（路由）中使用不同HTTP动词的请求编写处理程序。
  - 与“视图”呈现引擎集成，以便通过将数据插入模板来生成响应。
  - 设置常见的web应用程序设置，比如用于连接的端口，以及用于呈现响应的模板的位置。
  - 在请求处理管道的任何位置添加额外的请求处理“中间件”。
- 虽然Express本身是非常简单的，但是开发人员已经创建了兼容的中间件包来解决几乎所有的web开发问题
  - cookie、会话、用户登录、URL参数、POST数据、安全标头等等。
- 特点：精简、灵活、web程序框架、单页web程序、多页和混合的web程序

#### 10.1.1 Is Express opinionated?

- Web框架通常将自己称为“固执己见”或“不固执己见”。
- 固执的框架认为应该有⼀套“标准答案”来解决各类具体任务。 通常⽀持特定领域的快速开发（解决特定类型的问题）。因为 标准答案通常易于理解且文档丰富。然而在解决主领域之外的问题时，就会显得不那么灵活，可用的组件和方法也更少。
- Express是不固执己见的，是高度包容的。
  - 几乎可以将任何您喜欢的任何兼容的中间件插入到请求处理链中。
  - 可以在⼀个文件或多个文件中构造该应用程序，并使用任何目录结构。
  - 有太多的选择！

#### 10.1.2 Express 开发环境概述

- 完整的Express本地开发环境包括：Nodejs、NPM包管理器、Express 应用生成器（可选）

``` javascript
/* terminal */
// npm init
// npm install express --save
/* ---------------------------------------------- */

/* app.js */
var express = require('express');
var app = express();

app.get('/', function(req, res){
    res.send('Hello World!');
})

app.listen(3000, function(){
    console.log('Example app listening on port 3000!');
})
```

- 应用生成器工具

  通过应用生成器工具 express-generator 可以快速创建一个应用的骨架。

  ```
  npm install express-generator -g
  express helloworld
  cd helloworld
  npm install
  
  # Run the helloworld on Windows
  SET DEBUG=helloworld:* & npm start
  # Run helloworld on Linux/Mac OS X
  DEBUG=helloworld:* npm start
  ```

  [![pSKKbMF.png](https://s1.ax1x.com/2023/01/13/pSKKbMF.png)](https://imgse.com/i/pSKKbMF)

- 文件结构

  [![pSKKLqJ.png](https://s1.ax1x.com/2023/01/13/pSKKLqJ.png)](https://imgse.com/i/pSKKLqJ)

#### 10.1.3 处理数据流

下图展示了 HTTP请求/响应处理的主数据流和需要实现的行为

- 路由：把需要支持的请求（以及请求URL中包含的任何信息）转发到适当的控制器函数。

- 控制器：从模型中获取请求的数据，创建一个HTML页面显示出数据，并将页面返回给用户，以便在浏览器中查看。

- 视图（模块）：供控制器用来渲染数据。

  [![pSKMMQS.png](https://s1.ax1x.com/2023/01/13/pSKMMQS.png)](https://imgse.com/i/pSKMMQS)

### 10.2 路由 Route

#### 10.2.1 基本路由

- 路由用于确定应用程序如何响应对特定端点的客户机请求，包含一个URI（或路径）和一个特定的HTTP请求方法（GET、POST等）。

-	每个路由可以具有一个或多个处理程序函数，这些函数在路由匹配时执行。

- 路由定义采用以下结构：

  - app.METHOD(PATH, HANDLER)
  - 其中：app是express的实例；METHOD是HTTP请求方法；PATH是服务器上的路径；HANDLER是在路由匹配时执行的函数

  ```javascript
  /* 路由示例 */
  
  // 在主页上的 Hello World!进行响应：
  app.get('/', function(req, res){
      res.send('Hello World!');
  });
  
  // 在根路由(/)上(应用程序的主页)对POST请求进行响应：
  app.post('/', function(req, res){
      res.send('Got a POST request');
  });
  
  // 对 /user 路由的PUT请求进行响应：
  app.put('/user', function(req, res){
      res.send('Got a PUT request at /user');
  });
  ```

#### 10.2.2 路由方法

- 路由方法派生自 HTTP 方法之一，附加到 express 类的实例。

  ``` javascript
  // GET method route
  app.get('/', function(req, res){
      res.send('GET request to the homepage');
  })
  
  // POST method route
  app.post('/', function(req, res){
      res.send('POST request to the homepage');
  })
  ```

- 特殊路由方法：`app.all()`。它并非派生自HTTP方法。该方法用于在所有请求方法的路径中装入中间件函数。

  在以下示例中，无论使用 GET、POST、PUT、DELETE 还是在 http 模块中支持的其他任何 HTTP 请求方法，都将为针对“/ secret”的请求执行处理程序。

  ```javascript
  app.all('/secret', function(req, res, next){
      console.log('Accessing the secret section ...');
      next();	// pass control to the next handler
  })
  ```

#### 10.2.3 路由路径

- 路由路径与请求方法相结合，用于定义可以在其中提出请求的端点。路由路径可以是字符串、字符串模式或正则表达式。

- 路由路径用于定义可请求的端点。之前示例中路径都是字符串，并且必须精确写为：'/ ' 、'/ about'、'/ book'，等等。

- 路由路径也可以是字符串模式（String Pattern）。可用部分正则表达式语法来定义端点的模式。以下是所涉及的正则表达式（注意，连字符 ( -）和点（.）在字符串路径中解释为字面量，不能做为正则表达式）：

  - `?`：问号之前的⼀个字符只能出现零次或⼀次。例如，路由路径 '/ab?cd' 路径匹配端点 acd 或 abcd
  - `+`：加号之前的⼀个字符⾄少出现⼀次。例如，路径路径 '/ab+cd' 匹配端点abcd、abbcd、abbbcd等
  - `*`：星号可以替换为任意字符串。例如，路由路径 '/ab*cd' 匹配端点 abcd、abXcd、abSOMErandomTEXTcd 等
  - `()`：：将⼀个字符串视为⼀体以执行 ?、+、 * 操作。例如，'/ab(cd)?e' 将对 (cd) 进行匹配，将匹配 到 abe 和 abcde

- 路由路径也可以是 JavaScript 正则表达式。例如，下面的路由路径将匹配 catfish 和 dogfish，但不会匹配 catflap、catfishhead 等。注意，正则表达式路径不再用引号 "..." 括起来，而是正则表达式语法 /…/

  ```javascript
  app.get('/.*fish$/', (req, res) =>{
      ...
  });
  ```

- Express 使用 path-to-regexp 来匹配路由路径

  ```javascript
  // 此路由路径将请求与根路由 / 匹配。
  app.get('/', function (req, res) {
   	res.send('root');
  });
  // 此路由路径将请求与 /about 匹配。
  app.get('/about', function (req, res) {
   	res.send('about');
  });
  // 此路由路径将请求与 /random.text 匹配。
  app.get('/random.text', function (req, res) {
   	res.send('random.text');
  });
  // 基于字符串模式的路由路径的示例。此路由路径将匹配 acd 和 abcd。
  app.get('/ab?cd', function(req, res) {
   	res.send('ab?cd');
  });
  ```

#### 10.2.4 路由参数

- 路径参数是命名的 URL 段，用于捕获在 URL 中的位置指定的值。命名段以冒号为前缀，然后是名称（例如 /:your_parameter_name/。捕获的值保存在 req.params 对象中，键即参数名（例 如 req.params.your_parameter_name）。
- 路由参数名必须由”单词字符“（`/[A-Za-z0-9_]/`）组成

- 举例说，一个包含用户和藏书信息的URL：http://localhost:3000/users/34/books/8989，可以这样提取信息（使用userId和bookId路径参数）：

  ```javascript
  app.get('/users/:userId/books/:bookId', (req, res) => {
   // 通过 req.params.userId 访问 userId
   // 通过 req.params.bookId 访问 bookId
   res.send(req.params);
  });
  ```

#### 10.2.5 路由处理程序

- 可以提供多个回调函数，以类似于中间件的行为方式来处理请求。唯一例外是这些回调函数可能调用 next('route')来绕过剩余的路由回调。可以使用此机制对路由施加先决条件，在没有理由继续执行当前路由的情况下，可将控制权传递给后续路由。

- 路由处理程序的形式可以是一个函数、一组函数或者两者的结合，如以下示例中所示。

- 单个回调函数可以处理一个路由。例如：

  ```javascript
  // 单个回调函数可以处理⼀个路由。例如：
  app.get('/example/a', function (req, res) {
  	res.send('Hello from A!');
  });
  // 多个回调函数可以处理⼀个路由（确保您指定 next 对象）。例如：
  app.get('/example/b', function (req, res, next) {
  	console.log('the response will be sent by the next function ...');
  	next();
  }, function (req, res) {
   	res.send('Hello from B!');
  });
  ```

  ```javascript
  // ⼀组回调函数可以处理⼀个路由。例如：
  var cb0 = function (req, res, next) {
      console.log('CB0');
      next();
  }
  var cb1 = function (req, res, next) {
      console.log('CB1');
      next();
  }
  var cb2 = function (req, res) {
   	res.send('Hello from C!');
  }
  app.get('/example/c', [cb0, cb1, cb2]);
  ```

  ```javascript
  // 独⽴函数与⼀组函数的组合可以处理⼀个路由。例如：
  var cb0 = function (req, res, next) {
      console.log('CB0');
      next();
  }
  var cb1 = function (req, res, next) {
      console.log('CB1');
      next();
  }
  app.get('/example/d', [cb0, cb1], function (req, res, next) {
  	console.log('the response will be sent by the next function ...');
  	next();
  }, function (req, res) {
   	res.send('Hello from D!');
  });
  ```

#### 10.2.6 响应方法

- 下表中响应对象 (res) 的方法可以向客户机发送响应，并终止请求/响应循环。如果没有从路由处理程序调用其中任何方法，客户机请求将保持挂起状态。

  | 方法             | 描述                                             |
  | ---------------- | ------------------------------------------------ |
  | res.download()   | 提示将要下载文件。                               |
  | res.end()        | 结束响应进程。                                   |
  | res.json()       | 发送JSON响应。                                   |
  | res.jsonp()      | 在JSONP的支持下发送JSON响应。                    |
  | res.redirect()   | 重定向请求。                                     |
  | res.render()     | 呈现视图模块。                                   |
  | res.send()       | 发送各种类型的响应。                             |
  | res.sendFile()   | 以八位元流形式发送文件。                         |
  | res.sendStatus() | 设置响应状态码并以响应主体形式发送其字符串表示。 |

#### 10.2.7 app.route()

- 可以使用app.route() 为路由路径创建链式路由处理程序。因为在单一位置指定路径，所以可以减少冗余和输入错误。有关路由的更多信息，请参阅Router()文档。

- 以下是使用app.route()定义的链式路由处理程序的示例。

  ```javascript
  app.route('/book')
  	.get(function(req, res){
      	res.send('Get a random book');
  })
  	.post(function(req, res){
      	res.send('Add a book');
  })
  	.put(function(req, res){
      	res.send('Update the book');
  })
  ```

#### 10.2.8 express.Router

- 使⽤ express.Router 类来创建可安装的模块化路由处理程序。

- Router 实例是完整的中间件和路由系统；因此，常常将其称为“微型应用程序” 。

- 以下示例将路由器创建为模块，在其中装入中间件，定义⼀些路由，然后安装在主应⽤程序的路径中。

  ```javascript
  /* 在应⽤程序⽬录中创建名为 birds.js 的路由器⽂件，其中包含以下内容： */
  var express = require('express');
  var router = express.Router();
  // middleware that is specific to this router
  router.use(function timeLog(req, res, next) {
   	console.log('Time: ', Date.now());
   	next();
  });
  // define the home page route
  router.get('/', function(req, res) {
   	res.send('Birds home page');
  });
  // define the about route
  router.get('/about', function(req, res) {
   	res.send('About birds');
  });
  module.exports = router;
  ```

  ```javascript
  /* 接着，在应⽤程序中装⼊路由器模块： */
  var birds = require('./birds');
  ...
  app.use('/birds', birds);
  ```

### 10.3 编写中间件

- Connect 创造了”中间件“（middleware）这个术语来描述插入式的Node模块

- 从概念上讲，中间件是一种功能的封装方式，具体来说就是封装在程序中处理HTTP请求的功能。

- 中间件是在管道中执行的。

  - 在Express程序中，通过调用app.use向管道中插入中间件。

  [![pSK0sTx.png](https://s1.ax1x.com/2023/01/13/pSK0sTx.png)](https://imgse.com/i/pSK0sTx)

#### 10.3.1 Express 工作重点

- 路由处理器(app.get、app.post 等，经常被统称为app.VERB)可以被看作只处理特定 HTTP动词(GET、POST等)的中间件。同样，也可以将中间件看作可以处理全部 HTTP动词的路由处理器(基本上等同于app.all，可以处理任何HTTP动词;对于 PURGE之类特别的动词会有细微的差别，但对于普通的动词而言，效果是⼀样的)。

- 路由处理器的第⼀个参数必须是路径。如果你想让某个路由匹配所有路径，只需⽤/ * 。 中间件也可以将路径作为第⼀个参数，但它是可选的(如果忽略这个参数，它会匹配所有路径，就像指定了/\*⼀样)。

- 路由处理器和中间件的参数中都有回调函数，这个函数有2个、3个或4个参数(从技术上讲也可以有0或1个参数，但这些形式没有意义)。

  - 如果有2个或3个参数，头两个参数是请求和响应对象，第三个参数是 next 函数。
  - 如果有4个参数，它就变成了错误处理中间件，第⼀个参数变成了错误对象，然后依次是请求、响应和 next 对象。

- 如果不调⽤ next()，管道就会被终止，也不会再有处理器或中间件做后续处理。如果不调用 next()，则应该发送⼀个响应到客户端(res.send、res.json、res.render 等); 如果你不这样做，客户端会被挂起并最终导致超时。

- 如果调⽤了 next()，⼀般不宜再发送响应到客户端。如果你发送了，管道中后续的中间件或路由处理器还会执行，但它们发送的任何响应都会被忽略。

  ```javascript
  var express = require('express');
  var app = express();
  
  app.get('/', function (req, res) {
   	res.send('Hello World!');
  });
  
  app.listen(3000);
  ```

#### 10.3.2 中间件函数的简单示例

- 此函数仅在应用程序的请求通过它时显示“LOGGED”。中间件函数会分配给名为 myLogger 的变量。

- 请注意以上对 next() 的调用。

  - 调用此函数时，将调用应用程序中的下⼀个中间件函数。
  - next() 函数不是 Node.js 或 Express API 的⼀部分，而是传递给中间件函数的第三自变量。
  - next() 函数可以命名为任何名称，但是按约定，始终命名为“next”。
  - 为了避免混淆，请始终使用此约定。

  ```javascript
  var myLogger = function (req, res, next) {
  	console.log('LOGGED');
  	next();
  };
  ```

- 要装入中间件函数，请调用 app.use() 并指定中间件函数。例如，以下代码在根路径（/）的路由之前装入 mmyLogger 中间件函数。

  ```javascript
  var express = require('express');
  var app = express();
  var myLogger = function (req, res, next) {
  	console.log('LOGGED');
   	next();
  };
  app.use(myLogger);
  app.get('/', function (req, res) {
   	res.send('Hello World!');
  });
  app.listen(3000);
  ```

- 中间件装入顺序很重要！首先装入的中间件函数也首先被执行。

- 如果在根路径的路由之后装入 myLogger，那么请求永远都不会到达该函数，应用程序也不会显示“LOGGED”，因为根路径的路由处理程序终止了请求/响应循环。

- 中间件函数 myLogger 只是显示消息，然后通过调⽤ next() 函数将请求传递到堆栈中的下⼀个中间件函数。

  ```javascript
  /* 示例：名为 requestTime 的属性添加到请求对象 */
  var requestTime = function (req, res, next) {
  	req.requestTime = Date.now();
  	next();
  };
  ```

- 现在，该应⽤程序使⽤ requestTime 中间件函数。此外，根路径路由的回调函数使⽤由中间件函数添加到 req（请求对象）的属性。

  ```javascript
  var express = require('express');
  var app = express();
  var requestTime = function (req, res, next) {
  	req.requestTime = Date.now();
  	next();
  };
  app.use(requestTime);
  app.get('/', function (req, res) {
  	var responseText = 'Hello World!';
  	responseText += 'Requested at: ' + req.requestTime + '';
  	res.send(responseText);
  });
  app.listen(3000);
  ```

#### 10.3.3 使用中间件

- Express 是⼀个路由和中间件 Web 框架，其自身只具有最低程度的功能：
  - Express 应用程序基本上是⼀系列中间件函数调用。
- 中间件函数能够访问请求对象 (req)、响应对象 (res) 以及应⽤程序的请求/响应循环中的下⼀个中间件函数。下⼀个中间件函数通常由名为 next 的变量来表示。
- 中间件函数可以执行以下任务：
  - 执行任何代码。 
  - 对请求和响应对象进行更改。
  - 结束请求/响应循环。
  - 调用堆栈中的下⼀个中间件函数。
- 如果当前中间件函数没有结束请求/响应循环，那么它必须调用 next()，以将控制权传递给下⼀个中间件函数。否则，请求将保持挂起状态。
- Express 应用程序可以使用以下类型的中间件：
  - 应用层中间件
  - 路由器层中间件
  - 错误处理中间件
  - 内置中间件
  - 第三方中间件
- 可以使用可选安装路径来装⼊应用层和路由器层中间件。 还可以将⼀系列中间件函数⼀起装⼊，这样会在安装点创建中间件系统的子堆栈。

#### 10.3.4 应用层中间件

- 使⽤ app.use() 和 app.METHOD() 函数将应用层中间件绑定到应用程序对象的实例，其中 METHOD 是中间件函数处理的请求的小写 HTTP ⽅法（例如 GET、PUT 或 POST）。

  ```javascript
  /* 此示例显示没有安装路径的中间件函数。应⽤程序每次收到请求时执⾏该函数。 */
  var app = express();
  app.use(function (req, res, next) {
   	console.log('Time:', Date.now());
   	next();
  });
  
  /* 此示例显示安装在 /user/:id 路径中的中间件函数。在 /user/:id 路径中为任何类型的 HTTP 请求执⾏此函数。 */
  app.use('/user/:id', function (req, res, next) {
   	console.log('Request Type:', req.method);
   	next();
  });
  
  /* 此示例显示⼀个路由及其处理程序函数（中间件系统）。此函数处理针对 /user/:id 路径的 GET 请求。 */
  app.get('/user/:id', function (req, res, next) {
  	res.send('USER');
  });
  
  /* 在安装点使⽤安装路径装⼊⼀系列中间件函数的示例。 演示⼀个中间件子堆栈，用于显示针对 /user/:id 路径的任何类型 HTTP 请求的信息。 */
  app.use('/user/:id', function(req, res, next) {
  	console.log('Request URL:', req.originalUrl);
  	next();
  }, function (req, res, next) {
  	console.log('Request Type:', req.method);
  	next();
  });
  ```

- 路由处理程序可以为⼀个路径定义多个路由。以下示例为针对 / user/:id 路径的 GET 请求定义两个路由。第⼆个路由不会导致任何问题，但是永远都不会被调⽤，因为第⼀个路由结束了请求/响应循环。

  ```javascript
  /* 此示例显示⼀个中间件⼦堆栈，⽤于处理针对 /user/:id 路径的 GET请求。 */
  app.get('/user/:id', function (req, res, next) {
   	console.log('ID:', req.params.id);
   	next();
  }, function (req, res, next) {
   	res.send('User Info');
  });
  // handler for the /user/:id path, which prints the user ID
  app.get('/user/:id', function (req, res, next) {
  	res.end(req.params.id);
  });
  ```

- 要跳过路由器中间件堆栈中剩余的中间件函数，请调⽤ next('route') 将控制权传递给下⼀个路由。

- next('route') 仅在使⽤ app.METHOD() 或 router.METHOD() 函数装⼊的 中间件函数中有效。

  ```javascript
  /* 此示例显示⼀个中间件⼦堆栈，⽤于处理针对 /user/:id 路径的 GET 请求。 */
  app.get('/user/:id', function (req, res, next) {
  	// if the user ID is 0, skip to the next route
   	if (req.params.id == 0) next('route');
   	// otherwise pass the control to the next middleware function in this stack
   	else next(); //
  }, function (req, res, next) {
  	// render a regular page
  	res.render('regular');
  });
  // handler for the /user/:id path, which renders a special page
  app.get('/user/:id', function (req, res, next) {
  	res.render('special');
  });
  ```

#### 10.3.5 路由器层中间件

- 路由器层中间件的工作方式与应用层中间件基本相同，差异之处在于它绑定到 express.Router()的实例。

  ```javascript
  var router = express.Router();
  ```

- 使用 router.use() 和 router.METHOD() 函数装入路由器层中间件。

  ```javascript
  var app = express();
  var router = express.Router();
  // a middleware function with no mount path. This code is executed for every request to the router
  router.use(function (req, res, next) {
   	console.log('Time:', Date.now());
   	next();
  });
  // a middleware sub-stack shows request info for any type of HTTP request to the /user/:id path
  router.use('/user/:id', function(req, res, next) {
   	console.log('Request URL:', req.originalUrl);
   	next();
  }, function (req, res, next) {
   	console.log('Request Type:', req.method);
   	next();
  });
  // a middleware sub-stack that handles GET requests to the /user/:id path
  router.get('/user/:id', function (req, res, next) {
   	// if the user ID is 0, skip to the next router
   	if (req.params.id == 0) next('route');
   	// otherwise pass control to the next middleware function in this stack
   	else next(); //
  }, function (req, res, next) {
   	// render a regular page
   	res.render('regular');
  });
  // handler for the /user/:id path, which renders a special page
  router.get('/user/:id', function (req, res, next) {
   	console.log(req.params.id);
   	res.render('special');
  });
  // mount the router on the app
  app.use('/', router);
  ```

#### 10.3.6 错误处理中间件

- 错误处理中间件始终采用四个自变量。必须提供四个自变量， 以将函数标识为错误处理中间件函数。即使无需使用 next 对象，也必须指定该对象以保持特征符的有效性。否则，next 对象将被解释为常规中间件，从而无法处理错误。

- 错误处理中间件函数的定义方式与其他中间件函数基本相同， 差别在于错误处理函数有四个自变量而不是三个，专门具有特征符 (err, req, res, next)：

  ```javascript
  app.use(function(err, req, res, next) {
  	console.error(err.stack);
  	res.status(500).send('Something broke!');
  });
  ```

#### 10.3.7 内置中间件

- ⾃ V4.x 起，Express 不再依赖于 Connect。除 express.static 外，先前 Express 随附的所有中间件函数现在以单独模块的形式提供。请查看中间件函数的列表。

- express.static(root, [options])

  - Express 中唯⼀内置的中间件函数是 express.static。此函数基于 serve-static，负责提供 Express 应用程序的静态资源。

  - root 自变量指定从其中提供静态资源的根目录。

  - 可选的 options 对象可以具有以下属性：

    | 属性         | 描述                                                         | 类型   | 缺省值       |
    | ------------ | ------------------------------------------------------------ | ------ | ------------ |
    | dotfiles     | 是否对外输出文件名以点(.)开头的文件。有效值包括"allow"、"deny"、"ignore" | 字符串 | "ignore"     |
    | etag         | 启动或禁用 etag 生成                                         | 布尔   | true         |
    | extensions   | 用于设置后备文件扩展名                                       | 数组   | []           |
    | index        | 发送目录索引文件。设置为 false 可禁用建立目录索引。          | 混合   | "index.html" |
    | lastModified | 将 Last-Modified 的头设置为操作系统上该文件的上次修改日期。有效值包括 true 或 false | 布尔   | true         |
    | maxAge       | 设置 Cache-Control 头的 max-age 属性（以毫秒或者 ms 格式中的字符串为单位） | 数字   | 0            |
    | redirect     | 当路径名是目录时重定向到结尾的”/“                            | 布尔   | true         |
    | setHeaders   | 用于设置随文件一起提供的 HTTP 头的函数                       | 函数   |              |

- 以下示例将使⽤了 express.static 中间件，并且提供了⼀个详 细的’options’对象（作为示例）：

  ```javascript
  var options = {
       dotfiles: 'ignore',
       etag: false,
       extensions: ['htm', 'html'],
       index: false,
       maxAge: '1d',
       redirect: false,
       setHeaders: function (res, path, stat) {
       	res.set('x-timestamp', Date.now());
  	 }
  }
  app.use(express.static('public', options));
  ```

- 对于每个应用程序，可以有多个静态目录：

  ```javascript
  app.use(express.static('public'));
  app.use(express.static('uploads'));
  app.use(express.static('files'));
  ```

#### 10.3.8 第三方中间件

- 使⽤第三方中间件向 Express 应用程序添加功能。

- 安装具有所需功能的 Node.js 模块，然后在应用层或路由器层的应用程序中将其加装入。

- 以下示例演示如何安装和装⼊ cookie 解析中间件函数 cookieparser。

  ```
  $ npm install cookie-parser
  ```

  ```javascript
  var express = require('express');
  var app = express();
  var cookieParser = require('cookie-parser');
  // load the cookie-parsing middleware
  app.use(cookieParser());
  ```

### 10.4 模板引擎

#### 10.4.1 将模板引擎用于 Express

- Express 应⽤⽣成器⽀持多款流⾏的视图/模板引擎，包括 EJS、Hbs、Pug (Jade)、Twig 和 Vash，缺省选项是 Jade。Express 本身也⽀持⼤量其他模板语言，开箱即用

- 在 Express 可以呈现模板文件之前，必须设置以下应用程序设置：

  - views：模板文件所在目录。例如：app.set('views', './views')
  - view engine：要使用的模板引擎。例如：app.set('view engine', 'pug')

- 然后安装对应的模板引擎 npm 包：

  - ```
    $ npm install pug --save
    ```

  ```javascript
  /* 在设置视图引擎之后，不必指定该引擎或者在应⽤程序中装⼊模板引擎模块；Express
  在内部装⼊此模块，如下所示（针对以上示例）。 */
  app.set('view engine', 'pug');
  
  /* 在 views ⽬录中创建名为 index.pug 的 Pug 模板⽂件，其中包含以下内容： */
  /*  html
   *	  head
   *		title= title
   *	  body
   *		h1= message
   */
  
  /* 随后创建路由以呈现 index.pug ⽂件。如果未设置 view engine 属性，必须指定 view ⽂
  件的扩展名。否则，可以将其忽略。*/
  app.get('/', function (req, res) {
  	res.render('index', { title: 'Hey', message: 'Hello there!'});
  });
  
  /* 向主⻚发出请求时，index.pug ⽂件将呈现为 HTML。 */
  ```

#### 10.4.2 选用模板引擎需要考虑的因素

[![pSKb7Eq.png](https://s1.ax1x.com/2023/01/13/pSKb7Eq.png)](https://imgse.com/i/pSKb7Eq)

#### 10.4.3 为 Express开发模板引擎

- 可以使用 app.engine(ext, callback) 方法创建自己的模板引擎。

  - ext 表示文件扩展名
  - callback表示模板引擎函数，它接受以下项作为参数：文件位置、选项对象和回调函数。

  ```javascript
  /* 以下代码示例实现⾮常简单的模板引擎以呈现 .ntl ⽂件。 */
  var fs = require('fs'); // this engine requires the fs module
  app.engine('ntl', function (filePath, options, callback) { 
      // define the template engine
      fs.readFile(filePath, function (err, content) {
          if (err) return callback(new Error(err));
          // this is an extremely simple template engine
          var rendered = content.toString().replace('#title#', ''+ options.title +'')
          .replace('#message#', ''+ options.message +'');
          return callback(null, rendered);
      });
  });
  app.set('views', './views'); // specify the views directory
  app.set('view engine', 'ntl'); // register the template engine
  
  /* 应⽤程序现在能够呈现 .ntl ⽂件。在 views ⽬录中创建名为 index.ntl 且包含以下内
  容的文件： 
  	#title#
  	#message#
  */
  /* 然后，在应用程序中创建以下路径： */
  app.get('/', function (req, res) {
  	res.render('index', { title: 'Hey', message: 'Hello there!'});
  });
  /* 您向主⻚发出请求时，index.ntl 将呈现为 HTML。 */
  ```

#### 10.4.4 调试 Express

- Express 在内部使⽤调试模块来记录关于路由匹配、使⽤的中间件函数、应⽤程序模式以及请求/响应循环流程的信息。

- debug 就像是扩充版的 console.log，但是与 console.log 不同，不必注释掉⽣产代码中的 debug 日志。缺省情况下，日志记录功能已关闭，可以使⽤ DEBUG 环境变量有条件地开启日志记录。

- 要查看 Express 中使用的所有内部日志，在启动应用程序时，请将 DEBUG 环境变量设置为 express:*。

  - $ DEBUG=express:* node index.js

- 在 Windows 上，使⽤对应的命令。

  - \> set DEBUG=express:* & node index.js

  [![pSKq9V1.png](https://s1.ax1x.com/2023/01/13/pSKq9V1.png)](https://imgse.com/i/pSKq9V1)

​	