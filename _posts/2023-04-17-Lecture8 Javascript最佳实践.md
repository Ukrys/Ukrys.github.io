---
layout:     post
title:      Web前端-Lec08 最佳实践
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

## Lecture8 Javascript最佳实践

### 避免全局变量

- 请尽量少地使用全局变量
- 它包括所有的数据类型、对象和函数
- 全局变量和函数可被其他脚本覆盖
- 请使用局部变量替代，并学习如何使用闭包

### 始终声明局部变量

- 所有在函数中使用的变量应该被声明为局部变量
- 局部变量必须通过var关键词来声明，否则它们将变成全局变量
- 严格模式不允许未声明的变量
  - “use strict”;

### 为什么使用严格模式

- 消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为
- 消除代码运行的一些不安全之处，保证代码运行的安全
- 提高编译器效率，增加运行速度
- 为未来新版本的Javascript做好铺垫

### 严格模式

- ES6的模块自动采用严格模式，不管模块头部有没有use strict；
- 严格模式有以下限制：
  - 变量必须声明后再使用
  - 函数的参数不能有同名属性，否则报错 
  - 不能使用with语句 
  - 不能对只读属性赋值，否则报错 
  - 不能使用前缀0表示八进制数，否则报错 
  - 不能删除不可删除的属性，否则报错 
  - 不能使用delete prop删除变量，会报错，只能删除属性delete global[prop] 
  - eval不会在它的外层作⽤域引⼊变量 
  - eval和arguments不能被重新赋值 
  - arguments不会自动反映函数参数的变化 
  - 不能使用arguments.callee 
  - 不能使用arguments.caller 
  - 禁止this指向全局对象 
  - 不能使⽤fn.caller和fn.arguments获取函数调⽤的堆栈 
  - 增加了保留字(比如protected,static和interface)

### 在顶部声明

- 一项好的编码习惯是把所有声明放在每段脚本或函数的顶部

- 这么做的好处是：

  - 获得更整洁的代码
  - 提供了查找局部变量的好位置
  - 更容易避免不需要的全局变量
  - 减少不需要的重新声明的可能性

  ```javascript
  // Declare at the beginning
  var firstName, lastName, price, discount, fullPrice;
  // Use later
  firstName = "John";
  lastName = "Doe";
  price = 19.90;
  discount = 0.10;
  fullPrice = price * 100 / discount;
  // This also goes for loop variables:
  // Declare at the beginning
  var i;
  // Use later
  for (i = 0; i < 5; i++) {
  ```

### 初始化变量

- 在您声明变量时对其进行初始化是个好习惯

- 这么做的好处是：

  - 更整洁的代码
  - 在单独的位置来初始化变量
  - 避免未定义值

  ```javascript
  // Declare and initiate at the beginning
  var firstName = "",
      lastName = "",
      price = 0,
      discount = 0,
      fullPrice = 0,
      myArray = [],
      myObject = {};
  ```

### 请不要声明数值、字符串或布尔对象

- 请始终将数值、字符串或布尔值视作原始值。而非对象。

- 如果把这些类型声明为对象，会拖慢执行速度，并产生讨厌的副作用：

  ```javascript
  // Example
  var x = "John";             
  var y = new String("John");
  (x === y) // is false because x is a string and y is an object.
  
  // Or even worse:
  // Example
  var x = new String("John");             
  var y = new String("John");
  (x == y) // is false because you cannot compare objects.
  ```

### 请勿使用new Object()

- 请使⽤ {} 来代替 new Object() 

- 请使⽤ "" 来代替 new String() 

- 请使⽤ 0 来代替 new Number() 

- 请使⽤ false 来代替 new Boolean() 

- 请使⽤ [] 来代替 new Array() 

- 请使⽤ /()/ 来代替 new RegExp() 

- 请使⽤ function (){}来代替 new Function()

  ```javascript
  /* Example */
  var x1 = {};           // new object
  var x2 = "";           // new primitive string
  var x3 = 0;            // new primitive number
  var x4 = false;        // new primitive boolean
  var x5 = [];           // new array object
  var x6 = /()/;         // new regexp object
  var x7 = function(){}; // new function object
  ```

### 意识到自动类型转换

- 请意识到数值会被意外转换为字符串或 NaN（Not a Number）。 

