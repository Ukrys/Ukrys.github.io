---
layout:     post
title:      Web前端-Lec06 JavaScript
subtitle:   Web前端笔记
date:       2023-04-17
author:     ukrys
header-img: img/post-bg-js-version.jpg
catalog: 	 true
tags:
    - Web
    - Notes
    - js
---

## lecture6 JavaScript

### 6.1 客户端基础

#### 6.1.1 客户端脚本运行流程：

​	Web Browser发送请求 → Web Server执行脚本，生成相应HTML文件 → 传输回Web Browser → Web Browser 执行脚本

#### 6.1.2 客户端编程

- HTML适合于开发静态⻚⾯ 

  - 可以指定⽂本/图像布局，链接，… 

  - Web⻚⾯每次访问时看起来都是⼀样的 

  - 为了开发交互/响应式⻚⾯，必须以某种形式集成编程 

- 客户端编程 

  - 程序是⽤单独的编程(或脚本)语⾔编写的 
    - 例如，JavaScript, JScript, VBScript 
  - 程序被嵌⼊到Web⻚⾯的HTML中，使⽤(HTML)标记来标识程序组件 
    - 例如， `<script type="text/javascript"> … </script>`

  - 浏览器在加载⻚⾯时执⾏程序，将程序的动态输出与HTML的静态内容集成在⼀起 

  - 还允许⽤户(客户端)输⼊信息并对其进⾏处理,可在将输⼊提交到远程服 器之前对其进⾏验证

#### 6.1.3 客户端与服务器端编程

- 客户端脚本(JavaScript)的好处:
  - 可⽤性:可以修改⻚⾯⽽不必返回到服务器(更快的UI) 
  - 效率:可以在不等待服务器的情况下对⻚⾯进⾏⼩⽽快速的更改 
  - 事件驱动:可以响应⽤户操作，如点击和按键源代码 
  - 平台独⽴性:任何⽀持脚本的浏览器都可以解释代码
- 服务器端编程(例如PHP)的好处:
  - 安全性:可以访问服务器的私有数据;客户端看不到 
  - 兼容性:不受浏览器兼容性问题的影响 
  - 功能全:可以写⽂件，打开与服务器的连接，连接数据库，…

#### 6.1.4 常见脚本任务

- 向Web⻚⾯添加动态特性
  - 表单数据的验证(可能是最常⽤的应⽤程序) 
  - 图像翻转 
  - 时间敏感或随机⻚⾯元素 
  - 处理cookies
- 定义Web接⼝
  - 利⽤按钮，⽂本框，可点击的图像，提示等
- 客户端脚本的限制
  - 因为脚本代码嵌⼊在⻚⾯中，所以它对外界是可⻅的 
  - 出于安全原因，脚本所能做的事情是有限的 
    - 例如，⽆法访问客户端的硬盘驱动器 
  - 因为它们被设计为在任何机器平台上运⾏，所以脚本不包含特定于平台的命令 
  - 脚本语⾔功能不全 
    - 例如，JavaScript对象⾮常粗糙，不适合⼤型项⽬开发

### 6.2 JavaScript概述

#### 6.2.1 为何Javascript 

- 从“玩具”到流⾏
  - ⽹⻚（JS实现的网页弹窗恶意攻击）, **AJAX**（重要推动）, Web 2.0／3.0 
  - ⼤量web应⽤ 
  - APP 
  - 控制硬件，Arduino, Tessel, Espruino, NodeBots等，应⽤于嵌⼊ 式系统、IOT、机器⼈等领域. 
  - 桌⾯程序（Electron），SpaceX ⻰⻜船的触控 UI 基于 Chromium + JavaScript 技术栈开发，开放的 Web 技术就此成为 了⼈类⾸个应⽤到载⼈航天领域的 GUI 技术栈 
  - 服务端 
  - 命令⾏⼯具

- 阿特伍德定律
  - 任何可以⽤JavaScript来写的 应⽤ ，最终都将⽤JavaScript来写

#### 6.2.2 JavaScript的优势

- 性能
  - JIT
  - 垃圾收集和动态绑定的开销
- 对象
  - JavaScript使⽤原型继承模型。
- 语法
  - 对于任何有C家族语⾔使⽤经验的⼈来说很熟悉，⽐如c++、Java、c#和PHP。
