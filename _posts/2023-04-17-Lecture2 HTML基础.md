---
layout:     post
title:      Web前端-Lec02 HTML基础
subtitle:   Web前端笔记
date:       2023-04-17
author:     ukrys
header-img: img/post-bg-js-version.jpg
catalog: 	 true
tags:
    - Web
    - Notes
    - html
---

## Lecture2 HTML基础

### 2.1 HTML Overview

- Hypertext Markup Language (HTML) ，全称为超文本标记语言，是⼀种标记语⾔。它包括⼀系列标签．通过这些标签可以将⽹络上的⽂档格式统⼀，使分散的Internet资源连接为⼀个逻辑整体。
- HTML（超⽂本标记语⾔——HyperText Markup Language）是构成 Web 世界的⼀砖⼀瓦。它定义了网页内容的含义和结构。除 HTML 以外的其它技术则通常用来描述⼀个网页的表现与展示效果（如 CSS），或功能与行为（如 JavaScript）-- MDN

#### 2.1.1 HTML版本

- 1989: 伯纳斯-李写了⼀份备忘录，提议建⽴⼀个基于互联⽹的超⽂本系统
- 1995: RFC 1866，HTML 2成为官⽅标准语⾔
- 1997: HTML 4 
- 1999: HTML 4.01 
- 2001-01: XHTML 
- 2014 html5 
- 2016 html5.1 
- 2017 html5.2

#### 2.1.2 HTML and XHTML

- HTML最初是⼀种应用程序标准通⽤标记语⾔(SGML)
  - SGML是⼀种⾮常灵活的标记语⾔
  - 需要⼀个相对复杂、宽松且通常⾃定义的解析器
- XHTML:
  - XML的应用程序，SGML的⼀个更严格的子集
  - 真正的XHTML文档允许使用标准XML工具执行自动化处理

#### 2.1.3 标记语言

- 标记
  - 在文档中嵌入代码
  - 代码被称为“标签”
  - 代码
    - 描述结构文档
    - 包括处理说明
- 标记语言
  - 描述标签语法的计算机语言
  - 可以与其他工具一起使用来指定渲染

- 逻辑标记

  - 描述文档的各个部分
  - 不指定如何渲染

  ```html
  This is <strong>very</strong> important.
  ```

  效果： This is <strong>very</strong> important.

- 逻辑

  - 呈现是客户的“决定”

  - 当客户端⽆法展示时，会出现优雅降级

    ```html
    <img alt=“image description” src=“foo.gif”>
    ```

  > **优雅降级** graceful degradation：
  > 一开始就构建完整的功能，然后再针对低版本浏览器进行兼容。
  >
  > **渐进增强** progressive enhancement：
  > 针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能达到更好的用户体验。
  >
  > 区别：
  > 优雅降级是从复杂的现状开始，并试图减少用户体验的供给
  > 渐进增强则是从一个非常基础的，能够起作用的版本开始，并不断扩充，以适应未来环境的需要
  > 降级（功能衰减）意味着往回看；而渐进增强则意味着朝前看，同时保证其根基处于安全地带

#### 2.1.4 Markdown

- Markdown 是⼀种轻量级标记语⾔，它允许⼈们使⽤易读易写的 纯⽂本格式编写⽂档。
- Markdown 语⾔在 2004 由约翰·格鲁伯（英语：John Gruber）创建。
- Markdown 编写的⽂档可以导出 HTML 、Word、图像、PDF、 Epub 等多种格式的⽂档。
- Markdown 编写的⽂档后缀为 .md, .markdown。
- Markdown 应⽤
  - Markdown 能被使⽤来撰写电⼦书，如：Gitbook。
  - 当前许多⽹站都⼴泛使⽤ Markdown 来撰写帮助⽂档或是⽤于论坛上发 表消息。例如：GitHub、简书、reddit、Diaspora、Stack Exchange、 OpenStreetMap 、SourceForge等。

#### 2.1.5 如何编写(x)HTML

- 编辑器

- 生成器

  - https://github.com/Microsoft/ailab/tree/master/Sketch2Code

    https://sketch2code.azurewebsites.net/

