---
layout:     post
title:      Web前端-Lec07-2 JavaScript作用域与闭包
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

## Lecture7-2 Javascript作用域与闭包

 ### 7.4 JavaScript 作用域

- 作用域是当前的执行上下文，值（en-US）和表达式在其中“可见”或可被访问，即作用域指的是有权访问的变量集合
  - 如果一个变量（en-US）或表达式不在当前的作用域中，那么它是不可用的
  - 作用域也可以堆叠成层次结构，子作用域可以访问父作用域，反过来则不行
- JavaScript的作用域分以下三种：
  - 全局作用域：脚本模式运行所有代码的默认作用域
  - 模块作用域：模块模式中运行代码的作用域
  - 函数作用域：由函数创建的作用域
- 此外，（ES6）用`let`或`const`声明的变量属于额外的作用域：
  - 块级作用域：用一对花括号（一个代码块）创建出来的作用域

### 7.5 JavaScript 变量

- 在JavaScript中，对象和函数也是变量
- 作用域决定了从代码不同部分对变量、对象和函数的可访问性

#### 7.5.1 全局变量

- 在函数之外声明的变量，叫做全局变量，因为它可被当前文档中的任何其他代码所访问。

- 全局变量的作用域是全局的：网页的所有脚本和函数都能够访问它

  ```javascript
  /* Example */
  var carName = " Volvo";
  
  // code here can use carName
  
  function myFunction() {
      // code here can use carName
  }
  ```

- 自动全局：如果为尚未声明的变量赋值，此变量会自动成为全局变量

  ```javascript
  /* Example */
  /* 这段代码将声明一个全局变量 carName，即使在函数内进行了赋值 */
  
  // code here can use carName
  
  function myFunction() {
      carName = "Volvo";
      // code here can use carName
  }
  ```

#### 7.5.2 函数作用域

- 在函数内定义的变量不能在函数之外的任何地方访问，因为变量仅仅在该函数域的内部有定义。

- 相对应的，一个函数可以访问定义在其范围内的任何变量和函数

- 换言之，定义在全局域中的函数可以访问所有定义在全局域中的变量

- 在另一个函数中定义的函数也可以访问在其父函数中定义的所有变量和父函数有权访问的任何其他变量

  ``` javascript
  /* Example */
  
  // code here can not use carName
  
  function myFunction() {
      var carName = "Volvo";
      // code here can use carName
  }
  ```

#### 7.5.3 JavaScript 变量的有效期

- JavaScript变量的有效期始于其被创建时
  - 局部变量会在函数完成时被删除
  - 全局变量会在您关闭页面时被删除
- 函数参数：函数参数也是函数内的局部变量
- HTML中的全局变量
  - 通过JavaScript，全局作用域形成了完整的JavaScript环境
  - 在HTML中，全局作用域是window。所有全局变量均属于window对象。