- 一等函数
  - JavaScript中的⼏乎所有东⻄都是对象，包括函数。
- 事件
  - 在浏览器内部，⼀切都在⼀个事件循环中运⾏。
- 可重用性
  - 最可移植、可重⽤的代码 
  - JavaScript可以模块化和封装

#### 6.2.3 JavaScript概述

- JavaScript是⼀种脚本语⾔
- JavaScript程序由JavaScript解释器/引擎计算和执⾏
  - Rhino, SpiderMonkey, V8, Squirrelfish
- 主流⽤途和⽤法:
  - 在运⾏时公开应⽤程序的对象，⽤于定制/嵌⼊⽤户逻辑。 
  - 改进⽹站的⽤户界⾯ 
  - 让你的⽹站更容易浏览 
  - 在不重新加载⻚⾯的情况下替换⻚⾯上的图像 
  - 表单验证 
  - ⻚⾯修饰和特效 
  - 动态内容操作 
  - 新兴的Web 2.0:客户端功能在客户端实现 
  - 还有很多……

#### 6.2.4 JavaScript vs. Java

> 基本没有关系

- 解释的，不是编译的
- 更宽松的语法和规则
  - 更少、更“松散”的数据类型 
  - 变量不需要声明 
  - 错误通常是⽆声的(少数例外)
- 关键结构是函数⽽不是类
  - “⼀等”函数
- 包含在⽹⻚中，并与其HTML/CSS内容集成

#### 6.2.5 使用 `<script>`

- 为⽹⻚嵌⼊脚本:

  ```html
  <script>
  	script commands and comments
  </script>
  ```

- 访问外部的脚本:

  ```html
  <script src=“url”>
   	script commands and comments
  </script>
  ```

### 6.3 JavaScript基本语法

#### 6.3.1 语言基础

- JavaScript⼤⼩写敏感
  - HTML ⼤⼩写不敏感; onClick, ONCLICK, … are HTML
- **以回车或分号 (;)结束的语句**
  - x = x+1; same as x = x+1
  - 分号减少错误
    - 可以不加分号：除了最后一行 其他行都没有成为单独语句的可能
- JavaScript代码块
  - JavaScript 语句通过代码块的形式进⾏组合。
  -  块由左花括号开始，由右花括号结束。 
  - 块的作⽤是使语句序列⼀起执⾏。

#### 6.3.2 与Java的注释语法相同

```javascript
/* multi-line comment */
// single-line comment
```

#### 6.3.3 对象

- 对象是命名属性的集合
  - 简单视图:哈希表或关联数组
  - 可以通过⼀组名称:值对进⾏定义
    - objBob = {name: " Bob"， grade: 'A'， level: 3};
  - 新成员可以随时添加
    - objBob.fullname = 'Robert';
  - 可以有方法
- 数组、函数也是对象
  - 对象的属性可以是函数（=方法）

#### 6.3.4 变量与类型

- 变量
  - var, let, const(case sensitive)
  - Define implicitly by its first use, which must be an assignment
    - Implicit definition has global scope, even if it occurs in nested scope? 
- 类型没有指定，但JS确实有类型（“loosely typed”）
  - Number, Boolean, String, Array, Object, Function, Null, Undefined 
  - can find out a variable's type by calling typeof

```javascript
var name="Gates", age=60, job=“CEO";
var carname=“Benz”;
var carname;
```

#### 6.3.5 数值

- 数值在内部是通过双精度浮点型(64位)的形式表示的 (没有 int vs. double)
- 同样的运算符:+ - * / % ++ -- etc
- 优先级相似java 
- 许多运算符⾃动转换类型:
  - "2" * 3 is 6

```javascript
0.1 + 0.2
// 0.30000000000000004

/* reason: 
 *	0.1和0.2都是近似表示的，在他们相加的时候，两个近似值进行了计算，导致最后得到的值是
 *	0.30000000000000004
*/

/* solution:
 *	把计算数字 提升 10 的N次方倍再除以 10的N次方。一般都用 1000 就行了。-> 转换为整数
 *  (0.1*1000+0.2*1000)/1000==0.3
 */

0.1 + 0.2 + 0.3
// 0.6000000000000001
0.1 + (0.2 + 0.3)
// 0.6
0.1 + 0.3
// 0.4
```