- Sketch2Code处理流程

  - | [<img src="https://s1.ax1x.com/2022/11/28/zUTlF0.png" alt="zUTlF0.png"  />](https://imgse.com/i/zUTlF0) | [![zUT1YV.png](https://s1.ax1x.com/2022/11/28/zUT1YV.png)](https://imgse.com/i/zUT1YV) |
    | ------------------------------------------------------------ | ------------------------------------------------------------ |

#### 2.1.6 HTML基础

- XHTML 或 HTML 文档组成

  - DOCTYPE

    - 使用的文档类型定义DTD 

    - doctype是一种标准通用标记语言的文档类型声明，目的是告诉标准通用标记语言解析器要使用什么样的文档类型定义（DTD）来解析文档。

      doctype在html中的作用就是触发浏览器的标准模式，如果html中省略了doctype，浏览器就会进入到Quirks模式的怪异状态，在这种模式下，有些样式会和标准模式存在差异。

  - Head

    - 元信息 
    - 只有`<title>`是必须的

  - Body

    - 需要呈现的内容

- HTML 元素详解

  - 开始标签（Opening tag）：包含元素的名称（本例为 p），被大于号、小于号所包围。表示元素从这里开始或者开始起作用 —— 在本例中即段落由此开始。
  - 结束标签（Closing tag）：与开始标签相似，只是其在元素名之前包含了⼀个斜杠。这表示着元素的结尾 —— 在本例中即段落在此结束。初学者常常会犯忘 记包含结束标签的错误，这可能会产⽣⼀些奇怪的结果。
  - 内容（Content）：元素的内容，本例中就是所输⼊的⽂本本身。
  - 元素（Element）：开始标签、结束标签与内容相结合，便是⼀个完整的元素。

- 块级元素或⾏内元素

  - 块级元素占据其⽗元素（容器）的整个⽔平空间，垂 直空间等于其内容⾼度，因此创建了⼀个“块” 。
    - 例如: paragraphs, lists, table cells
    - 通常浏览器会在块级元素前后另起⼀个新⾏
  - ⾏内元素只占据它对应标签的边框所包含的空间。
    - 例如: bold text, code fragments, images
    - 浏览器允许许多⾏内元素出现在同⼀⾏上
    - 必须嵌套在块级元素中

- 注释：`<!-- ... -->`

  - 不能嵌套
  - 许多网页根本没有注释

- 网页标题：`<title>`

  ```html
  <title>Chapter 2: HTML Basics</title>
  ```

  - 用于：
    - 定义浏览器⼯具栏中的标题 
    - 提供⻚⾯被添加到收藏夹时的标题 
    - 显示在搜索引擎结果中的⻚⾯标题
  - 标题长度受限
  - SEO（Search Engine Optimization：搜索引擎优化）权重大

- `<meta>`

  ```html
  <meta name=“description" content=“introduction of XXX" />
  <meta http-equiv="Content-Type" content="text/html; charset=gbk" />
  ```

  - ⽤于提供关于HTML⽂档的元数据

  - `<meta>`标签只能出现在`<head>`⾥

  - 标签通常⽤于给出⽹⻚描述、关键词、⽂档作者、最后修改日期等信息。

  - 属性

    | 属性       | 值                                                           | 描述                                          |
    | ---------- | :----------------------------------------------------------- | :-------------------------------------------- |
    | charset    | character_set                                                | HTML5新属性：定义文档的字符编码，通常为 UTF-8 |
    | http-equiv | contennt-type<br>expires<br>refresh<br>set-cookie            | 把content属性关联到http头部                   |
    | name       | author<br>description<br>keywords <br>generator <br>revised <br>others | 把content属性关联到一个名称                   |
    | scheme     | some_text                                                    | (html5不支持)定义用于翻译content属性值的格式  |

    - 设置网页关键字 keywords

      - 设置关键字可以帮助搜索引擎检索信息，但是不会直接显示在网页上。<br>
        语法：`<meta name="keywords" content="具体的关键字">`

        ```html
        <!DOCTYPE html>
        <html>
        	<head>
        		<meta name="keywords" content="诗词" />
        		<title></title>
        	</head>
        	<body>	
        	</body>
        </html>
        ```

    - 设置网页说明

      - 设置网页说明也是为了方便搜索引擎搜索，它用来详细说明网页的内容，同样不会在网页上直接显示出来。
        语法：`<meta name="description" content="具体的网页说明">`

        ```html
        <!DOCTYPE html>
        <html>
        	<head>
        		<meta name="description" content="这是一个内容为诗词的网页" />
        		<title></title>
        	</head>
        	<body>	
        	</body>
        </html>
        ```

    - 添加作者信息

      - 在`<meta>`中添加网页制作者的姓名
        语法：`<meta name="author" content="作者的姓名">`

        ```html
        <!DOCTYPE html>
        <html>
        	<head>
        		<meta name="author" content="adins" />
        		<title></title>
        	</head>
        	<body>	
        	</body>
        </html>
        ```

    - 规定字符编码

      - charset属性规定HTML文档的字符编码。
        语法：`<meta charset="字符编码集">`

        ```html
        <!DOCTYPE html>
        <html>
        	<head>
        		<meta charset="UTF-8" />
        		<title></title>
        	</head>
        	<body>	
        	</body>
        </html>
        ```

    - 定时跳转

      - 使用`<meta>`标签可以使网页在一段时间后自动刷新，将http-equiv属性设置为refresh来实现自动刷新，content属性设置为更新时间。
        语法：`<meta http-equiv="refresh" content="跳转的时间; url=跳转到的地址">`
        刷新时间和链接地址之间用分号相隔。默认情况下，跳转以秒为单位。

        ```html
        <!DOCTYPE html>
        <html>
        	<head>
        		<meta http-equiv="refresh" content="5; url=target/index.html" />
        		<title></title>
        	</head>
        	<body>	
        	</body>
        </html>
        ```

- `<h1> - <h6>`
  - `<h1> - <h6>`标签被⽤来定义 HTML 标题。
  - ⽤标题来呈现⽂档结构是很重要的
    - `<h1`\> 定义重要等级最⾼的标题。`<h6>`定义重要等级最低的标题。
- `<p>`
  - 段落

- `<br>`

  - 插⼊⼀个简单的换⾏符
  - `<br>`标签是⼀个空标签，意味着它没有结束标签。

- `<a>`

  - 定义超链接

    ```html
    <p>
    	 Search
     	<a href=“http://www.google.com/”>Google</a> or our
     	<a href=“lectures.html”>Lecture Notes</a>
    </p>
    ```

  - <p>
    	 Search
     	<a href=“http://www.google.com/”>Google</a> or our
     	<a href=“lectures.html”>Lecture Notes</a
    </p>

  - `<a>`元素最重要的属性是 href 属性，它指定链接的⽬标。
  - 请使⽤ CSS 来改变链接的样式。

- 图像 `<img>`

  - `<img>` 是空标签，只包含属性，并且没有闭合标签

    ```html
    <img src="url" alt="some_text">
    ```

  - src 指 "source"。源属性的值是图像的 URL 地址。

  - alt 属性⽤来为图像定义⼀串预备的可替换的⽂本。

  - 通过在`<a>`标签中嵌套`<img>`标签，给图像添加到另⼀个⽂档的链接。

    ```html
    <a href=“http://theonering.net/”>
    	<img src="hh.jpg" alt=“some-text” width="304"height="228">
    </a>
    ```

  - 图像格式
    - GIF
      - 透明、⽆损、256
      - ⽤于动画
    - JPEG
      - 使⽤范围最⼴ 
      - 有损 
      - 背景图、轮播图或者商品的banner图
    - PNG
      - 真彩⾊和调⾊板、透明、⽆损 
      - ⽂件体积⼤ 
      - 颜⾊数少的单帧图像，图标，LOGO
    - webp
      - 有损、压缩率⾼，同时⽀持透明度和动画 
      - 浏览器兼容性
    - SVG
      - LOGO

- `<em> & <strong>`

  - em: 呈现为被强调的⽂本
  - strong: 定义重要的⽂本

  ```html
  <p>
   	HTML is <em>really</em>,
   	<strong>REALLY</strong> fun!
  </p>
  ```

  <p>
   	HTML is <em>really</em>,
   	<strong>REALLY</strong> fun!
  </p>

  - em vs. i, strong vs. b
    - `<i>`⽆强调或着重意味的斜体（italic），⽐如⽣物学名、术语、外来语（⽐如 「de facto」这样的英语⾥常⽤的拉丁语短语）
    - `<b>`\>⽆强调或着重意味的粗体（bold），⽐如⽂章摘要中的关键词、评测⽂章 中的产品名称、⽂章的导⾔……

- 嵌套的标签

  - 标签必须正确嵌套：结束标记必须与最近打开的标记匹配
  - 浏览器可能会正确地呈现它（错误的嵌套标签），但它是⽆效的XHTML

- `Table: <table> <tr> <td> <th> <caption>`

  ```html
  <table>
  	<caption>Smart Guys</caption>
  	<tr><th>name</th><th>gender</th></tr> 
      <tr><td>Bill</td><td>male</td></tr>
      <tr><td>Susan</td><td>female</td></tr>
  </table>
  ```

  <table>
  	<caption>Smart Guys</caption>
  	<tr><th>name</th><th>gender</th></tr> 
      <tr><td>Bill</td><td>male</td></tr>
      <tr><td>Susan</td><td>female</td></tr>
  </table>

  - 不要⽤于布局!
    - 结构混乱，不清晰 
    - css更强⼤，访问性更好，能在范围更⼴的设备上运作，如⼿机 
    - 机器难以理解，不利于SEO 
    - 基于css的布局⻚⾯⽐表单布局更⼩更简单\

- 块元素`<blockquote>`

  ```html
  <p>As Lincoln said in his famous Gettysburg Address:</p>
  <blockquote>
  <p>Fourscore and seven years ago, our fathers brought forth on this continent a new
  nation, conceived in liberty, and dedicated to the proposition that all men are created
  equal.</p>
  </blockquote>
  ```

  <p>As Lincoln said in his famous Gettysburg Address:</p>
  <blockquote>
  <p>Fourscore and seven years ago, our fathers brought forth on this continent a new
  nation, conceived in liberty, and dedicated to the proposition that all men are created
  equal.</p>
  </blockquote>

- 行内引用 `<q>`

  ```html
  <p>Quoth the Raven, <q>Nevermore.</q></p>
  ```

  <p>Quoth the Raven, <q>Nevermore.</q></p>

  - 为何不像下⾯的⽅式?

    - ```html
      <p>Quoth the Raven, "Nevermore."</p>
      ```

    - 不使⽤`""` 的原因是: 

      - XHTML不应该直接包含引号字符，应该写成转义`&quot;`
      - 使⽤`<q>`的话可以使⽤CSS样式

- HTML字符实体

  - HTML 中的预留字符必须被替换为字符实体

  - ⼀些在键盘上找不到的字符也可以使⽤字符实体来替换

    | character (s) | entity                          |
    | ------------- | ------------------------------- |
    | <>            | `&lt;` `&gt;`                   |
    | é è ñ         | `&eacute;` `&egrave;` `&ntilde` |
    | TM ©          | `&trade;` `&copy`               |
    | π **δ** ∆     | `&pi;` `&delta;` `&Delta;`      |
    | И             | `&#1048;`                       |
    | " &           | `&quot;` `&amp;`                |

  - 要在Web⻚⾯中显示链接⽂本，必须对其特殊字符进⾏如下所示的编码

    ```html
    &lt;p&gt; &lt;a href=&quot;http://google.com/search?
    q=marty&amp;ie=utf-8&amp;aq=t&quot;&gt; Search
    Google for Marty &lt;/a&gt; &lt;/p&gt; 
    ```

    &lt;p&gt; &lt;a href=&quot;http://google.com/search?q=marty&amp;ie=utf-8&amp;aq=t &quot;&gt; Search Google for Marty &lt;/a&gt; &lt;/p&gt; 

### 2.2 表单 Form

- `<form>`：HTML 表单⽤于收集⽤户的输⼊信息

- HTML 表单表示⽂档中的⼀个区域，此区域包含交互控件，将⽤户收集到的信息发送到 Web 服务器。

  - 基本语法:  `<form>...form elements...</form>` 
  - 表单元素允许用户在表单中输⼊内容，比如：文本域 （textarea）、下拉列表（select）、单选框（radiobuttons）、复选框（checkbox）等等
  - 包含提交按钮
  - 当用户单击确认按钮时，表单的内容会被传送到服务器。表单的动作属性 action 定义了服务端的⽂件名。

- 表单例子（必须将表单的控件包装在块元素中，比如div, fieldset等）

  ```html
  <form>
  	 <div class="form-group">
  		 <label for="inputEmail">Email</label>
   		 <input type="email" class="form-control" id="inputEmail" placeholder="Email">
   	 </div>
   	 <div class="form-group">
   		 <label for="inputPassword">Password</label>
  		 <input type="password" class="form-control" id="inputPassword" placeholder="Password">
  	 </div>
   	 <div class="checkbox">
  		 <label><input type="checkbox"> Remember me</label>
   	 </div>
   	 <button type="submit" class="btn">Login</button>
   </form>
  ```

  <form>
  	 <div class="form-group">
  		 <label for="inputEmail">Email</label>
   		 <input type="email" class="form-control" id="inputEmail" placeholder="Email">
   	 </div>
   	 <div class="form-group">
   		 <label for="inputPassword">Password</label>
  		 <input type="password" class="form-control" id="inputPwd" placeholder="Password">
  	 </div>
   	 <div class="checkbox">
  		 <label><input type="checkbox"> Remember me</label>
   	 </div>
   	 <button type="submit" class="btn">Login</button>
   </form>

- `<form>`标签

  [![zaQlEF.png](https://s1.ax1x.com/2022/11/28/zaQlEF.png)](https://imgse.com/i/zaQlEF)

  - 表单属性说明如何处理用户输⼊
    - action="url" (必须)
      - 指定单击Submit按钮时将数据发送到哪⾥
    - method="get" (缺省)
      - 将表单数据以名称/值对的形式附加到 URL 中
      - URL 的长度是有限的（大约 3000 字符）
      - 绝不要使⽤ GET 来发送敏感数据！（在 URL 中是可见的）
      - 对于用户希望加⼊书签的表单提交很有用 
      - GET 更适用于非安全数据，比如在 Google 中查询字符串
    - method="post"
      - 将表单数据附加到 HTTP 请求的 body 内（数据不显示在 URL 中）
      - 没有长度限制
      - 通过 POST 提交的表单不能加入书签

- `<input>`

  - `<input>`标签规定了用户可以在其中输⼊数据的输入字段。

  - `<input>`元素在`<form>`元素中使用，用来声明允许用户输入数据的 input 控件。

  - 输入字段可通过多种方式改变，取决于 type 属性。

    ```html
    <form action="demo_form.php">
     	First name: <input type="text" name="fname"><br>
        Last name: <input type="text" name="lname"><br>
     	<input type="submit" value="提交">
    </form>
    <!--点击"提交"按钮，表单数据将被发送到服务器上的“demo-form.php”。-->
    ```

    ```html
    <input type="text" name="firstname" />
    <input type="radio" name="sex" value="male" /> Male
    <input type="checkbox" name="bike" />
    <input type="password" name=“pwd">
    ```

  | [![zaKvLT.png](https://s1.ax1x.com/2022/11/28/zaKvLT.png)](https://imgse.com/i/zaKvLT) | [![zaMSwF.png](https://s1.ax1x.com/2022/11/28/zaMSwF.png)](https://imgse.com/i/zaMSwF) |
  | ------------------------------------------------------------ | ------------------------------------------------------------ |

### 2.3 Web Standards

- Web标准
  - 更严格和结构化的语言
  - 不同浏览器之间的兼容性更强 
  - 更有可能让页面在以后也能正确显示 
  - 可以与SVG(图形)、MathML、MusicML等其他XML数据进行交换。
- XHTML 1.0 vs HTML 4.01
  - 文档结构
    - XHTML DOCTYPE 是强制性的
    - `<html>`中的 XML namespace 属性是强制性的
    - `<html>`、`<head>`、`<title>`以及`<body>`也是强制性的
  - 元素语法
    - XHTML 元素必须正确嵌套 
    - XHTML 元素必须始终关闭 
    - XHTML 元素必须小写 
    - XHTML 文档必须有⼀个根元素
  - 属性语法
    - XHTML 属性必须使用小写 
    - XHTML 属性值必须用引号包围 
    - XHTML 属性最小化也是禁止的