- JavaScript 属于松散类型。变量可包含不同的数据类型，并且变量能够改变其数据类型：

  ```javascript
  /* Example */
  var x = "Hello";     // typeof x is a string
  x = 5;               // changes typeof x to a number
  /* When doing mathematical operations, JavaScript can convert
  numbers to strings, Example: */
  var x = 5 + 7;       // x.valueOf() is 12, typeof x is a number
  var x = 5 + "7";     // x.valueOf() is 57, typeof x is a string
  var x = 5 - 7;       // x.valueOf() is -2, typeof x is a number
  var x = 5 - "7";     // x.valueOf() is -2, typeof x is a number
  var x = 5 - "x";     // x.valueOf() is NaN, typeof x is a number
  /* Subtracting a string from a string, does not generate an error but
  returns NaN (Not a Number), Example */
  "Hello" - "Dolly"    // returns NaN
  ```

### 使用 === 比较

-  `==` 比较运算符总是在比较之前进行类型转换（以匹配类型）

- `===` 运算符会强制对值和类型进行比较：

  ```javascript
  /* Example */
  0 == "";        // true
  1 == "1";       // true
  1 == true;      // true
  0 === "";       // false
  1 === "1";    // false
  1 === true;     // false
  ```

### 使用 Parameter Defaults

- 如果调用函数时缺少一个参数，那么这个确实参数的值会被设置为 undefined

- undefined 值会破坏您的代码。为参数设置默认值是一个好习惯

  ```javascript
  /* Example */
  function myFunction(x, y) {
      if (y === undefined) {
          y = 0;
      }
  }
  ```

### 用default来结束switch

- 请使用default来结束您的switch语句。即使您认为没有这个必要：

  ```javascript
  /* Example */
  switch (new Date().getDay()) {
      case 0:
        day = "Sunday";
          break;
     ……
      case 6:
        day = "Saturday";
          break;
      default:
          day = "Unknown";
  }
  ```

### 避免使用 eval()

- eval()函数用于将文本作为代码来允许。在几乎所有情况下，都没有必要使用它。
- 因为允许任意代码运行，它同时也意味着安全问题。

### “For in” Statements

- 遍历对象内的成员时，你也会得到方法函数。为了解决这个问题，应始终将你的代码包装在一个if语句中来过滤信息

  ```javascript
  for(key in object) {
  	if(object.hasOwnProperty(key) {
  		...then do something...
  	}
  }
  ```

### 减少循环中的活动

- 编程经常会用到循环

- 循环每迭代一次，循环中的每条语句，包括for语句，都会被执行

- 能够放在循环之外的语句或赋值会使循环运行得更快

  ```javascript
  // 差的代码：
   var i;
   for (i = 0; i < arr.length; i++) {
  // 更好的代码：
   var i;
   var l = arr.length;
   for (i = 0; i < l; i++) {
  ```

### Vanilla JS

- vanilla JS是史上最轻量跨平台前端框架。

- 使用方法：

  - 引入方式只需要在html中加入这行script

    ```javascript
    <script src="path/to/vanilla.js"></script>
    ```

  - 当部署在正式环境中，直接把html中的这段引用删去即可 —— 所有的浏览器都已经内置这个框架

- 通过ID获取元素

  | 框架         | 代码                                                    | 次数/秒    |
  | ------------ | ------------------------------------------------------- | ---------- |
  | vanillaJS    | document.getElementById('test-table')                   | 12,137,211 |
  | Dojo         | dojo.byId('test-table')                                 | 5,443,343  |
  | Prototype JS | $('test-table')                                         | 2,940,734  |
  | Ext JS       | delete Ext.elCache['test-table']; Ext.get('test-table') | 997,562    |
  | jQuery       | $jq('#test-table');                                     | 350,557    |
  | YUI          | YAHOO.util.Dom.get('test-table');                       | 326,534    |
  | MooTools     | document.id('test-table');                              | 78,802     |

- 通过tag获取元素

  | 框架         | 代码                                                         | 次数/秒   |
  | ------------ | ------------------------------------------------------------ | --------- |
  | vanillaJS    | document.getElementsByTagName("span");                       | 8,280,893 |
  | Prototype JS | Prototype.Selector.select('span', document);                 | 2,940,734 |
  | YUI          | YAHOO.util.Dom.getElementsBy(function(){return true;},'span'); | 48,545    |
  | Ext JS       | Ext.query('span');                                           | 46,915    |
  | jQuery       | $jq('span');                                                 | 19,449    |
  | Dojo         | dojo.query('span');                                          | 10,335    |
  | MooTools     | Slick.search(document, 'span', new Elements);                | 5,457     |