- IEEE 754[![zY0Rns.png](https://s1.ax1x.com/2022/11/25/zY0Rns.png)](https://imgse.com/i/zY0Rns)

  - 通常推荐先将数字转换成整数。

  - ⽐较两个浮点数差值的绝对值，是否超过误差精度

    ```javascript
    function compareTwo(n1,n2) {
    	 return Math.abs( n1 - n2 ) < Number.EPSILON;
    }
    compareTwo(0.1+0.2, 0.3);
    ```


#### 6.3.6 String

- 转义：与Java中相同：`\' \" \& \n \t \\`

- 与数值和字符串之间转换：

```javascript
var x = 30;
var s1 = "" + x;					// "30"
var n1 = parseInt("10 oranges");	// 10
var n2 = parseFloat("hello");		// NaN
```

- 访问字符串的字符：

``` javascript
var firstLetter = s[0];				// fails in IE
var firstLetter = s.charAt(0);
var lastLetter = s.charAt(s,length-1);
```

​	[![zXYEbn.png](https://s1.ax1x.com/2022/12/22/zXYEbn.png)](https://imgse.com/i/zXYEbn)

#### 6.3.7 布尔式

- 任何值都可以用作布尔值

  - false: 0, -0, 0.0, NaN, "", null, undefined
  - true: anything else

- 将值显示转换为布尔值

  - var boolValue = Boolean(otherValue);
  - var boolValue = !!(otherValue);     // ! 表示非， !! 表示布尔值

- null, NaN, undefined

  - NaN

    - isNaN()
    - typeof(NaN)     -> 'number'
    - 比如字符串转换成数值失败时

  - undefined

  - null

    - typeof(null) -> object

  - (-)Infinity: 大到无法表示的值

    ```
    var x = 1000 / 0;
    isNaN(x);
    ```

    >isNaN：
    >
    >返回 true: NaN、对象（除包含单个数值的数组）、undefined、不能用Number()方法转为number类型的字符串
    >返回false: 数值、null、布尔值、能用Number()方法转为number类型的字符串、包含单个数值的数组
    >
    >例：isNaN([["1.5"]])=false; Number(true)=1; Number("0xabc")=false; Number("2.5e+7")=false

  - 例子：平常业务中比较建议尽量不要使⽤ == 和 !=。这两个比较的时候会做⼀些强制的类型转换，所以⽐较结果很可能有误。务必使用 \=== 和 !==。

    ```javascript
    undefined < null		// false
    undefined > null		// false
    undefined === null		// false
    NaN == NaN				// false NaN是唯一一个不等于自身的值
    NaN !== NaN				// true
    "11" < "2"				// true
    "2" < "5"				// true
    5 < "11"				// true
    ```

#### 6.3.8 Math对象

- methods: abs, ceil, cos, floor, log, max, min, pow, random, round, sin, sqrt, tan
- properties: E, PI

```javascript
var pi_value = Math.PI;
var sqrt_value = Math.sqrt(30);
```

#### 6.3.9 逻辑运算符

-  `> < >= <= && || ! == != === !==`

- 大多数逻辑运算符自动转换类型：
  - 5<"7" 为true 
  - 42 == 42.0 为 true 
  - "5.0" == 5 为 true
- `===` 与 `!==`是严格的相等检查，同时⽐较类型和值
  - "5.0" === 5 is false

#### 6.3.10 if/else 条件语句

- 结构与Java的if/else语句相同

- JavaScript几乎允许任何东西作为条件

  ```javascript
  if(condition){
      statements;
  }else if(condition){
      statements;
  }else {
      statements;
  }
  ```

#### 6.3.11 for循环

> https://blog.csdn.net/qq_45634593/article/details/116540699?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-116540699-blog-105421884.pc_relevant_3mothn_strategy_recovery&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-116540699-blog-105421884.pc_relevant_3mothn_strategy_recovery&utm_relevant_index=1

- for
- for-in
- for-of

```js
var x;
var txt="";
var person={fname:"Bill",lname:"Gates",age:56};
for (x in person){
 	txt=txt + person[x];
}
```

#### 6.3.12 while, do/while

- 同Java

- break和continue关键字也和Java中的一样

  ```javascript
  cars=["BMW","Volvo","Saab","Ford"];
  var i=0;
  while (cars[i]){
   	document.write(cars[i] + "<br>");
   	i++;
  }
  ```

#### 6.3.13 数组

- 两种方法初始化数组

- 长度属性（在添加元素时根据需要增长）

  ```javascript
  var empty=[];
  var mycars=new Array();
  mycars[0]="Saab"
  mycars[1]="Volvo"
  mycars[2]=“BMW"
  var misc=new Array(1.1,true,"BMW");
  ```

- Array方法

  - 数组可以实现多种数据结构: list, queue, stack, ...
  - 方法：concat, join, pop, push, reserve, shift, slice, sort, splice, toString, unshift
    - push and pop add / remove from back 
    - unshift and shift add / remove from front 
    - shift and pop return the element that is removed

  ```javascript
  var fruits = ["Banana", "Orange"];
  fruits.push("Apple");
  fruits.unshift("Mango");
  fruits.pop();
  fruits.shift();
  fruits.sort();
  alert(fruits);
  ```

#### 6.3.14 函数

```javascript
function functionName(parameters){
    codes;
}
```

- 声明可以出现在函数体中
  - Local variables, "inner" functions
  - =>
    - (arg1, arg2) => {// something here}
- 匿名函数
  - (function(x, y){return x+y})(2,3);
- 参数
  - 参数传递
    - 基本类型按值传递，对象按引用传递
  - 调用可以提供任意数量的实参
    - functionname.length : # of arguments in definition 
    - functionname.arguments.length : # args in call

### 6.4 DOM(Document Object Model)

- 当一个网页被加载时，浏览器会创建一个页面的文档对象模型（Document Object Model，DOM）

- HTML DOM模型被构造成一个对象树

  [![zXtfFx.png](https://s1.ax1x.com/2022/12/22/zXtfFx.png)](https://imgse.com/i/zXtfFx)

- 通过对象模型，Javascript获得了创建动态HTML所需的所有**功能**：
  - JavaScript可以更改⻚⾯中的所有HTML元素
  - JavaScript可以更改⻚⾯中的所有HTML属性
  - JavaScript可以更改⻚⾯中的所有CSS样式
  - JavaScript可以删除现有的HTML元素和属性
  - JavaScript可以添加新的HTML元素和属性
  - JavaScript可以对⻚⾯中所有现有的HTML事件做出反应
  - JavaScript可以在⻚⾯中创建新的HTML事件

- DOM是什么？
  - DOM是W3C（万维网联盟）标准
  - DOM定义了一个访问文档的标准：
    - W3C⽂档对象模型(DOM)是⼀个平台和语⾔⽆关的接⼝，它允许程序和脚本动态访问和更新⽂档的内容、结构和样式。
  - W3C DOM标准分为3个不同的部分:
    - 核⼼DOM——所有⽂档类型的标准模型 
    - XML DOM——XML⽂档的标准模型 
    - HTML DOM——HTML⽂档的标准模型

#### 6.4.1 HTML DOM

- HTML DOM是HTML的标准对象模型和编程接口。它定义了: 

  - HTML元素作为对象 
  - 所有HTML元素的属性 
  - 访问所有HTML元素的方法 
  - 所有HTML元素的事件

  换句话说：*HTML DOM是获取、更改、添加或删除 HTML元素的标准。*

- DOM编程接口
  - 可以使⽤JavaScript(以及其他编程语⾔)访问HTML DOM。
  - 在DOM中，所有HTML元素都定义为对象。
  - 编程接口是每个对象的属性和方法。 
  - 属性是可以获取或设置的值(如更改HTML元素的内容)。 
  - 方法是可以执行的操作(如添加或删除HTML元素)。

- DOM元素

  - 页面上的每个元素都有⼀个相应的DOM对象 
  - 使用objectName.attributeName访问/修改DOM对象的属性 
  - 事实上，浏览器在运行时将Web页面计算为相应的DOM对象

  ```html
  <script>
  	document.getElementById("demo").innerHTML = "Hello World!";
  </script>
  ```

- 查找HTML元素

  - 通过id查找HTML元素

    ```javascript
    var myElement = document.getElementById("intro"); 
    ```

  - 根据标记名查找HTML元素 

    ```javascript
    var x = document.getElementsByTagName("p"); 
    ```

  - 根据类名查找HTML元素

    ```javascript
    var x = document.getElementsByClassName("intro"); 
    ```

  - 通过CSS选择器查找HTML元素

    ```javascript
    var x = document.querySelectorAll("p.intro"); 
    ```

  - 通过HTML对象集合查找HTML元素

    ```javascript
    var x = document.forms["frm1"];
    ```

#### 6.4.2 Javascript HTML DOM 导航

- 页面的元素嵌套在对象的树状结构中——DOM树

  - DOM具有遍历该树的属性和方法

- DOM节点类型

  ```html
  <p>
      This is a paragraph of text with a 
      <a href="/path/page.html">link</a>
  </p>
  ```

- 每个节点都有nodeType（节点类型）、 nodeName（节点名称）、nodeValue（节点值）属性

- html DOM中常出现的类型：

  - Element(元素节点) 

  - Text(文本节点)

  - Attr(属性节点) 

  - Comment(注释节点) 

  - Document(文档节点) 

  - DocumentFragment(⽂档片段节点)

    | [![pSmnPpQ.png](https://s1.ax1x.com/2023/01/10/pSmnPpQ.png) | [![pSmuPUK.png](https://s1.ax1x.com/2023/01/10/pSmuPUK.png)](https://imgse.com/i/pSmuPUK) |
    | ----------------------------------------------------------- | ------------------------------------------------------------ |

- 遍历DOM树

  - 每个节点的DOM对象都有以下属性：

    | name(s)                      | description                               |
    | ---------------------------- | ----------------------------------------- |
    | firstChild, lastChild        | start/end of this node's list of children |
    | childNodes                   | array of all this node's children         |
    | nextSibling, previousSibling | neighboring nodes with the same parent    |
    | parentNode                   | the element that contains this node       |

  - 浏览器不兼容问题（IE很糟糕）

### 6.5 BOM(The Browser Object Model)

- 浏览器对象模型（Browser Object Model，简称 BOM）是 JavaScript 的组成部分之⼀，BOM 赋予了 JavaScript 程序与浏览器交互的能力。

- 每个浏览器的Javascript程序都可以引用以下全局对象：

  | name      | description                                        |
  | --------- | -------------------------------------------------- |
  | document  | current HTML page and its content                  |
  | history   | list of pages the user has visited                 |
  | location  | URL of the current HTML page                       |
  | navigator | info about the web browser you are using           |
  | screen    | info about the screen area occupied by the browser |
  | window    | the browser window                                 |

- window 对象

  - 所有浏览器都⽀持window对象。它表示浏览器的窗⼝ 

  - 所有JavaScript全局对象、函数和变量都⾃动成为窗口对象的成员 

  - 在客户端 JavaScript 中，Window 对象是全局对象， 所有的表达式都在当前的环境中计算。也就是说，要引用当前窗口根本不需要特殊的语法，可以把那个窗⼝的 属性作为全局变量来使用： 

    ```javascript
    window.document.getElementById("header");
    document.getElementById("header");
    ```

- document 对象

  - 每个载入浏览器的 HTML 文档都会成为 Document 对象 
  - Document 对象使我们可以从脚本中对 HTML 页面中的所有元素进行访问 
  - 提示：Document 对象是 Window 对象的⼀部分，可通过 window.document 属性对其进行访问
  - Document 对象是 HTML 文档的根节点 
  - 属性: anchors, body, cookie, domain, forms, images, links, referrer, title, URL 
  - 方法: getElementById getElementsByName getElementsByTagName close, open, write, writeln

- location 对象

  - Location 对象包含有关当前 URL 的信息。 

  - Location 对象是 Window 对象的⼀个部分，可通过 window.location 属性来访问。

  - 例子：

    ```javascript
    window.location.href // 设置或返回完整的 URL
    window.location.hostname // 设置或返回当前 URL 的主机名
    window.location.pathname // 设置或返回当前 URL 的路径部分
    window.location.protocol // 设置或返回当前 URL 的协议。
    /* http:// 或 https:// */
    window.location.assign() // 加载新的⽂档
    ```

- navigator 对象

  - window.navigator 对象包含有关浏览器的信息。 

  - 注释：没有应用于 navigator 对象的公开标准，不过所有浏览器都支持该对象。

  - 例子：

    ```javascript
    navigator.appName // 返回浏览器的名称
    navigator.onLine // 返回指明系统是否处于脱机模式的布尔值
    navigator.appCodeName // 返回浏览器的代码名
    navigator.platform // 返回运⾏浏览器的操作系统平台
    ```

    ```html
    <p id="demo"></p>
    <script>
    	document.getElementById("demo").innerHTML =
    		"Name is " + navigator.appName + ". Code name is " +	 					navigator.appCodeName;
    </script>
    ```

  - 注意：来自navigator对象的信息通常会产生误导，不应该用于检测浏览器版本，因为：
    - 不同的浏览器可以使⽤相同的名称 
    - 浏览器所有者可以更改浏览器数据 
    - ⼀些浏览器为了绕过站点测试⽽故意错误标识⾃身 
    - 浏览器不能报告比浏览器晚发布的新操作系统

- screen对象

  - window.screen对象包含有关客户端显示屏幕的信息 

  - 注释：没有应用于 screen 对象的公开标准，不过所有浏览器都支持该对象

  - 属性：

    ```javascript
    screen.width // 返回显示器屏幕的宽度
    screen.height // 返回显示屏幕的⾼度
    screen.availWidth // 返回显示屏幕的宽度 (除 Windows 任务栏之外)
    screen.availHeight // 返回显示屏幕的⾼度 (除 Windows 任务栏之外)
    screen.colorDepth // 返回⽬标设备或缓冲器上的调⾊板的⽐特深度
    screen.pixelDepth // 返回显示屏幕的颜⾊分辨率（⽐特每像素）
    ```

- history 对象

  - window.history对象包含用户（在浏览器窗⼝中）访问过的URL 

  - History 对象是 window 对象的⼀部分，可通过 window.history 属性对其进行访问。

  - 为了保护用户的隐私，对JavaScript访问该对象的方式有限制 

  - 注释：没有应用于 History 对象的公开标准，不过所有浏览器都支持该对象。

  - 方法：

    ```javascript
    history.back() // 加载 history 列表中的前⼀个 URL
    history.forward() // 加载 history 列表中的下⼀个 URL
    ```

- Cookies
  - Cookies可以让你在网页中存储用户信息 
  - cookie是存储在计算机上的小文本文件中的数据 
  - Cookies的发明是为了解决“如何记住用户信息”的问题: 
    - 当⼀个⽤户访问⼀个网页时，他的名字会被存储在⼀个cookie中。 下次⽤户访问该页面时，cookie就会“记住”他的名字。 
  - cookie以名称-值对的形式保存，例如 username=Tom 
  - 当浏览器从服务器请求⼀个网页时，属于该网页的 cookies被添加到请求中。通过这种方式，服务器获得必要的数据来“记住”关于用户的信息。

#### 6.5.1 用Javascript创建一个Cookie

- JavaScript 可以使用document.cookie属性来创建、读取和删除cookie

- 比如：

  ```javascript
  document.cookie="username=Tom";
  ```

- 还可以添加⼀个过期日期(以UTC时间表示)。缺省情况下，关闭浏览器时删除cookie:

  ```javascript
  document.cookie="username=Tom; expires=Thu, 18 Sep 2015 10:00:00 UTC";
  ```

- 通过路径参数，可以告诉浏览器cookie属于哪个路径。缺 省情况下，cookie属于当前页面。

  ```javascript
  document.cookie="username=Tom; expires=Thu, 18 Sep 2015 10:00:00 UTC; path=/";
  ```

#### 6.5.2 如何使用cookies

- 使用JavaScript读取⼀个cookie

  ```javascript
  var x = document.cookie;
  /*
   * Note document.cookie will return all cookies in one string much
   * like: cookie1=value1; cookie2=value2; cookie3=value3;
   */
  ```

- 使用JavaScript修改

  ```javascript
  document.cookie="username=Tom; expires=Thu, 18 Sep 2015 10:00:00 UTC; path=/";
  ```

- 用JavaScript删除Cookie，⾮常简单，只需将expires参数设置为⼀个过去的日期:

  ```javascript
  document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 UTC";
  // 注意，在删除cookie时不必指定cookie值
  ```

[![pSmMw3F.png](https://s1.ax1x.com/2023/01/10/pSmMw3F.png)](https://imgse.com/i/pSmMw3F)