| [![pSmLgPS.png](https://s1.ax1x.com/2023/01/11/pSmLgPS.png)](https://imgse.com/i/pSmLgPS)<br />result: 1, 2, 3 |
| ------------------------------------------------------------ |
| [![pSmLR2Q.png](https://s1.ax1x.com/2023/01/11/pSmLR2Q.png)](https://imgse.com/i/pSmLR2Q) <br />**result： 1, 1, 1** |
| [![pSmLWvj.png](https://s1.ax1x.com/2023/01/11/pSmLWvj.png)](https://imgse.com/i/pSmLWvj) |

### 7.6 JavaScript 闭包

- 给变量add分配一个自调用函数的返回值。

- 自调用函数只运行一次。它将计数器设置为零(0)，并返回一个函数表达式。

- 这样add就变成了一个函数。“奇妙的”部分是它可以访问父作用域中的计数器。

- 这称为JavaScript闭包。它使函数具有“私有”变量成为可能。

- 计数器受匿名函数作用域的保护，只能使用add函数进行更改。

- 闭包是可以访问父作用域的函数，即使父函数已经关闭。

  ```javascript
  /* Example */
  var add = ( function () {
      var counter = 0;
      return function () { 
          return counter += 1;
      }
  })();
  console.log(add());	// 1
  console.log(add()); // 2
  console.log(add()); // 3
  ```

#### 7.6.1 闭包的定义

- 闭包（closure）是一个函数以及其捆绑的周边环境状态（lexical environment， 词法环境）的引用的组合。换而言之，闭包让开发者可以从内部函数访问外部函数的作用域。在Javascript中，闭包会随着函数的创建而被同时创建。
  - 内部函数比它的外部函数具有更长的生命周期
- 闭包是引用了自由变量的函数
  - 自由变量是作用域可以导出到外部作用域的变量
    - 函数内部变量和函数参数都可以是自由变量
    - 函数参数不包含this和arguments

#### 7.6.2 词法作用域

- 词法（lexical）一词指的是，词法作用域根据源代码中声明变量的位置来确定该变量在何处可用。嵌套函数可访问声明于它们外部作用域的变量

  ```javascript
  function init() {
  	var name = "Mozilla"; // name 是⼀个被 init 创建的局部变量
  	function displayName() { // displayName() 是内部函数，⼀个闭包
  		alert(name); // 使⽤了⽗函数中声明的变量
  	}
   	displayName();
  }
  init();  // Mozilla
  ```

#### 7.6.3 闭包应用场景

- 闭包很有用，因为它允许将函数与其所操作的某些数据（环境）关联起来。这显然类似于面向对象编程。

  - 实现私有成员
  - 保护命名空间
  - 避免污染全局变量
  - 变量需要长期驻留在内存

  ```javascript
  function a(){
      var i = 0;
      function b(){
          alert(++i);
      }
      return b;
  }
  var c = a();
  c(); 	// 1
  ```

  ```javascript
  /* 用闭包模拟私有方法 */
  var Counter = (function() {
  	var privateCounter = 0;
  	function changeBy(val) {
      	privateCounter += val;
  	}
      return {
          increment: function() {
              changeBy(1);
          },
          decrement: function() {
              changeBy(-1);
          },
          value: function() {
              return privateCounter;
          }
      }
  })();
  console.log(Counter.value()); /* logs 0 */
  Counter.increment();
  Counter.increment();
  console.log(Counter.value()); /* logs 2 */
  Counter.decrement();
  console.log(Counter.value()); /* logs 1 */
  ```

### 7.7 作用域链

​	function对象同其他对象一样，拥有可以编程访问的属性，和一系列不能通过代码访问而仅供js引擎存取的内部属性，其中一个是`[[scope]]`，包含了一个函数被创建的作用域中对象的集合。称为作用域链（Scope chain）。决定了那些数据可以被函数访问。

| [![pSnkI4H.png](https://s1.ax1x.com/2023/01/11/pSnkI4H.png)](https://imgse.com/i/pSnkI4H) | 函数初始化时，会将自己的作用域链中放入全局变量               |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [![pSnkTCd.png](https://s1.ax1x.com/2023/01/11/pSnkTCd.png)](https://imgse.com/i/pSnkTCd) | **active object是活跃对象，是函数执行时创建的对象，然后scope chain类似于<br/>栈结构，函数执行前压入栈中，函数执行结束就从栈中弹出。函数访问属性的过程就<br/>是沿着scope chain从上往下一次查找。** |

#### 7.7.1 改变作用域链

- **作用域链和优化**

​	从上面的例子中，我们可以看出，访问全局作用域是最慢的，因为需要依次从上往下进行查找，应当尽可能少的使用全局变量，应该尽可能使用局部变量。如果在函数中，使用多次全局变量，我们可以将全局变量转化为局部变量，然后在使用局部变量。

```javascript
function changeColor(){
    document.getElementById("btnChange").onclick=function(){
        document.getElementById("targetCanvas").style.backgroundColor="red";
    };
}
//上面代码我们使用了两次document，但是document作为全局变量，此时我们应该将其转化为局部变量来使用,所以下面为转化后的代码。
function changeColor(){
    var doc=document;
    doc.getElementById("btnChange").onclick=function(){
        doc.getElementById("targetCanvas").style.backgroundColor="red";
    };
}
```

- **with**

​	不推荐使用with，在 ECMAScript 5 严格模式中该标签已被禁止。推荐的替代方案是声明一个临时变量来承载你所需要的属性。 

```javascript
// with语法的作用就是为了解决代码重写问题，是对象快捷书写方式，但是这么好的方式，为什么不大力推广使用呢？
// 因为性能存在一些问题。
function initUI(){
     with (document){ //avoid!
     	var bd = body,
     	links = getElementsByTagName("a"), // 这里使用with语法省略了document。
     	i= 0,
     	len = links.length;
     	while(i < len){
     		update(links[i++]);
     	}
     	getElementById("go-btn").onclick = function(){
     		start();
     	};
     	bd.className = "active";
     }
}
```

​	with传入的对象的属性放入最上层，剩余的都往下压，导致局部变量的访问代价增大，所以with的性能不好。

​			[![pSnESeK.png](https://s1.ax1x.com/2023/01/11/pSnESeK.png)](https://imgse.com/i/pSnESeK)

- **try-catch**

  ```javascript
  // 我们在使用try--catch时，当代码执行错误时，会执行catch函数，catch函数中参数是错误对象，就是这个错误对象，会放到作用域链的头部。
  // 但是try--catch我们在必要的使用得使用，我们可以这样解决。
  try{
      methodThatMightCauseAnError();
  }catch(ex){
      alert(ex.message); // 作用域链在此处改变
  }
  ```

  ```javascript
  // 解决方案：将catch错误处理交给另外一个函数进行处理
  try{
      methodThatMightCauseAnError();
  }catch(ex){
      handleError(ex); // 委托给处理器方法
  }
  ```

### 7.8 闭包、作用域和内存

```javascript
function assignEvents(){
    var id = "xdi9592";
    document.getElementById("save-btn").onclick = function(event){
        saveDocument(id);
    };
}
```

[![pSnEwY4.png](https://s1.ax1x.com/2023/01/11/pSnEwY4.png)](https://imgse.com/i/pSnEwY4)

[![pSnErlR.png](https://s1.ax1x.com/2023/01/11/pSnErlR.png)](https://imgse.com/i/pSnErlR)

### 7.9 提升（Hosting）

- 引擎会在解释JavaScript代码之前首先进行编译，编译过程中的一部分工作就是找到所有的声明，并用合适的作用域将他们关联起来，这也正是词法作用域的核心内容。
- JavaScript变量的另一个不同寻常的地方是，你可以先使用变量稍后再声明变量而不会引发异常。这一概念称为变量提升；Javascript变量感觉上是被“提升”或移到了函数或语句的最前面。
- 但是，提升后的变量将返回undefined值。因此在使用或引用某个变量之后进行声明和初始化操作，这个被提升的变量仍将返回undefined值。

> 由于存在变量提升，⼀个函数中所有的var语句应尽可能地放在接近函数顶部的地方。这个习惯将大大提升代码的清晰度。

```javascript
/*** 例子 1*/
console.log(x === undefined); 
var x = 3;
// result: true

/*** 例子 2*/
var myvar = "my value";
(function() {
	console.log(myvar); 
	var myvar = "local value";
})();
// result: undefined
// 在上面这段代码中有两个作用域，window全局作用域和fn函数作用域，在打印变量myvar时，会先在fn函数作用域里面查找，因为在执行fn函数时，在函数内部也会先进行变量提升，所以最终的打印结果为undefined。

/*** 例子 3*/
function a() {}
var a;
console.log(typeof a)
// result: function
function a() {}
var a = 1;
console.log(typeof a)
// result: number
console.log(typeof a)
function a() {}
var a = 1;
// result: function
// 函数提升优先级高于变量提升，且不会被同名变量声明时覆盖，但是会被同名变量赋值后覆盖。

/*** 例子 4*/
console.log(v1);
var v1 = 100;
function foo() {
    console.log(v1);
    var v1 = 200;
    console.log(v1);
}
foo();
console.log(v1);
// result: undefined, undefined, 200, 100
```

#### 7.9.1 let和const关键字

- ES6新增块级作用域。这个区块对这些变量从一开始就形成了封闭作用域，直到声明语句完成，这些变量才能被访问（获取或设置），否则会报错ReferenceError。

- 暂时性死区（英temporal dead zone，简TDZ），即代码块开始到变量声明语句完成之间的区域。

- 通过let声明的变量没有变量提升、拥有暂时性死区，作用于块级作用域：

  - 当进入变量的作用域（包围它的语法块），立即为它创建（绑定）存储空间，不会立即初始化，也不会被赋值
  - 访问（获取或设置）该变量会抛出异常 ReferenceError
  - 当执行到变量的声明语句时，如果变量定义了值则会被赋值，如果变量没有定义值，则被赋值为undefined

  ```javascript
  { 	// TDZ starts at beginning of scope
       console.log(bar); // undefined
       console.log(foo); // ReferenceError
       var bar = 1;
       let foo = 2; // End of TDZ (for foo)
  }
  ```

#### 7.9.2 temporal

- 使⽤术语“temporal”是因为区域取决于执行顺序（时间），而不是编写代码的顺序（位置）。例如，下面的代码会生效，是因为即使使用 let 变量的函数出现在变量声明之前，但函数的执 行是在暂时性死区的外面。

  ```javascript
  {
   // TDZ starts at beginning of scope
   const func = () => console.log(letVar); // OK
   // Within the TDZ letVar access throws `ReferenceError`
   let letVar = 3; // End of TDZ (for letVar)
   func(); // Called outside TDZ!
  }
  ```

#### 7.9.3 函数提升

- 对于函数来说，只有函数声明会被提升到顶部，而函数表达式不会被提升。

  ```javascript
  /* 函数声明 */
  foo(); // "bar"
  function foo() {
  	console.log("bar");
  }
  
  /* 函数表达式 */
  baz(); // 类型错误：baz 不是⼀个函数
  var baz = function() {
  	console.log("bar2");
  };
  ```

  ```javascript
  var name = "The Window";
  var object = {
  	name : "My Object",
  	getNameFunc : function(){
  		return function(){
  			return this.name;
  		};
  	}
  };
  alert(object.getNameFunc()()); // The Window
  /* 相当于
   * function(){return this.name;} 
   * 此时 fun中的this指向window
   */
  ```
  
  ```javascript
  var name = "The Window";
  var object = {
  	name : "My Object",
  	getNameFunc : function(){
  		var that = this;
  		return function(){
  			return that.name;
  		};
  	}
  };
  alert(object.getNameFunc()()); // My Object
  /*
   * 而这里因为有一个that，所以它需要依赖getNameFunc这个函数，就形成了一个闭包，局部变量会一直在内存中，that点的就是局部变量的值
  */
  ```
  
  