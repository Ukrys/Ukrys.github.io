---
layout:     post
title:      Web前端-Lec11 AJAX
subtitle:   Web前端笔记
date:       2023-04-17
author:     ukrys
header-img: img/post-bg-js-version.jpg
catalog: 	 true
tags:
    - Web
    - Notes
    - ajax
---

## Lecture11 Asynchronous JavaScript and XML (AJAX)

### 11.1 RIA

#### 11.1.1 从网站到web应用

- Client / Server

- 三层架构 Three-Tier

  - 将业务应用规划中的表示层 UI、数据访问层 DAL 以及业务逻辑层 BLL，其分层的核心任务是”高内聚低耦合“的实现。
  - Model-View-Controller
  - 富互联网应用 Rich Internet

  <table>
      <tr>
      	<td rowspan="2"><a href="https://imgse.com/i/pSMFIrq"><img src="https://s1.ax1x.com/2023/01/14/pSMFIrq.png" alt="pSMFIrq.png" border="0" /></a></td>
          <td><a href="https://imgse.com/i/pSMF7ZV"><img src="https://s1.ax1x.com/2023/01/14/pSMF7ZV.png" alt="pSMF7ZV.png" border="0" /></a></td>
      </tr>
      <tr>
          <td><a href="https://imgse.com/i/pSMFHaT"><img src="https://s1.ax1x.com/2023/01/14/pSMFHaT.png" alt="pSMFHaT.png" border="0" /></a></td>
      </tr>
  </table>

#### 11.1.2 传统的web应用

- 瘦客户端架构
  - 服务器完成大部分工作并保存大部分数据 → 更高的流量
- 同步通信
  - 对于作为某些操作的结果发送的每个请求，客户机在服务器完成响应之前不能与应用程序交互。
  - 也就是说，缺少交互性的用户体验

#### 11.1.3 Rich Internet Applications

- MVC的RIA实现

