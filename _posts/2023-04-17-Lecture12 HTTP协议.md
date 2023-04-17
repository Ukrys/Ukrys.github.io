---
layout:     post
title:      Web前端-Lec12 HTTP协议
subtitle:   Web前端笔记
date:       2023-04-17
author:     ukrys
header-img: img/post-bg-js-version.jpg
catalog: 	 true
tags:
    - Web
    - Notes
    - HTTP
---

## Lecture12 HTTP协议

### 12.1 Web与HTTP

- Web页面由对象组成

- 对象可以是HTML文件、JPEG图像、音频文件...

- Web页面由基本html文件组成，其中包含几个引用对象

- 每个对象都可以通过URL寻址

- 实例URL（统一资源定位器）

  ```
  /*   host name   *//*  path name  */         
  www.someschool.edu/someDept/pic.gif
  ```

### 12.2 HTTP 总览

- HTTP：超文本传输协议

  超文本传输协议（HTTP）是⼀种为分布式，协作式的，超媒体信息系统。它是⼀种通用的，无状态（stateless）的协议，除了应用于超文本传输外，它也可以应用于诸如名称服务器和分布对象管理系统之类的系统， 这可以通过扩展它的请求方法，错误代码和消息头来实现。HTTP的⼀个特性就是是数据表现形式是可以定义的和可协商性的，这就允许系统能独立于于数据传输被构建。 

- Web的应用层协议

- 客户机/服务器模型

  - 客户端：请求、接收、显示Web对象的浏览器
  - 服务器：Web服务器发送对象以响应请求

- 使用TCP：

  - 客户端启动TCP连接（创建套接字）到服务器，端口80
  - 服务器接收来自客户端的TCP连接
  - 浏览器（HTTP客户端）和Web服务器（HTTP服务器）之间交换HTTP消息（应用层协议消息）
  - TCP连接关闭

- HTTP是无状态的：

  - 服务器不维护关于过去客户端请求的信息
  - 维护“状态”的协议非常复杂！
    - 必须保留过去的历史（状态）
    - 如果服务器/客户端崩溃，它们的“状态”视图可能不一致，必须进行协调

> Request For Comments（RFC），是一系列以编号排定的文件。文件收集了有关互联网相关信息，以及UNIX和互联网社区的软件文件。RFC文件是由Internet Society（ISOC）赞助发行。基本的互联网通信协议都有在RFC文件内详细说明。RFC文件还额外加入许多在标准内的论题，例如对于互联网新开发的协议及发展中所有的记录。因此几乎所有的互联网标准都有收录在RFC文件之中。

### 12.3 HTTP历史与演进