### JS框架的优点

- JS框架封装了复杂困难的代码; 
- JS框架能加快开发速度，更快完成项⽬; 
- JS框架让你更专注于产品内容的价值，而不是实现过程;
-  JS框架让合作更简单，大家都对基础代码有共同的理解; 
- JS框架还会强迫你练习，多实践，顺能生巧。

### JS框架的问题

- 每个项目的开发都会遇到框架文档没有说明的问题，这时候就要深入框架查找原因，这时候就需要对原生JavaScript的深度掌握。 
- 新框架频繁发布，更新快速，⼀旦确定了项目的技术栈，随着时间，如何升级更新是个问题。

[![pSnfAOO.png](https://s1.ax1x.com/2023/01/11/pSnfAOO.png)](https://imgse.com/i/pSnfAOO)

### 正则表达式

- 正则表达式是⽤于匹配字符串中字符组合的模式。

- 正则表达式是构成搜索模式（search pattern）的字符序列。

- 当您搜索文本中的数据时，您可使用搜索模式来描述您搜索的内容。

- 正则表达式可以是单字符，或者更复杂的模式。

- 正则表达式可用于执行所有类型的文本搜索和文本替换操作。

  ```javascript
  /*  /正则表达式主体/修饰符(可选)  */
  /*  /([\w\-]+\@[\w\-]+\.[\w\-]+)/  */
  var re = /ab+c/;
  ```

#### 使用简单模式

- 以`/`开始和结束
- 最简单的正则是子字符串匹配
- 下述正则表达式匹配任一包含“abc”的字符串：
  - YES： "abc", "abcdef", "defabc", ".=.abc.=.", ... 
  - NO："fedcba", "ab c", "PHP", ...

#### 匹配单个字符：.

- `.`匹配单个字符，除了换行和行结束符。
  - `/.oo.y/` 匹配 "Doocy", "goofy", "LooNy", ...
- 修饰符`i`执行对大小写不敏感的匹配。
  - `/mart/i` matches "Marty Stepp", "smart fellow", "WALMART", ...

#### 特殊字符：|，()，^，\

- `|` 选择匹配
  - `/abc|def|g/` 匹配 "abc", "def", or "g"
- `()` 子表达式：把一个表达式分割为几个子表达式是非常有用的。
  - `/(Homer|Marge) Simpson/` 匹配 "Homer Simpson" or "Marge Simpson"

- `^` 匹配输入的开始。如果多行标志被设置为true，那么也匹配换行符后紧跟的位置。
  - `/^A/` 并不会匹配”an A“中的‘A’，但是会匹配”An E“中的'A'
  
- `$` 匹配输入的结束。如果多行标志被设置为true，那么也匹配换行符前的位置。
  - `/t$/`并不会匹配”eater“中的‘t’，但是会匹配”eat“中的‘t’。
  
- `\` 转义
- 如果要匹配特殊字符：`/ \ $ . [ ] ( ) ^ * + ?`
  
- `/<br \/>/` 匹配`<br />`标记

#### 量词：`*，+，?`

- `*` 匹配0次或更多次
  - `/abc*/` 匹配 "ab", "abc", "abcc", "abccc", ... 
  - `/a(bc)*/` 匹配 "a", "abc", "abcbc", "abcbcbc", ... 
  - `/a.*a/` 匹配 "aa", "aba", "a8qa", "a!?_a", ...

- `+` 匹配1次或更多次
  - `/a(bc)+/` 匹配 "abc", "abcbc", "abcbcbc", ... 
  - `/Goo+gle/` 匹配 "Google", "Gooogle", "Goooogle", ...

- `?`匹配0次或1次
  - `/a(bc)?/` 匹配 "a" or "abc”

#### 更多量词：{min, max}

- `{min,max}`， 允许重复的次数，其中，“min”是0或⼀个正整数， “max”是⼀个正整数，而max > min，至少匹配“min”次，最多匹配 “max”次。
  - `"/a(bc){2,4}/"` matches "abcbc", "abcbcbc", or "abcbcbcbc"
- 省略形式
  - {2,} 匹配至少2次 
  - {,6} 匹配最多6次 
  - {3} 匹配正好3次

#### 字符集： []

- `[]`字符集。匹配任何一个包含的字符。
  - `/[bcd]art/`匹配包含"bart", "cart", and "dart" 的字符串
  - 等同于 `/(b|c|d)art/` 但更短。
- `[]`中，许多修饰符作为正常字符
  - `/what[!*?]*/` matches "what", "what!", "what?**!", "what??!", ... 

#### 字符范围：[start-end]

- 可以使用连字符来指定字符范围，但如果连字符显示为方括号中的第⼀个或最后⼀个字符，则它将被视为作为普通字符包含在字符集中的文字连字符。也可以在字符集中包含字符类。
  - `/[a-z]/`匹配任一小写字母
  - `/[a-zA-Z0-9]/` 匹配任一大小写字母和数字
- 起始`^`表示⼀个否定的或被补充的字符集。也就是说，它匹配任何没有包含在括号中的字符
  - `/[^abcd]/` 匹配除了 a, b, c, or d以外的字母
- 字符集中，`-`需要转义
  - `/[+\-]?[0-9]+/` 匹配 + 或 -, 随后⾄少⼀位数字

```
例：匹配评估分数 A, B+, or D- 的正则表达式？
	/[ABCDF][+\-]?/
```

#### 字符

- 特殊字符集：

  - `\d` 匹配任何数字（阿拉伯数字）。相当于`[0-9]`。

    `\D` 匹配任何非数字（阿拉伯数字）的字符。相当于`[^0-9]`。

  - `\w` 匹配基本拉丁字母中的任何字母数字字符，包括下划线。相当于`[A-Za-z0-9_]`。

    `\W` 匹配任何不是来自基本拉丁字母的单词字符。相当于`[^A-Za-z0-9_]`

  - `\s` 匹配一个空白字符，包括空格、制符表、换页符和换行符。

    `\S` 匹配一个非空白字符

  ```
  例：至少 $1000.00的正则表达式？
  	/\$[1-9]\d{3,}\.\d{2}/
  ```

#### Javascript 正则表达式的使用

- 在 JavaScript 中，正则表达式常用于两个字符串方法： `search()` 和 `replace()`。

  ```javascript
  var str = "Visit W3School";
  var n = str.search(/w3school/i);
  ```

- 在 JavaScript 中，RegExp 对象是带有预定义属性和方法的正则表达式对象。

- 使用test()，test() 方法是一个正则表达式方法。

  ```javascript
  var patt = /e/;
  patt.test("The best things in lifr are free!"); // true
  ```

- 使用exec()，用于检索字符串中的正则表达式的匹配。该函数返回一个数组，其中存放匹配的结果。如果未找到匹配，则返回值为null。

  ```javascript
  /e/.exec("The best things in life are free"); // e
  ```

#### Javascript RegExp 对象

```javascript
var patt = new RegExp(pattern, modifiers);
// 或者更简单的方式：
var patt = /pattern/modifiers;

// 等价
var re = new RegExp("\\w+");
var re = /\w+/;


var re = /\\/gm;
// 正则构造函数
var reg = new RegExp("\\\\","gm");
var foo = "abc\\123";	// foo的值为"abc\123"

console.log(re.test(foo)); // true
console.log(reg.test(foo));
```

#### 编写更好的函数

- Don't Repeat Yourself（DRY） 不重复造轮子：封装为函数，对象模块
- Do One Thing（DOT）一次只做一件事情：提升代码复用行易读与可调式性
- Keep It Simple Stupid（KISS）保持简单：技巧，高深晦涩，一行代码中安排多个原子性任务
- Less Is More 少即是多：易读，避免一次执行多个任务，函数内容尽可能精简，不贪多，代码量独立完成一个功能点，拆分多个子函数

#### 函数表达式

- 函数表达式的优点是可以像给变量赋值一样将函数赋给变量

- 可以依靠函数表达式可靠地遵循应用程序逻辑。例如，条件分支中按预期工作。

- 缺点是函数表达式创建匿名函数，除非显式提供名称。

  ```javascript
  var bar = function(){
      return arguments.callee;
  };
  bar(); // =>[Function](Note:It's anonymous)
  ```

#### 对象字面量

```javascript
var baz = {
    f: function(){
        return arguments.callee;
    }
};
baz.f(); // [Function](Note:Also anonymous)
```

- 优点：
  - 使用对象字面量对相关函数进行分组非常容易。代码更有条理，可读性更强。上下午中的代码更容易理解和维护。
  - 容易拆解和排列：如果模块变得太大，可以更容易地重新排列代码

#### Prototypes

- 原型对象为所有对象实例所共享，因此这些实例也共享了原型函数的成员。通过内部属性绑定到原型。

  ```javascript
  var book = {
      title: "High Performance JavaScript",
      publisher: "Yahoo!Press"
  }
  
  alert(book.toString()); // "[object Object]"
  ```

  [![pSuJlGR.png](https://s1.ax1x.com/2023/01/12/pSuJlGR.png)](https://imgse.com/i/pSuJlGR)

- 例子 — 原型链

  ``` javascript
  function Book(title, publisher){
   	this.title = title;
   	this.publisher = publisher;
  }
  Book.prototype.sayTitle = function(){
   	alert(this.title);
  };
  var book1 = new Book("High Performance JavaScript", "Yahoo!Press");
  var book2 = new Book("JavaScript: The Good Parts", "Yahoo!Press");
  alert(book1 instanceof Book); 		// true
  alert(book1 instanceof Object); 	// true
  book1.sayTitle(); 					// "High Performance JavaScript"
  alert(book1.toString()); 			// "[object Object]" 
  ```

  [![pSuJUde.png](https://s1.ax1x.com/2023/01/12/pSuJUde.png)](https://imgse.com/i/pSuJUde)

#### Class

```javascript
class Point{
    constructor(x, y){
        this.x = x;
        this.y = y;
    }
    // 注意函数构造的方式
    toString(){
        return '(' + this.x + ',' + this.y + ')'; 
    }
}
var p1 = new Point(5, 5);
p1.toString(); // "(5,5)"

typeof Point // function
p1.constructor === Point // true
```

#### extends

```javascript
class Square extends Point{
    constructor(x){
        super(x, x);
    }
    toString(){
        return super.toString() + 'Square!';
    }
}
var s1 = new Square(4);
s1.toString(); 			// "(4, 4)Square!"
s1 instanceof Point		// true
s1 instanceof Square	// true
```

#### \_\_proto\_\_

```javascript
Square.__proto__ === Point
// true
Square.prototype.__proto__ === Point.prototype
// true
```

#### super

```javascript
class A{
    constructor(a){
        this.x = a;
    }
}
A.prototype.y = 2;
class B extends A{
    constructor(a){
        super();
    }
    getY(){
        super(); // 报错
        return super.y;
    }
}
```

#### 原生构造函数的继承

```javascript
class MyArray extends Array{
    constructor(...args){
        super(...args);
    }
}

var arr = new MyArray();
arr[0] = 12;
arr.length; 	// 1

arr.length = 0;
arr[0]			// undefined
```

#### static

```javascript
class A{
    static add(x, y){
        return x + y;
    }
}
A.add(1, 2);
var a = new A();
a.add(); 		// error
class B extends A{}
B.add(2, 2);	// 4
```

#### this

- 在函数体中，非显式或隐式地简单调用函数时，在严格模式下，函数内的this会被绑定到undefined上，在非严格模式下则会被绑定到全局对象window/global上。
- 一般使用new方法调用构造函数时，构造函数内的this会被绑定到新创建的对象上。
- 一般通过call / apply / bind 方法显式调用函数时，函数体内的this会被绑定到指定参数的对象上。
- 一般通过上下文对象调用函数时，函数体内的this会被绑定到该对象上。
- 在箭头函数中，this的指向是由外层（函数或全局）作用域来决定的。

- 全局环境中的this

  - 在函数体中，非显式或隐式地简单调用函数时，在严格模式下，函数内的this会被绑定到undefined上，在非严格模式下则会被绑定到全局对象window/global上。

  ```javascript
  function f1(){
      console.log(this);
  }
  function f2(){
      "user strict";
      console.log(this);
  }
  
  f1();		// window
  f2();		// undefined
  ```

  ``` javascript
  var foo = {
      bar: 10,
      fn: function(){
          console.log(this);
          console.log(this.bar);
      }
  }
  var fn1 = foo.fn;
  fn1(); 		// window, undefined
  ```

- this指向最后调用它的对象

  ```javascript
  var foo = {
      bar: 10,
      fn: function(){
          console.log(this);
          console.log(this.bar);
      }
  }
  foo.fn();	// {bar: 10, fn: f}, 10
  ```

- 上下文对象调用中的this

  ```javascript
  var student = {
      name: 'Lucas',
      fn: function(){
          return this;
      }
  }
  console.log(student.fn() === student)	// true
  ```

  ```javascript
  var person = {
      name: 'Lucas',
      brother:{
          name: 'Mike',
          fn: function(){
              return this.name;
          }
      }
  }
  console.log(person.brother.fn());		// Mike
  ```

  ```javascript
  var o1 = {
       text: 'o1',
       fn: function() {
       	return this.text
  	 } 
  }
  var o2 = {
   	text: 'o2',
   	fn: function() {
   		return o1.fn()
   	} 
  }
  var o3 = {
   	text: 'o3',
   	fn: function() {
   		var fn = o1.fn
   		return fn()
  	} 
  }
  console.log(o1.fn())	// o1
  console.log(o2.fn())	// o1
  console.log(o3.fn())	// undefined
  ```

- 通过bind、call、apply改变this指向

  - 一般通过call/apply/bind方法显示调用函数时，函数体内的this会被绑定到指定参数的对象上。

  ```javascript
  const foo ={
      name: 'lucas',
      logName: function(){
          console.log(this.name)
      }
  }
  const bar = {
      name: 'mike'
  }
  console.log(foo.logName.call(bar))		// mike
  ```

- 构造函数和this

  ```javascript
  function Foo(){
      this.bar = "Lucas";
  }
  const instance = new Foo();
  console.log(instance.bar);		// Lucas
  ```

- 箭头函数中的this

  - 箭头函数使用this不适用以上标准规则，而是根据外层（函数或者全局）上下文来决定。

  ``` javascript
  const foo = {
      fn: function(){
          setTimeout(function(){
              console.log(this);
          })
      }
  }
  console.log(foo.fn());		// window
  ```

  ```javascript
  var foo = {
      fn: function(){
          setTimeout(() => {
              console.log(this);
          })
      }
  }
  console.log(foo.fn());		// {fn: f}
  ```

- this 优先级

  - 显示绑定：通过call、apply、bind、new
  - 隐式绑定：根据调用关系确定this指向

  ```javascript
  function foo(a) {
   	console.log(this.a) 
  }
  var obj1 = {
  	a: 1,
   	foo: foo 
  }
  var obj2 = {
  	a: 2,
   	foo: foo 
  }
  obj1.foo.call(obj2)		// 2
  obj2.foo.call(obj1)		// 1
  ```

  ```javascript
  function foo(a) {
   	this.a = a 
  }
  var obj1 = {}
  var bar = foo.bind(obj1)
  bar(2)
  console.log(obj1.a)		// 2
  ```
  
  ```javascript
  var baz = new bar(3)
  console.log(baz.a)		// 3
  ```
  
  ```javascript
  function foo() {
   	return a => {
   		console.log(this.a)
   	};
  }
  var obj1 = {
   	a: 2
  }
  var obj2 = {
   	a: 3
  }
  var bar = foo.call(obj1)		// 2
  console.log(bar.call(obj2))		// undefined

#### Babel

- Babel 是一个 JavaScript编译器

- Babel 是一个工具链，主要用于将 ECMAScript 2015+ 版本的代码转换为向后兼容的 JavaScript 语法，以便能够运行在当前和旧版本的浏览器或其他环境中。下面列出的是 Babel 能为你做的事情：

  - 语法转换 
  - 通过 Polyfill 方式在目标环境中添加缺失的特性 (通过 @babel/polyfill 模块) 
  - 源码转换 (codemods) ……

  ```javascript
  const sum = (a,b)=>a+b
  ```

  ```javascript
  "use strict";
  var sum = function sum(a, b) {
   	return a + b;
  };
  ```

  ```javascript
  for(let i=0;i<5;i++){} console.log(i);
  for(var i=0;i<5;i++){} console.log(i);
  ```

  ```javascript
  "use strict";
  for (var _i = 0; _i < 5; _i++) {}
  console.log(i);//undefined
  for (var i = 0; i < 5; i++) {}
  console.log(i);//5
  ```

  