[![pSMFjz9.png](https://s1.ax1x.com/2023/01/14/pSMFjz9.png)](https://imgse.com/i/pSMFjz9)

- RIA：优势
  - 不需要安装；易于升级；可以通过互联网/内部网轻松获取；丰富的用户界面；更好的响应性；客户机/服务器平衡；异步通信；网络效率
- RIA：不足
  - 搜索引擎不够友好；专有的（相对于开放标准）；完整性丧失(RIA通常不能很好地与HTML混合)；软件开发的复杂性(在客户端计算机上缓存或不缓存什 么?)；RIA体系结构打破了Web页面范式
- RIA的实现方式
  - 浏览器插件
    - Flash/Flex, Java Swing, Silverlight
    - 潜在的更强的交互性，更⾼的应用障碍
    - 关注开放/控制
  - 在浏览器中，不需要插件
    - AJAX
    - 更低的采用门槛
    - 跨浏览器问题？

### 11.2 Ajax

#### 11.2.1 web通信模型

| web同步通信模型                                              | web异步通信模型                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [![pSMFzs1.png](https://s1.ax1x.com/2023/01/14/pSMFzs1.png)](https://imgse.com/i/pSMFzs1) | [![pSMkSqx.png](https://s1.ax1x.com/2023/01/14/pSMkSqx.png)](https://imgse.com/i/pSMkSqx) |
| 同步：用户必须等待新页面加载<br>    网页中使用的典型通信模式(点击-等待-刷新)<br>几乎所有对新数据的更改都会导致页面刷新 | 异步：用户可以在数据加载时继续与页面交互<br>    Ajax使通信模式成为可能<br>使用新数据进行更改，但不刷新页面 |

#### 11.2.2 Ajax 简介

- AJAX（Asynchronous JavaScript And XML ）是⼀种使用 XMLHttpRequest 技术构建更复杂，动态的网页的编程实践。

- Asynchronous JavaScript + XML（异步 JavaScript 和 XML）, 其本身不是⼀种新技术， 而是⼀个在 2005 年被 Jesse James Garrett 提出的新术语，用来描述⼀种使⽤现有技术集合的‘新’方法，包括：HTML 或 XHTML, CSS, JavaScript, DOM, XML (en-US), XSLT, 以及最重要的 XMLHttpRequest。

- AJAX 允许只更新⼀个 HTML 页面的部分 DOM，而无须重新加载整个页面。AJAX 还允许异步工作，这意味着当网页的⼀部分正试图重新加载时，您的代码可以继续运行（相比之下，同步会阻止代码继续运行，直到这部分的网页完成重新加载）。

- 尽管 X 在 Ajax 中代表 XML，但由于JSON的许多优势，比如更加轻量以及作为 Javascript 的⼀部分，⽬前 JSON 的使用比 XML 更加普遍。JSON 和 XML 都被用于在 Ajax 模型中打包信息。

- 通过交互式网站和现代 Web 标准，AJAX 正在逐渐被 JavaScript 框架中的函数和官方的 Fetch API 标准取代。

  | [![pSMy9ne.png](https://s1.ax1x.com/2023/01/14/pSMy9ne.png)](https://imgse.com/i/pSMy9ne) | [![pSMymjS.png](https://s1.ax1x.com/2023/01/14/pSMymjS.png)](https://imgse.com/i/pSMymjS) |
  | :----------------------------------------------------------: | ------------------------------------------------------------ |

#### 11.2.3 AJAX优缺点

<table>
    <tr><td>优点</td>	<td>缺点</td></tr>
    <tr>
    	<td>
        	<ul>
                <li>更好的交互性和响应性。</li>
                <li>页面将更于使用。</li>
                <li>由于部分呈现，减少了到Web服务器的连接。</li>
                <li>因为只加载更新页面所需的数据，而不是刷新整个页面，因此节省了带宽</li>
                <li>有助于减少网络流量。</li>
            </ul>
        </td>
        <td>
        	<ul>
                <li>后退和刷新按钮变得不可用。</li>
                <li>收藏网页将变得不可用。</li>
                <li>要求在web浏览器上启用JavaScript。</li>
                <li>网络延迟可能会破坏可用性。</li>
                <li>通过AJAX加载的数据不会被任何主要搜索引擎索引。因此，使其SEO不友好。</li>
            </ul>
        </td>
    </tr>
</table>

#### 11.2.4 使用AJAX的真实场景

- 自动完成搜索文本框
- 级联下拉列表框
- 实时通信，如即时消息传递
- 实时数据更新，如分数更新
- 即时表单验证反馈
- 自动保存用户信息

### 11.3 XMLHttpRequest

#### 11.3.1 AJAX组件

- AJAX 不能独立工作。
- 与其他技术结合使用，以创建以下列表中描述的交互式Web页面：
  - Javascript：
    - 松散类型的脚本语言
    - 当页面中发生事件时调用 JavaScript 函数
    - 整个AJAX操作的胶水
  - DOM：
    - 用于访问和操作结构化文档的API
    - 表示XML和HTML文档的结构
  - CSS：
    - 允许将表示样式与内容清晰分离，并且可以通过Javascript以编程方式更改
  - XMLHttpRequest：
    - Javascript 对象，它执行与服务器的异步交互

#### 11.3.2 XMLHttpRequest 对象

- XMLHTTPRequest对象：
  - 是AJAX最重要的组件
  - 自2000年7月Internet Explorer 5.5发布以来⼀直可用。
  - 是⼀个API，可以被JavaScript、JScript、VBScript和其他Web浏览 器脚本语言使用。
  - 用于使用HTTP在Web服务器之间传输和操作XML数据。
  - 在Web页面的客户端和服务器端之间建立独立的连接通道。
  - 除了XML, XMLHttpRequest还可以用于获取其他格式的数据，比如 JSON甚至纯文本。
  - 执行如下操作：
    - 在后台从客户端发送数据
    - 从服务器接收数据
    - 更新网页，无需重新加载

- AJAX Web应用程序模型的处理周期如下图所示：

  [![pSM6saj.png](https://s1.ax1x.com/2023/01/14/pSM6saj.png)](https://imgse.com/i/pSM6saj)

- XMLHttpRequest对象的常见属性：

  | 属性               | 描述                                                         |
  | ------------------ | ------------------------------------------------------------ |
  | onReadyStateChange | Is called whenever readyState attribute changes. It must not be used with synchronous requests. |
  | readyState         | Represents the state of the request. It ranges from 0 to 4, as described in the following list: <br />• 0: UNOPENED, open() is not called. <br />• 1: OPENED, open is called but send() is not called. <br />• 2: HEADERS_RECEIVED, send() is called, and headers and status are available. <br />• 3: LOADING, downloading data; responseText holds the data. <br>• 4: DONE, the operation is completed fully. |
  | responseText       | Returns response as text                                     |
  | responseXML        | Returns response as XML.                                     |

- XMLHttpRequest对象的基本方法：

  | 方法                                              | 描述                                                         |
  | ------------------------------------------------- | ------------------------------------------------------------ |
  | void open(method, URL)                            | Opens the request specifying get or post method and URL of the requested Web page. |
  | void open(method, URL, async)                     | same as above but specifies asynchronous or not.             |
  | void open(method, URL, async, username, password) | same as above but specifies username and password.           |
  | void send()                                       | sends get request.                                           |
  | void send(stirng)                                 | send post request.                                           |
  | setRequestHeader(header, value)                   | it adds request headers.                                     |

- 为了使用 JavaScript 向服务器发送⼀个 http 请求，需 要⼀个包含必要函数功能的XMLHttpRequest对象实例。

  ```javascript
  const httpRequest = new XMLHttpRequest();
  
  // Old compatibility code, no longer needed.
  if (window.XMLHttpRequest) { // Mozilla, Safari, IE7+ ...
   	httpRequest = new XMLHttpRequest();
  } else if (window.ActiveXObject) { // IE 6 and older
  	httpRequest = new ActiveXObject("Microsoft.XMLHTTP");
  }
  ```

- 创建XMLHttpRequest对象后，需要决定在收到服务器对请求的响应后要做什么。

  在这一步，需要定义JavaScript函数，该函数将处理服务器响应。

  这可以使用XMLHttpRequest对象的onreadystatechange属性来完成，如下所示的代码片段：

  ``` javascript
  httpRequest.onreadystatechange = function(){
  	//process the server response
  };
  ```

- 设置响应功能后，需要进行请求。

  为了发出请求，需要调用XMLHttpRequest对象的open()和send() 方法，如下所示:

  ``` javascript
  httpRequest.open(‘GET’,’serverpage.php’,true);
  httpRequest.send(null);
  ```

  下面的列表描述了前面代码片段中传递给open()方法的参数：

   <ul>
       <li>第⼀个参数是HTTP请求方法，例如GET、POST和HEAD。</li>
       <li>第⼆个参数是请求的Web页面的URL。</li>
       <li>第三个参数(可选)设置请求是否是异步的。</li>
   </ul>

- 处理服务器的响应：

  - 首先，响应函数需要检查请求的就绪状态。
    - 如果就绪状态的值为4，则可以进一步执行。
  - 接下来，需要检查HTTP服务器响应的响应代码。

  下面的代码片段描述了如何处理服务器的响应：

  ```javascript
  httpRequest.onreadystatechange = function(){
      if (httpRequest.readyState === 4) {
          // everything is good, the response is received
          if (httpRequest.status === 200) { 
              // process the response 
          }else { 
              // request encountered some problem,
              // for example, the response may contain a HTTP
              404 (Not Found) response code
          }
      } else { 
          // still not ready 
      } 
  };
  ```

- 使用 XMLHttpRequest获取数据

  下面的代码片段描述了如何在Web页面上显示来自Web服务器的响应：

  ```html
  <!-- AJAXExample.htm -->
  <button id="ajaxButton" type="button">Make a request</button>
  <script>
      (function() {
          var httpRequest;
          document.getElementById("ajaxButton").addEventListener('click', makeRequest);
          function makeRequest() {
              httpRequest = new XMLHttpRequest();
              if (!httpRequest) {
                  alert('Giving up :( Cannot create an XMLHTTP instance');
                  return false;
              }
              httpRequest.onreadystatechange = alertContents;
              httpRequest.open('GET', 'test.html');
              httpRequest.send();
          }
          function alertContents() {
              if (httpRequest.readyState === XMLHttpRequest.DONE) {
                  if (httpRequest.status === 200) {
                      alert(httpRequest.responseText);
                  } else {
                      alert('There was a problem with the request.');
                  }
              }
          }
      })();
  </script>
  ```

#### 11.3.3 跨站的 XMLHttpRequest

- 现代浏览器可以通过执行 WebApps 工作小组通过的 Access Control for Cross-Site Requests 标注来支持跨站请求。只要服务器端的配置允许您从您的 Web 应用发送请求，就可以使用 XMLHttpRequest 。 否则，会抛出⼀个 INVALID_ACCESS_ERR 异常

- 跨源资源共享（CORS，或通俗地译为跨域资源共享）是⼀种基于 HTTP 头的机制，该机制通过允许服务器标示除了它自己以外的其它源（域、协议和端口），使得浏览器允许这些 origin 访问加载自己的资源。跨源资源共享还通过⼀种机制来检查服务器是否会允许要发送的真实请求，该机制通过浏览器发起⼀个到服务器托管的跨源资源的“预检”请求。在预检中，浏览器发送的头中标示有 HTTP 方法和真实请求中会用到的头。

- 跨源 HTTP 请求的一个例子：运行在 `https://domain-a.com` 的 JavaScript 代码使用 XMLHttpRequest 来发起⼀个到 `https://domain-b.com/data.json` 的请求。

- 出于安全性，浏览器限制脚本内发起的跨源 HTTP 请求。例如， XMLHttpRequest 和 Fetch API 遵循同源策略。这意味着使用这些 API 的 Web 应用程序只能从加载应用程序的同⼀个域请求 HTTP 资源，除非响应报文包含了正确 CORS 响应头。

- CORS 机制允许 Web 应用服务器进行跨源访问控制，从而使跨源数据传输得以安全进行。现代浏览器支持在 API 容器中（例如 XMLHttpRequest 或 Fetch）使用 CORS， 以降低跨源 HTTP 请求所带来的风险。

  [![pSMgkN9.png](https://s1.ax1x.com/2023/01/14/pSMgkN9.png)](https://imgse.com/i/pSMgkN9#pic_center)

#### 11.3.4 Fetch

- Fetch 是⼀个现代的概念，等同于 XMLHttpRequest。它提供了许多与 XMLHttpRequest 相同的功能，但被设计成更具可扩展性和高效性。

  Fetch API 提供了⼀个 JavaScript 接⼝，⽤于访问和操纵 HTTP 管道的⼀些具体部分，例如请求和响应。它还提供了⼀个全局 fetch() 方法，该方法提供了⼀种简单，合理的方式来跨网络异步获取资源。

  这种功能以前是使用 XMLHttpRequest 实现的。Fetch 提供了⼀个更理想的替代方案，可以很容易地被其他技术使用，例如 Service Workers。Fetch 还提供了专门的逻辑空间来定义其他与 HTTP 相关的概念，例如 CORS 和 HTTP的扩展。

- 基本的fetch请求

  ```javascript
  fetch('http://example.com/movies.json')
   	.then(response => response.json())
   	.then(data => console.log(data));
  ```

### 11.4 Ajax的局限

#### 11.4.1 Ajax 风险

- 浏览器后退机制的破坏，后退和前进按钮问题
- 安全风险
- 搜索引擎
- 书签的问题

#### 11.4.2 并发连接数限制

- HTTP 1.1 (RFC 2616)建议单用户客户端不应该与任何服务器或代理保持超过2个连接。

- 大多数浏览器(包括IE)都遵守这个规则

  ![image-20230114152852576](C:\Users\94327\AppData\Roaming\Typora\typora-user-images\image-20230114152852576.png)

### 11.5 提示

#### 11.5.1 Ajax优化

优化任何Ajax应⽤程序的方法是找到优化其中的每个元素的最佳方法。应用程序尽可能快速高效地运行是很重要的。

**通信**

- 当从服务器接收新数据时没有巨大的延迟时，Ajax应用程序是快速的。优化两个方面将有助于应用程序成功。
  - 第⼀种是压缩从服务器发送到客户端的所有数据。这对于快速数据传输非常重要。
  - 第⼆个问题与数据本身有关。从客户机和服务器来回发送的数据也应该尽可能地优化。

**数据**

- 向服务器发送数据时，发送最小数量的信息。如果要发送键/值对，请保持键和值都小。尽可能列举选择。而 不是像这样:

  ```javascript
  user_choice = add_data_to_database&data1=value1&data2=value2
  ```

- 考虑将每个选项设置为单个值，并发送该值:

  ```javascript
  c=3&d1=value1&d2=value2
  ```

- 更小的数据使得被拦截的信息更难被解释(⼀个很好的 安全好处)，并保持需要发送和解析的数据的大小更小。

**代码优化**

- Ajax优化的另⼀个重要部分是优化在客户机上执行的JavaScript 代码，并创建尽可能快的数据检索。
  - 内联SQL查询
  - 存储过程
- 在客户机上，许多JavaScript技术将有助于增加代码的执行时间。当接收到Ajax响应时代码可能需要执行的DOM操作时，这⼀点尤其重要。
- 没有⼈说Ajax应用程序在没有任何优化的情况下不能平稳有效地运行。在大多数情况下，以太网连接的速度、计算机的处理能力以及浏览器中JavaScript的更好实现将确保应用程序运行良好。 优化将使应用程序运行得更快。对于用户来说，越快越好。

#### 11.5.2 使用库

- 库不仅提供了可以使用的详尽特性集，而且还确保代码与所有浏览器兼容，而无需做任何额外的工作。
  - axios
  - AngularJS
- 掌握一个库

- Ajax库的局限性
  - 所有JavaScript库都允许访问Ajax对象，该对象规范了浏览器之间的差异，并提供了⼀致的界面。然而，在提供统⼀的界面时，这些库也必须简化界面，因为不是每个浏览器都实现每个特性。这将阻止您访问 XMLHttpRequest的全部功能。
  - 直接与XHR对象交互还减少了函数开销，进⼀步提高了 性能。只是要注意，如果放弃使⽤Ajax库，可能会在使用更老、更晦涩的浏览器时遇到⼀些问题。

#### 11.5.3 利用适当的事件和回调函数

正确使用这些事件和它们各自的回调来操作UI，以获得更好的用户体验。

```javascript
$.ajax({
        //Other code
           success: function(msg)
        {
            // Update the UI here to reflect that the request was successful.
            doSomethingClever();
        },
        error: function(msg)
        {
            // Update the UI here to reflect that the request was unsuccessful
            doSomethingMoreClever();
        },
        complete: function(msg)
        {
            // Update the UI here to reflect completion
            doSomethingEvenMoreClever();
        }
});
```

#### 11.5.4 选择合适的格式

- 在考虑数据传输技术时，必须考虑以下几个因素:特性集、兼容性、性能和方向(到服务器或从服务器)。
- 在考虑数据格式时，惟⼀需要比较的尺度是速度。
- 没有⼀种数据格式总是比其他格式更好。根据正在传输的数据及其在页面上的预期用途，⼀个可能下载得更 快，而另⼀个可能解析得更快。

##### 11.5.4.1 数据格式比较

**XML**

（ XML在⾼性能Ajax中没有⼀席之地 ）

 <table>
    <tr><td>优点</td>	<td>缺点</td></tr>
    <tr>
    	<td>
        	<ul>
                <li>极⼤的互操作性(在服务器端和客户端都有出色的支持)</li>
                <li>严格的格式</li>
                <li>容易验证</li>
            </ul>
        </td>
        <td>
        	<ul>
                <li>⾮常详细。每⼀个离散的数据都需要大量的结构，而数据与结构的比率极低。</li>
                <li>XML的语法也有点模糊。</li>
                <li>解析这个语法同样是不明确的。</li>
            </ul>
        </td>
    </tr>
</table>

**JSON**

JSON（JavaScript Object Notation）由Douglas Crockford形式化并推广开来，是⼀种使用JavaScript 对象和数组文字语法编写的轻量级且易于解析的数据格式。基于 ECMAScript的⼀个子集。

```json
// Verbose JSON
[
	{ "id": 1, "username": "alice", "realname": "Alice Smith",
		"email": "alice@alicesmith.com" },…
]
// Simple JSON
[
	{ "i": 1, "u": "alice", "r": "Alice Smith", "e":
		"alice@alicesmith.com" }, ……
]
//Array JSON
[
    [ 1, "alice", "Alice Smith", "alice@alicesmith.com" ], ……
]
```

**JSON-P**

- Jsonp(JSON with Padding) 是 json 的⼀种"使用模式"，可以让网页从别的域名（网站）那获取资料，即跨域读取数据
  - 当使用动态脚本标记插入时，JSON数据被视为另⼀个JavaScript文件，并作为本机代码执行。为了实现这⼀点，必须将数据包装在回调函数中。
- 由于数据被视为原生JavaScript，因此它将以原生JavaScript速度进行解析。
- 有⼀个避免使用JSON-P的原因与性能无关:由于JSON-P必须是可 执⾏的JavaScript，任何⼈都可以调用它，并在任何使用动态脚本标签插⼊的网站中包含它。
- 不要在JSON-P中编码任何敏感数据，因为即使使用随机url或 cookie，也不能确保它保持私有。

**HTML**

- HTML作为⼀种数据格式，既缓慢又臃肿。

**自定义格式**

- 这种格式非常简洁，并提供了非常高的数据结构比(显著高于任何其他格式，不包括纯文本)。 

- 最重要的决定之⼀是使用什么作为分隔符。

  ```
  1:alice:Alice Smith:alice@alicesmith.com;
  2:bob:Bob Jones:bob@bobjones.com;
  ```

##### 11.5.4.2 数据格式总结

- ⼀般支持轻量级格式; 最好的格式是JSON和字符分隔的 ⾃定义格式。如果数据集很大，解析时间成为问题，可以使用以下两种技术之⼀:
  - JSON-P数据，使用动态脚本标记插⼊获取。这将数据视为可执行的JavaScript，而不是字符串，并允许极快的解析。这可以跨域使用，但不应该用于敏感数据。
  - 字符分隔的自定义格式，使用XHR或动态脚本标记插入获取，并使用split()进行解析。这种技术解析超大数据集的速度略快于JSON-P技术，而且通常具有较小的文件大小。

#### 11.5.5 缓存数据

- 最快的Ajax请求是不必发出的请求。防止不必要的请求有两种主要方法:
  - 在服务器端，设置HTTP报头，以确保响应将缓存在浏览器中。
  - 在客户端，将获取的数据存储在本地，这样就不会再次请求它。