- HTTP Version 0.9
- HTTP 1.0: RFC 1945 
- HTTP 1.1: RFC 2616
- HTTPS (HTTP over TLS, HTTP over SSL, HTTP Secure）
- 2009 Google 设计了基于TCP的SPDY
- HTTP/2 (originally named HTTP/2.0)
  - Hypertext Transfer Protocol version 2 - RFC7540 /9113
  - HPACK - Header Compression for HTTP/2 - RFC7541
- HTTP/3：RFC9114
  - QUIC(Quick UDP Internet Connections, 快速UDP网络连接)

[![pSMh3lR.png](https://s1.ax1x.com/2023/01/14/pSMh3lR.png)](https://imgse.com/i/pSMh3lR)

### 12.4 HTTP/2

- HTTP/2 是 HTTP 网络协议的⼀个重要版本。HTTP / 2 的主要目标是通过启用完整的请求和响应多路复用来减少延迟，通过有效压缩 HTTP 标头字段来最小化协议开销，并增加对请求优先级和服务器推送的支持。
- HTTP/2 不会修改 HTTP 协议的语义。HTTP 1.1 中的所有核心概念（例如 HTTP 方法，状态码，URI 和 headers）都得以保留。而是修改了 HTTP/2 数据在客户端和服务器之间的格式 （帧）和传输方式，这两者都管理整个过程，并在新的框架层内隐藏了应用程序的复杂性。所以，所有现有的应用程序都可以不经修改地交付。

### 12.5 请求 — 响应

- HTTP 的结构很简单：

  - 客户端发送请求
  - 服务器返回一个响应

- HTTP可以在单个TCP连接上支持多个请求-应答交换

- HTTP客户端和服务器端使用TCP套接字接口进行通信

  [![pSM4PHK.png](https://s1.ax1x.com/2023/01/14/pSM4PHK.png)](https://imgse.com/i/pSM4PHK)

### 12.6 HTTP 事务延迟

[![pSM4V9H.png](https://s1.ax1x.com/2023/01/14/pSM4V9H.png)](https://imgse.com/i/pSM4V9H)

- 影响HTTP的常见的与tcp相关的延迟
  - TCP连接建立（三次握⼿）
  - TCP慢启动拥塞控制
  - Nagle的数据聚合算法
  - TCP用于承载确认的延迟确认算法
  - TIME_WAIT延迟和端⼝耗尽

### 12.7 HTTP/1.x 的连接管理

[![pSM4mjI.png](https://s1.ax1x.com/2023/01/14/pSM4mjI.png)](https://imgse.com/i/pSM4mjI)

#### 12.7.1 短连接

- 每一个 HTTP 请求都由它自己独立的连接完成；这意味着发起每一个 HTTP 请求之前都会有一次 TCP 握手，而且是连续不断的。
- 这是 HTTP/1.0 的默认模型（如果没有指定 Connection 协议头，或者是值被设置为 close）。而在 HTTP/1.1 中，只有当 Connection 被设置为 close 时才会用到这个模型。
- 短连接有两个比较大的问题：创建新连接耗费的时间尤为明显，另外 TCP 连接的性能只有在该连接被使用一段时间后 (热连接) 才能得到改善。

#### 12.7.2 长连接/持久连接

- ⼀个长连接会保持⼀段时间，重复用于发送⼀系列请求，节省了新建 TCP 连接握⼿的时间，还可以利用 TCP 的性能增强能力。当然这个连接也不会⼀直保留着：连接在空闲⼀段时间后会被关闭 (服务器可以使用 Keep-Alive 协议头来指定⼀个最小的连接保持时间)。
- 长连接也还是有缺点的；就算是在空闲状态，它还是会消耗服务器资源，而且在重负载时，还有可能遭受 DoS attacks 攻击。这种场景下， 可以使用非长连接，即尽快关闭那些空闲的连接，也能对性能有所提升。
- HTTP/1.0 里默认并不使用长连接。把 Connection 设置成 close 以外的其它参数都可以让其保持长连接，通常会设置为 retry-after。
- 在 HTTP/1.1 里，默认就是长连接的，协议头都不用再去声明它 (但我们还是会把它加上，万⼀某个时候因为某种原因要退回到 HTTP/1.0 呢)。

#### 12.7.3 HTTP 流水线

- 默认情况下，HTTP 请求是按顺序发出的。下⼀个请求只有在当前请求收到应答过后才会被发出。由于会受到网络延迟和带宽的限制，在下⼀个请求被发送到服务器 之前，可能需要等待很长时间。
- 流水线是在同⼀条长连接上发出连续的请求，而不用等待应答返回。这样可以避免连接延迟。理论上讲，性能还会因为两个 HTTP 请求有可能被打包到⼀个 TCP 消息包中而得到提升。就算 HTTP 请求不断的继续，尺寸会增加，但设置 TCP 的 MSS(Maximum Segment Size) 选项，仍然足够包含⼀系列简单的请求。
- 并不是所有类型的 HTTP 请求都能用到流水线：只有 idempotent 方式，比如 GET、HEAD、PUT 和 DELETE 能够被安全的重试：如果有故障发生时，流水线的内容要能被轻易的重试。
- 今天，所有遵循 HTTP/1.1 的代理和服务器都应该⽀持流水线，虽然实际情况中还 是有很多限制：⼀个很重要的原因是，⽬前没有现代浏览器默认启用这个特性。

#### 12.7.4 域名分片

- 如果服务器端想要更快速的响应网站或应用程序的应答，它可以迫使客户端建立更多的连接。例如，不要在同⼀个域名下获 取所有资源，假设有个域名 是 www.example.com，我们可以把它拆分成好几个域名：www1.example.com、 www2.example.com、 www3.example.com。所有这些域名都指向同⼀台服务器，浏览器会同时为每个域名建立 6 条连接 (在我们这个例子中，连接数会达到 18 条)。这⼀技术被称作域名分片。

- 备注： 除非你有紧急而迫切的需求，不要使用这⼀过时的技术，升级到 HTTP/2 就 好了。

  | [![pSM7B9S.png](https://s1.ax1x.com/2023/01/14/pSM7B9S.png)](https://imgse.com/i/pSM7B9S) | [![pSM7sXj.png](https://s1.ax1x.com/2023/01/14/pSM7sXj.png)](https://imgse.com/i/pSM7sXj) |
  | ------------------------------------------------------------ | ------------------------------------------------------------ |

### 12.8 HTTP 事务

[![pSM76ns.png](https://s1.ax1x.com/2023/01/14/pSM76ns.png)](https://imgse.com/i/pSM76ns)

### 12.9 HTTP 消息

- HTTP 消息是服务器和客户端之间交换数据的方式
- HTTP 消息由采用 ASCII 编码的多行文本构成
- 有两种类型的消息：
  - 请求（requests）—— 由客户端发送用来触发一个服务器上的动作。
  - 响应（responses）—— 来自服务器的应答。

[![pSM7WNV.png](https://s1.ax1x.com/2023/01/14/pSM7WNV.png)](https://imgse.com/i/pSM7WNV)

#### 12.9.1 消息组成

- HTTP 请求和响应具有相似的结构，有以下部分组成：

  - ⼀行起始行用于描述要执行的请求，或者是对应的状态，成功或失败。这个起始行总是单行的。
  - ⼀个可选的 HTTP 头集合指明请求或描述消息正文。
  - ⼀个空行指示所有关于请求的元数据已经发送完毕。
  - ⼀个可选的包含请求相关数据的正文 (比如 HTML 表单内容), 或者响应相关的文档。正文的大小有起始行的 HTTP 头来指定。

- 起始行和 HTTP 消息中的 HTTP 头统称为请求头，而其有效负载被称为消息正文。

  [![pSM77u9.png](https://s1.ax1x.com/2023/01/14/pSM77u9.png)](https://imgse.com/i/pSM77u9)

#### 12.9.2 请求消息

- HTTP 请求消息

  - ASCII
  - 行以CRLF `\r\n` 结尾
  - 第一行叫做“请求行”

  [![pSM7X4K.png](https://s1.ax1x.com/2023/01/14/pSM7X4K.png)](https://imgse.com/i/pSM7X4K)

**请求方法：**

- GET：从服务器获取URL对应的资源
- HEAD：除了服务器响应中不能包含消息体，该方法与GET一样。用于只需少数元信息的情况
- POST：被设计用来注解、修改URL所对应的资源
- PUT：被设计用来修改或创建资源。当URL对应的资源存在时，则提交的作为新版本，否则新建资源
- DELETE：被设计用来删除URL对应的资源
- TRACE：主要用来测试。服务器将最终接收到的请求本身发送回来，作为客户端诊断依据
- OPTIONS：客户端查询服务器对与某URL允许的通信选项
- CONNECT：保留的方法名，用于代理切换隧道

支持扩展

| GET方法示例<br />[![pSMHFEt.png](https://s1.ax1x.com/2023/01/14/pSMHFEt.png)](https://imgse.com/i/pSMHFEt) |
| :----------------------------------------------------------: |
| **POST方法示例**<br />[![pSMHVC8.png](https://s1.ax1x.com/2023/01/14/pSMHVC8.png)](https://imgse.com/i/pSMHVC8) |
| **TRACE示例**[![pSMHmvQ.png](https://s1.ax1x.com/2023/01/14/pSMHmvQ.png)](https://imgse.com/i/pSMHmvQ) |

- 头域

  - 由主键/值对组成，描述客户端或者服务器的属性、被传输的资源以及应该实现连接。
  - 四种不同类型的头标：
    - 通用头标：即可用于请求，也可用于响应，是作为⼀个整体而不是特定资源与事务相关联。
    - 请求头标：允许客户端传递关于自身的信息和希望的响应形式。
    - 响应头标：服务器和于传递自身信息的响应。
    - 实体头标：定义被传送资源的信息。即可用于请求，也可用于响应。

  ```http
  Accept: text/html
  Host: www.nju.edu.cn
  From: abc@nju.edu.cn
  User-Agent: Mozilla/4.0
  Referer: http://test.com/abc
  ```

#### 12.9.3 响应消息

- HTTP 响应消息

  - ASCII 状态行
  - 头域
  - 内容

  [![pSMHY2F.png](https://s1.ax1x.com/2023/01/14/pSMHY2F.png)](https://imgse.com/i/pSMHY2F)

- 响应状态行
  - http 协议版本 HTTP-Version
  - 状态码（三位数字）Status-Code
  - 状态描述 Reason-Phrase

##### 12.9.3.1 状态码

- HTTP 响应状态码用来表明特定 HTTP 请求是否成功完成。 响应被归为以下五大类：

  - 信息响应 (100–199) 

  - 成功响应 (200–299) 

  - 重定向消息 (300–399) 

  - 客户端错误响应 (400–499) 

  - 服务端错误响应 (500–599)

**常用状态码：**

| 200     | OK                        |
| ------- | ------------------------- |
| **301** | **Moved permanently**     |
| **400** | **Bad Request**           |
| **401** | **Unauthorized**          |
| **403** | **forbidden**             |
| **404** | **Not Found**             |
| **500** | **Internal Server Error** |

**消息响应：**

<table>
    <tr>
    	<td>100</td>
        <td>Continue</td>
    	<td>这个临时响应表明，迄今为止的所有内容都是可行的，客户端应该继续请求， 如果已经完成，则忽略它。</td>
    </tr>
    <tr>
    	<td>101</td>
        <td>Switching Protocols</td>
    	<td>该代码是响应客户端的 Upgrade (en-US) 请求头发送的，指明服务器即将切换的协议。</td>
    </tr>
    <tr>
    	<td>102</td>
        <td> Processing（WebDAV）</td>
        <td>此代码表示服务器已收到并正在处理该请求，但当前没有响应可用。</td>
    </tr>
    <tr>
    	<td>103</td>
        <td>Early Hints</td>
    	<td>此状态代码主要用于与 Link 链接头⼀起使用，以允许用户代理在服务器准备响应阶段时开始预加载 preloading 资源。</td>
    </tr>
</table>

**成功响应：**

<table>
    <tr>
    	<td>200</td>
        <td>OK</td>
        <td>请求成功。</td>
    </tr>
    <tr>
    	<td>201</td>
        <td>Created</td>
        <td>该请求已成功，并因此创建了⼀个新的资源。这通常是在 POST 请求，或是某些 PUT 请求之后返回的响应。</td>
    </tr>
    <tr>
    	<td>202</td>
        <td>Accepted</td>
        <td>请求已经接收到，但还未响应，没有结果。意味着不会有⼀个异步的响应去表明当前请求的结果，预期另外的进程和服务去处理请求，或者批处理。
- </td>
    </tr>
    <tr>
    	<td>203</td>
        <td>Non-Authoritative Information</td>
        <td>服务器已成功处理了请求，但返回的实体头部元信息不是在原始服务器上有效的确定集合，而是来自本地或者第三方的拷贝。当前的信息可能是原始版本的子集或者超集。例如，包含资源的元数据可能导致原始服务器知道元信息的超集。使用此状态码不是必须的，而且只有在响应不使用此状态码便会返回200 OK的情况下才是合适的。</td>
    </tr>
    <tr>
    	<td>204</td>
        <td>No Content</td>
        <td>对于该请求没有的内容可发送，但头部字段可能有用。用户代理可能会用此时请求头部信息来更新原来资源的头部缓存字段。</td>
    </tr>
    <tr>
    	<td>205</td>
        <td>Reset Content</td>
        <td>告诉用户代理重置发送此请求的文档。</td>
    </tr>
    <tr>
    	<td>206</td>
        <td>Partial Content</td>
        <td>当从客户端发送Range范围标头以只请求资源的⼀部分时，将使用此响应代码。</td>
    </tr>
    <tr>
    	<td>207</td>
        <td>Multi-Status（WebDAV）</td>
        <td>对于多个状态代码都可能合适的情况，传输有关多个资源的信息。</td>
    </tr>
    <tr>
    	<td>208</td>
        <td>Already Reported（WebDAV）</td>
        <td>在 DAV 里面使用户响应元素以避免重复枚举多个绑定的内部成员到同⼀个集合。</td>
    </tr>
    <tr>
        <td>226</td>
        <td>IM Used（HTTP Delta encoding）</td>
        <td>服务器已经完成了对资源的GET请求，并且响应是对当前实例应用的⼀个或多个实例操作结果的表示。</td>

**重定向消息：**

<table>
    <tr>
    	<td>300</td>
        <td>Multiple Choice</td>
        <td>请求拥有多个可能的响应。用户代理或者用户应当从中选择⼀个。</td>
    </tr>
    <tr>
    	<td>301</td>
        <td>Moved Permanently</td>
        <td>请求资源的 URL 已永久更改。在响应中给出了新的 URL。</td>
    </tr>
    <tr>
    	<td>302</td>
        <td>Found</td>
        <td>此响应代码表示所请求资源的 URI 已暂时更改。未来可能会对 URI 进⾏进⼀步的改变。因此，客户机应该在将来的请求中使用这个相同的 URI。</td>
    </tr>
    <tr>
    	<td>303</td>
        <td>See Other</td>
        <td>服务器发送此响应，以指示客户端通过⼀个 GET 请求在另⼀个 URI 中获取所请求的资源。</td>
    </tr>
    <tr>
    	<td>304</td>
        <td>Not Modified</td>
        <td>这是用于缓存的目的。它告诉客户端响应还没有被修改，因此客户端可以继续使用相同的缓存版本的响应。</td>
    </tr>
    <tr>
    	<td>305</td>
        <td>Use Proxy 已弃用</td>
        <td>在 HTTP 规范中定义，以指示请求的响应必须被代理访问。由于对代理的带内配置的安全考虑，它已被弃用。</td>
    </tr>
    <tr>
    	<td>306</td>
        <td>unused</td>
        <td>此响应代码不再使用；它只是保留。它曾在 HTTP/1.1 规范的早期版本中使用过。</td>
    </tr>
    <tr>
    	<td>307</td>
    	<td>Temporary Redirect</td>
        <td>服务器发送此响应，以指示客户端使用在前⼀个请求中使用的相同方法在另⼀个 URI 上获取所请求的资源。这与 302 Found HTTP 响应代码具有相同的语义，但用户代理不能更改所使用的 HTTP 方法：如果在第⼀个请求中使用了 POST，则在第二个请求中必须使用 POST</td>
    </tr>
    <tr>
    	<td>308</td>
        <td>Permanent Redirct</td>
        <td>这意味着资源现在永久位于由Location: HTTP Response 标头指定的另⼀个 URI。这与 301 Moved Permanently HTTP 响应代码具有相同的语义，但用户代理不能更改所使用的 HTTP 方法：如果在第⼀个请求中使用 POST，则必须在第二个请求中使用 POST。</td>
    </tr>
</table>

> **什么情况下使用301重定向：**
>
> - 迁移到另外⼀个域名时，通过301永久重定向将旧域名重定向⾄新域名，挽回流量损失和SEO。
>
> - 保持链接有效
>
>   - 当重构 Web 站点的时候，资源的 URL 会发生改变。你并不想因此而使旧链接失效，因为它们会带来宝贵的用户（并且帮助优化你的 SEO），所以需要建立从旧链接到新链接的重定向映射。
>
> - 如果有多个闲置域名需要指向同一网站时，通过301永久重定向可以实现。
>
> - 打算实现网址规范化
>
> - 强制使用 HTTPS 协议。对于 HTTP 版本站点的请求会被重定向至采用了 HTTPS 协议的版本。
>
>   [![pSMOFsg.png](https://s1.ax1x.com/2023/01/14/pSMOFsg.png)](https://imgse.com/i/pSMOFsg)
>
> **临时重定向：**
>
> - 有时候请求的资源无法从其标准地址访问，但是却可以从另外的地方访问。在这种情况下可以使用临时重定向。
>
> - 搜索引擎不会记录该新的、临时的链接。在创建、更新或者删除资源的时候，临时重定向也可以用于显示临时性的进度页面。
>
>   | 编码 | 含义               | 处理方法                                                     | 典型应用场景                                                 |
>   | ---- | ------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
>   | 302  | Found              | GET 方法不会发生变更，其他方法有可能会变更为 GET 方法。      | 由于不可预见的原因该页面暂不可用。在这种情况下，搜索引擎不会更新它们的链接。 |
>   | 303  | See Other          | GET 方法不会发生变更，其他方法会变更为 GET 方法（消息主体会丢失）。 | 用于 PUT 或 POST 请求完成之后进行页面跳转来防止由于页面刷新导致的操作的重复触发。 |
>   | 307  | Temporary Redirect | 方法和消息主体都不发生变化。                                 | 由于不可预见的原因该页面暂不可用。在这种情况下，搜索引擎不会更新它们的链接。当站点支持非 GET 方法的链接或操作的时候，该状态码优于 302 状态码。 |
>
> **特殊重定向：**
>
> ​		[![pSQV58O.png](https://s1.ax1x.com/2023/01/14/pSQV58O.png)](https://imgse.com/i/pSQV58O)

**客户端错误响应：**

<table>
    <tr>
    	<td>400</td>
        <td>Bad Request</td>
        <td>由于被认为是客户端错误（例如，错误的请求语法、无效的请求消息帧或欺骗性的请求路由），服务器无法或不会处理请求。</td>
    </tr>
    <tr>
    	<td>401</td>
        <td>Unauthorized</td>
        <td>虽然 HTTP 标准指定了"unauthorized"，但从语义上来说，这个响应意味着"unauthenticated"。也就是说，客户端必须对自身进行身份验证才能获得请求的响应。</td>
    </tr>
    <tr>
    	<td>402</td>
        <td>Payment Required</td>
        <td>实验性；此响应代码保留供将来使用。创建此代码的最初目的是将其用于数字支付系统，但是此状态代码很少使用，并且不存在标准约定。</td>
    </tr>
    <tr>
    	<td>403</td>
        <td>Forbidden</td>
        <td>客户端没有访问内容的权限；也就是说，它是未经授权的，因此服务器拒绝提供请求的资源。与 401 Unauthorized 不同，服务器知道客户端的身份。</td>
    </tr>
    <tr>
    	<td>404</td>
        <td>Not Found</td>
        <td>服务器找不到请求的资源。在浏览器中，这意味着无法识别 URL。在 API 中，这也可能意味着端点有效，但资源本身不存在。服务器也可以发送此响应，而不是 403 Forbidden，以向未经授
权的客户端隐藏资源的存在。这个响应代码可能是最广为⼈知的，因为它经常出现在网络上。</td>
    </tr>
    <tr>
    	<td>405</td>
        <td>Method Not Allowed</td>
        <td>服务器知道请求方法，但目标资源不支持该⽅法。例如，API 可能不允许调用DELETE来删除资源。</td>
    </tr>
    <tr>
    	<td>406</td>
        <td>Not Acceptable</td>
        <td>当 web 服务器在执行服务端驱动型内容协商机制后，没有发现任何符合用户代理给定标准的内容时，就会发送此响应。</td>
    </tr>
    <tr>
    	<td>407</td>
        <td>Proxy Authentication Required</td>
        <td>类似于 401 Unauthorized 但是认证需要由代理完成。</td>
    </tr>
    <tr>
    	<td>408</td>
        <td>Request Timeout</td>
        <td>此响应由⼀些服务器在空闲连接上发送，即使客户端之前没有任何请求。这意味着服务器想关闭这个未使用的连接。由于⼀些浏览器，如 Chrome、Firefox 27+ 或 IE9，使⽤ HTTP 预连接机
制来加速冲浪，所以这种响应被使用得更多。还要注意的是，有些服务器只是关闭了连接⽽没有发送此消息。</td>
    </tr>
    <tr>
    	<td>409</td>
        <td>Conflict</td>
        <td>当请求与服务器的当前状态冲突时，将发送此响应。</td>
    </tr>
    <tr>
    	<td>410</td>
        <td>Gone</td>
        <td>当请求的内容已从服务器中永久删除且没有转发地址时，将发送此响应。客户端需要删除缓存和指向资源的链接。HTTP 规范打算将此状态代码用于“有限时间的促销服务”。API 不应被迫指出
已使用此状态代码删除的资源。</td>
    </tr>
    <tr>
    	<td>410</td>
        <td>Gone</td>
        <td>当请求的内容已从服务器中永久删除且没有转发地址时，将发送此响应。客户端需要删除缓存和指向资源的链接。HTTP 规范打算将此状态代码用于“有限时间的促销服务”。API 不应被迫指出
已使用此状态代码删除的资源。</td>
    </tr>
    <tr>
    	<td>411</td>
        <td>Length Required</td>
        <td>服务端拒绝该请求因为 Content-Length 头部字段未定义但是服务端需要它。</td>
    </tr>
    <tr>
    	<td>412</td>
        <td>Precondition Failed</td>
        <td>客户端在其头文件中指出了服务器不满足的先决条件。</td>
    </tr>
    <tr>
    	<td>413</td>
        <td>Payload Too Large</td>
        <td>请求实体⼤于服务器定义的限制。服务器可能会关闭连接，或在标头字段后返回重试 Retry-After。</td>
    </tr>
    <tr>
    	<td>414</td>
        <td>URI Too Long</td>
        <td>客户端请求的 URI ⽐服务器愿意接收的长度长。</td>
    </tr>
    <tr>
    	<td>415</td>
        <td>Unsupported Media Type</td>
        <td>服务器不支持请求数据的媒体格式，因此服务器拒绝请求。</td>
    </tr>
    <tr>
    	<td>416</td>
        <td>Range Not Satisfiable</td>
        <td>无法满足请求中 Range 标头字段指定的范围。该范围可能超出了目标 URI 数据的大小。</td>
    </tr>
    <tr>
    	<td>417</td>
        <td>Expectation Failed</td>
        <td>此响应代码表示服务器无法满⾜ Expect 请求标头字段所指示的期望。</td>
    </tr>
    <tr>
    	<td>418</td>
        <td>I'm a teapot</td>
        <td>服务端拒绝用茶壶煮咖啡。笑话，典故来源茶壶冲泡咖啡。</td>
    </tr>
    <tr>
    	<td>421</td>
        <td>Misdirected Request</td>
        <td>请求被定向到无法生成响应的服务器。这可以由未配置为针对请求 URI 中包含的方案和权限组合生成响应的服务器发送。</td>
    </tr>
    <tr>
    	<td>422</td>
        <td>Unprocessable Entity(WebDAV)</td>
        <td>请求格式正确，但由于语义错误⽽无法遵循。</td>
    </tr>
    <tr>
    	<td>423</td>
        <td>Locked(WebDAV)</td>
        <td>正在访问的资源已锁定。</td>
    </tr>
    <tr>
    	<td>424</td>
        <td>Failed Dependency(WebDAV)</td>
        <td>由于前⼀个请求失败，请求失败。</td>
    </tr>
    <tr>
    	<td>425</td>
        <td>Too Early</td>
        <td>实验性;表示服务器不愿意冒险处理可能被重播的请求。</td>
    </tr>
    <tr>
    	<td>426</td>
        <td>Upgrade Required</td>
        <td>服务器拒绝使用当前协议执行请求，但在客户端升级到其他协议后可能愿意这样做。服务端发送带有Upgrade (en-US) 字段的 426 响应来表明它所需的协议（们）。</td>
    </tr>
    <tr>
    	<td>428</td>
        <td>Precondition Required</td>
        <td>源服务器要求请求是有条件的。此响应旨在防⽌'丢失更新'问题，即当第三方修改服务器上的状态时，客户端 GET 获取资源的状态，对其进⾏修改并将其 PUT 放回服务器，从而导致冲突。</td>
    </tr>
    <tr>
    	<td>429</td>
        <td>Too Many Requests</td>
        <td>用户在给定的时间内发送了太多请求（"限制请求速率"）</td>
    </tr>
    <tr>
    	<td>431</td>
        <td>Request Header Fields Too Large</td>
        <td>服务器不愿意处理请求，因为其头字段太大。在减⼩请求头字段的大⼩后，可以重新提交请求。</td>
    </tr>
    <tr>
    	<td>451</td>
        <td>Unavailable For Legal Reasons</td>
        <td>⽤户代理请求了无法合法提供的资源，例如政府审查的网⻚。</td>
    </tr>
</table>

**服务端错误响应：**

<table>
    <tr>
    	<td>500</td>
        <td>Internal Server Error</td>
        <td>服务器遇到了不知道如何处理的情况。</td>
    </tr>
     <tr>
    	<td>501</td>
        <td>Not Implemented</td>
        <td>服务器不支持请求方法，因此⽆法处理。服务器需要⽀持的唯二方法（因此不能返回此代码）是 GET and HEAD.</td>
    </tr>
     <tr>
    	<td>502</td>
        <td>Bad Gateway</td>
        <td>此错误响应表明服务器作为网关需要得到一个处理这个请求的响应，但是得到一个错误的响应。</td>
    </tr>
     <tr>
    	<td>503</td>
        <td>Service Unavailable</td>
        <td>服务器没有准备好处理请求。常见原因是服务器因维护或重载而停机。请注意，与此响应一起，应发送解释问题的用户友好页面。这个响应应该用于临时条件和如果可能的话，HTTP 标头 Retry-After 字段应该包含恢复服务之前的估计时间。网站管理员还必须注意与此响应一起发送的与缓存相关的标头，因为这些临时条件响应通常不应被缓存。</td>
    </tr>
     <tr>
    	<td>504</td>
        <td>Gateway Timeout</td>
        <td>当服务器充当网关且无法及时获得响应时，会给出此错误响应。</td>
    </tr>
     <tr>
    	<td>505</td>
        <td>HTTP Version Not Supported</td>
        <td>服务器不支持请求中使用的 HTTP 版本。</td>
    </tr>
     <tr>
    	<td>506</td>
        <td>Variant Also Negotiates</td>
        <td>服务器存在内部配置错误：所选的变体资源被配置为参与透明内容协商本身，因此不是协商过程中的适当终点。</td>
    </tr>
     <tr>
    	<td>507</td>
        <td>Insufficient Storage(WebDAV)</td>
        <td>无法在资源上执行该⽅法，因为服务器无法存储成功完成请求所需的表示。</td>
    </tr>
     <tr>
    	<td>508</td>
        <td>Loop Detected(WebDAV)</td>
        <td>服务器在处理请求时检测到无限循环。</td>
    </tr>
     <tr>
    	<td>510</td>
        <td>Not Extended</td>
        <td>服务器需要对请求进行进一步扩展才能完成请求。</td>
    </tr>
     <tr>
    	<td>511</td>
        <td>Network Authentication Required</td>
        <td>指示客户端需要进行身份验证才能获得网络访问权限。</td>
    </tr>
</table>

##### 12.9.3.2 Body

- 请求/响应的最后一部分是它的 body
  - 不是所有的请求都有⼀个 body：例如获取资源的请求，GET，HEAD， DELETE 和 OPTIONS，通常它们不需要 body。有些请求将数据发送到服务器 以便更新数据：常见的情况是 POST 请求（包含 HTML 表单数据）。
  - 不是所有的响应都有 body：具有状态码 (如 201 或 204) 的响应，通常不会有 body。
- 任何消息
- 需要Content-Length、Content-Type

### 12.10 HTTP/1.x  &  HTTP/2

#### 12.10.1 HTTP/1.x 报文缺点

- HTTP/1.x 报文有⼀些性能上的缺点：
  - Header 不像 body，它不会被压缩。
  - 两个报文之间的 header 通常非常相似，但它们仍然在连接中重复传输。
  - 无法复用。当在同⼀个服务器打开几个连接时：TCP 热连接比冷连接更加有效。

#### 12.10.2 HTTP/2 - 为了更优异的表现

- 在 2010 年到 2015 年，谷歌通过实践了⼀个实验性的 SPDY 协议，证明了⼀个在客户端和服务器端交换数据的另类方式。其收集了浏览器和服务器端的开发者的焦点问题。明确了响应数量的增加和解决复杂的数据传输，SPDY 成为了 HTTP/2 协议的基础。
- HTTP/2 在 HTTP/1.1 有几处基本的不同：
  - HTTP/2 是⼆进制协议而不是文本协议。不再可读，也不可无障碍的手动创建，改善的优化技术现在可被实施。
  - 这是⼀个复用协议。并行的请求能在同⼀个链接中处理，移除了 HTTP/1.x 中顺序和阻塞的约束。
  - 压缩了 headers。因为 headers 在⼀系列请求中常常是相似的，其移除了重复和传输重复数据的成本。
  - 其允许服务器在客户端缓存中填充数据，通过⼀个叫服务器推送的机制来提前请求。

### 12.11 流、消息、帧

- 流（Stream）：是在HTTP/2连接中在客户端和服务器之间交换的独立双向帧序列。流是连接中的⼀个虚拟信道，可以承载双向消息传输。每个流有唯⼀整数标识符。为了防止两端流 ID冲突，客户端发起的流具有奇数ID，服务器端发起的流具有偶数ID。能携带⼀个至多个消息。
- 消息（Message）：⼀个完整的请求或者响应，比如请求、响应等，由⼀个或多个组成。
- 帧（Frame）：在HTTP/2通信的最小单元。每个帧包括⼀个帧头，里面有个很小标志，来区别是属于哪个流。

#### 12.11.1 流的重要特征

- ⼀个HTTP/2连接可以包含多个同时打开的流，并且可以从多 个流中交叉帧。
- 流可以单独建立和使用，也可以由客户端或服务器共享。
- 流可以由任⼀端点关闭。
- 帧在流上发送的顺序非常重要。 收件⼈按收到的顺序处理框架。 特别是，HEADERS和DATA帧的顺序在语义上很重要。
- 流用无符号的31位整数标识。 流标识符由启动流的端点分配给流。客户端发起的流必须使用奇数流标识符;那些由服务器发起的必须使用偶数流标识符。

#### 12.11.2 二进制格式

[![pSQef1O.png](https://s1.ax1x.com/2023/01/15/pSQef1O.png)](https://imgse.com/i/pSQef1O)

#### 12.11.3 二进制帧层

| [![pSQehcD.png](https://s1.ax1x.com/2023/01/15/pSQehcD.png)](https://imgse.com/i/pSQehcD) | [![pSQe4je.png](https://s1.ax1x.com/2023/01/15/pSQe4je.png)](https://imgse.com/i/pSQe4je) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |

#### 12.11.4 请求和响应多路复用

| [![pSQeInH.png](https://s1.ax1x.com/2023/01/15/pSQeInH.png)](https://imgse.com/i/pSQeInH) |
| :----------------------------------------------------------: |
| [![pSQeoBd.png](https://s1.ax1x.com/2023/01/15/pSQeoBd.png)](https://imgse.com/i/pSQeoBd) |

#### 12.11.5 流量控制

- 流量控制特定于连接。两种类型的流量控制都位于单跳的端点之间，而不是整个端到端路径。

- 流量控制基于WINDOW_UPDATE帧。接收者宣告他们准备在一个流上以及整个连接上接收多少个字节。
- 流量控制是由接收器提供的全面控制方向。接收者可以选择为每个流和整个连接设置它想要的任何窗口大小。发送方必须遵守接收方施加的流量控制限制。客户端，服务器和中介都独立地将其流量控制窗口作为接收者进行通告，并遵守发送时由对等方设置的流量控制限制。
- 对于新流和整个连接，流量控制窗口的初始值为65,535个八比特组。
- 帧类型决定流量控制是否适⽤于帧。在本文档中指定的帧中，只有数据帧受流量控制; 所有其他帧类型不会占用通告的流量控制窗口中的空间。这确保了重要的控制框架不会被流量控制阻塞。
- 流量控制不能禁用。
- HTTP/2仅定义WINDOW_UPDATE帧的格式和语义。

#### 12.11.6 优先级和依赖性

- 每个流都包含⼀个优先级（也就是“权重”），它被用来告诉对端哪个流更重要。当资源有限的时候，服务器会根据优先级来选择应该先发送哪些流。
- 客户端可以通过在打开流的HEADERS帧中包含优先级信息来为新流分配优先级。在其他任何时候，PRIORITY帧都可以用来改变流的优先级。
- 每个流可以被赋予对另⼀个流的显式依赖。包括依赖关系表示优先将资源分配给识别的流而不是依赖流。借助于PRIORITY帧，客户端同样可以告知服务器当前的流依赖于其他哪个流。该功能让客户端能建立⼀个优先级“树” ， 所有“子流”会依赖于“父流”的传输完成情况。
- 优先级和依赖关系可以在传输过程中被动态的改变。这样当用户滚动⼀个全是图片的页面的时候，浏览器就能够指定哪个图片拥有更高的优先级。或者是在你切换标签页的时候，浏览器可以提升新切换到页面所包含流的优先级。

#### 12.11.7 服务器推送

- 这个功能通常被称作“缓存推送”。主要的思想是：当⼀个客户端请求资源X，而服务器知道它很可能也需要资源Z的情况下，服务器可以在客户端发送请求前，主动将资源Z推送给客户端。这个功能帮助客户端将Z放进缓存以备将来之需。

- 服务器推送需要客户端显式的允许服务器提供该功能。但即使如此，客户端依然能自主选择是否需要中断该推送的流。如果不需要的话，客户端可以通过发送⼀个RST_STREAM帧来中止。

  [![pSQejgS.png](https://s1.ax1x.com/2023/01/15/pSQejgS.png)](https://imgse.com/i/pSQejgS)

### 12.12 头压缩

- http1.x的头带有大量信息，而且每次都要重复发送。http/2使用encoder来减少需要传输的header大小，通讯双⽅各自缓存⼀份头部字段表，既避免了重复 header的传输，⼜减小了需要传输的大小。
- 对于相同的数据，不再通过每次请求和响应发送，通信期间几乎不会改变通用键-值对(用户代理、可接受的媒体类型，等等)只需发送一次。
- 事实上,如果请求中不包含首部(例如对同⼀资源的轮询请求)，那么，首部开销就是零字节，此时所有首部都自动使用之前请求发送的首部。
- 如果首部发生了变化，则只需将变化的部分加⼊到header帧中，改变的部分会加入到头部字段表中，首部表在 http 2.0 的连接存续期内始终存在，由客户端和服务器共同渐进地更新。
- 需要注意的是，http 2.0关注的是首部压缩，而我们常用的gzip等是报文内容 （body）的压缩，⼆者不仅不冲突，且能够⼀起达到更好的压缩效果。
- http/2使用的是专门为首部压缩而设计的HPACK算法。

​	**头压缩实例：**[![pSQmmDJ.png](https://s1.ax1x.com/2023/01/15/pSQmmDJ.png)](https://imgse.com/i/pSQmmDJ)

​	**协商示例：**

```http
 GET /page HTTP/1.1
 Host: server.example.com
 Connection: Upgrade, HTTP2-Settings
 Upgrade: HTTP/2.0
 HTTP2-Settings: (SETTINGS payload)
 
 HTTP/1.1 200 OK
 Content-length: 243
 Content-type: text/html
 (... HTTP 1.1 response ...)
 	(or)
 
 HTTP/1.1 101 Switching Protocols
 Connection: Upgrade
 Upgrade: HTTP/2.0
 (... HTTP 2.0 response ...)
```

```javascript
const http2 = require('http2');
const fs = require('fs');
const server = http2.createSecureServer({
    key: fs.readFileSync('localhost-privkey.pem'),
    cert: fs.readFileSync('localhost-cert.pem')
});
server.on('error', (err) => console.error(err));
server.on('stream', (stream, headers) => {
    // stream is a Duplex
    stream.respond({
        'content-type': 'text/html',
        ':status': 200
    });
    stream.end('<h1>Hello World</h1>');
});
server.listen(8443)
```

### 12.13 HTTP/3

#### 12.13.1 为何需要HTTP/3

- TCP队头阻塞问题

- TCP握手时长

- 移动场景的网络切换成本

  - IP地址会发⽣变化，而TCP协议是根据四元组来确定⼀个连接的，需要重新建立连接

  [![pSQmQ4x.png](https://s1.ax1x.com/2023/01/15/pSQmQ4x.png)](https://imgse.com/i/pSQmQ4x)

#### 12.13.2 HTTP/3 定义

- HTTP/3基于UDP协议重新定义了连接，在QUIC层实现了无序、并发字节流的传输，解决了队头阻塞问题（包括基于QPACK解决了动态表的队头阻塞）；
- HTTP/3重新定义了TLS协议加密QUIC头部的方式，既提高了网络攻击成本，又降低了建立连接的速度（仅需1个RTT就可以同时完成建链与密钥协商）；
- HTTP/3将Packet、QUIC Frame、HTTP3 Frame分离，实现了连接迁移功能，降低了5G环境下高速移动设备的连接维护成本。

​	![image-20230115004409002](C:\Users\94327\AppData\Roaming\Typora\typora-user-images\image-20230115004409002.png)