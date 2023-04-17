---
layout:     post
title:      Web前端-Lec07-1 JavaScript事件
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

## Lecture7-1 JavaScript 事件

 ### 7.1 Javascript 事件

#### 7.1.1 事件

- 事件和事件处理
  - 使Web应用程序的响应性、动态性和交互性更强
  - 通过回调编程
- Javascript事件
  - 允许脚本相应用户与网页上元素的交互
  - 是否可以启动对页面的修改

#### 7.1.2 事件驱动编程

- 事件驱动编程是⼀种编程范式，其中程序流由事件决定，诸如用户操作(鼠标点击、按键)、传感器输出或来⾃其他程序/线程的消息。
- 事件驱动编程是图形用户界面和其他应用程序(如JavaScript web应用程序)中使用的主要范式，这些应用程序以执行特定的操作来响应用户输入为中心。
- 在事件驱动的应用程序中，通常有⼀个主循环监听事件，然后在检测到其中⼀个事件时触发回调函数。
- 事件驱动程序可以用任何编程语言编写，尽管使用提供高级抽象的语⾔(如闭包)更容易完成此任务。

#### 7.1.3 事件处理程序

- 处理程序接收的输入的回调子例程(在Java和JavaScript中称为侦听器) 

- 当事件发生时调用的函数 

- 通常与XHTML元素相关联 

- 必须注册：也就是说，必须指定关联

- Javascript的用途

  - 事件处理程序可用于处理和验证用户输入、用户操作和浏览器操作:
    - 每次加载页面时应该做的事情<br>当页面关闭时应该做的事情<br>当用户单击按钮时应该执行的操作<br>当用户输入数据时应该验证的内容<br>还有更多……
  - 可以使用许多不同的方法让JavaScript处理事件:
    - HTML事件属性可以直接执行JavaScript代码<br>HTML事件属性可以调用JavaScript函数<br>可以将自己的事件处理函数分配给HTML元素<br>可以阻止事件的发送或处理<br>还有更多……

- 语法

  ```javascript
  element.addEventListener(event, function, useCapture);
  /*
   * 第⼀个参数是事件类型 (如"click" 或"mousedown").
   * 第⼆个参数是我们想在事件发⽣时调⽤的函数.
   * 第三个参数是⼀个布尔值，指定是使⽤事件冒泡还是使⽤事件捕获，是可选参数.
   */
  element.removeEventListener(event, function, useCapture);
  // removeEventListener()⽅法删除已由addEventListener()⽅法注册的事件处理程序
  ```

#### 7.1.4 观察者模式

- 观察者模式是⼀种软件设计模式，在这种模式中，⼀个称为主题的对象维护⼀个名为观察者的依赖项列表，通常通过调⽤它 们的⼀个⽅法⾃动通知其任何状态变化

- 主要用于实现分布式事件处理系统

- 观察者模式也是我们熟悉的模型-视图-控制器(MVC)体系结构模式中的关键部分。观察者模式在许多编程库和系统中实现， 包括几乎所有的GUI工具包。

- 发布者/订阅者模式的子集

  | [![pSm2i8K.png](https://s1.ax1x.com/2023/01/10/pSm2i8K.png)](https://imgse.com/i/pSm2i8K) |
  | ------------------------------------------------------------ |
  | [![pSm2FgO.png](https://s1.ax1x.com/2023/01/10/pSm2FgO.png)](https://imgse.com/i/pSm2FgO) |

- 特征

  - 好处：主题与观察者之间的抽象耦合；支持广播通信
  - 注意：观察者模式会导致内存泄漏，即所谓的失效侦听器问题

- 事件使得一个主题可能有多个观察者队列

  [![pSm22I1.png](https://s1.ax1x.com/2023/01/10/pSm22I1.png)](https://imgse.com/i/pSm22I1)

#### 7.1.5 用jQuery方式附加事件处理程序

```javascript
var hiddenBox = $( "#banner-message" );
$( "#button-container button" ).on( "click", function( event ) {
	hiddenBox.show();
});
```

### 7.2 事件类型

在 Web 中，事件在浏览器窗口中被触发并且通常被绑定到窗口内部的特定部分——可能是一个元素、⼀系列元素、被加载到这个窗口的 HTML 代码或者是整个浏览器窗口。举几个可能发生的不同事件：用户在某个元素上点击鼠标或悬停光标；用户在键盘中按下某个按键；用户调整浏览器的大小或者关闭浏览器窗口；⼀个网页停⽌加载；提交表单；播放、暂停、关闭视频；发生错误。

#### 7.2.1 DOM2 事件类型

- ⽤户界⾯（UI）事件:
  - DOMFocusIn, DOMFocusOut, DOMActivate
- ⿏标事件:
  - click, mousedown, mouseup, mouseover, mousemove, mouseout
- 键盘事件: (not in DOM 2, but will in DOM 3)
- 变动事件:
  - DOMSubtreeModified, DOMNodeInserted, ... 
- HTML事件:
  - load, unload, abort, error, select, change, submit, reset, focus, blur, resize, scroll

#### 7.2.2 HTML5 新事件

- audio, video
  - canplay, playing, suspend,……
- drag/drop
- history
- new form events
  - invalid
- offline,online……
- message

#### 7.2.3 触屏和移动设备事件

- 功能强⼤的移动设备，特别是带有触摸屏的移动设备被⼴泛采⽤，要求创建新的事件类别。
- 在许多情况下，触屏事件映射到传统事件类型，如单击和滚动。但并⾮所有触屏UI的交互都模仿⿏标，也不是所有的触摸都可以被视为⿏标事件。
  - gesturestart, gestureend

#### 7.2.4 事件对象

- 有时候在事件处理函数内部，您可能会看到⼀个固定指定名称的参数， 例如event，evt或简单的e。这被称为事件对象，它被自动传递给事件处理函数，以提供额外的功能和信息。事件对象具有以下属性/方法:

  [![pSmWg9x.png](https://s1.ax1x.com/2023/01/10/pSmWg9x.png)](https://imgse.com/i/pSmWg9x)

#### 7.2.5 鼠标事件

[![pSmWhuD.png](https://s1.ax1x.com/2023/01/10/pSmWhuD.png)](https://imgse.com/i/pSmWhuD)

### 7.3 事件处理模型

#### 7.3.1 DOM 0

- 此事件处理模型是由Netscape Navigator引⼊的，到2005年 仍然是跨浏览器最多的模型。有两种模型类型：

  - 内联模型:事件处理程序作为元素的属性添加。 
  - 传统模型:可以通过脚本添加/删除事件处理程序。与内联模型⼀样，每个事件只能注册⼀个事件处理程序。通过将处理程序名称分配给元素对象的事件属性来添加事件。要删除事件处理程序，只需将属性设置为null。

  ```html
  <p>Hey <a href="http://www.example.com" onclick="triggerAlert('Joe'); return
  false;">Joe</a> ! </p>
  <script>
   	function triggerAlert(name) {
   		window.alert("Hey " + name);
   	}
  </script>
  
  <script>
   var triggerAlert = function () {
       window.alert("Hey Joe”);};
   	// Assign an event handler
  	document.onclick = triggerAlert;
  	// Assign another event handler
  	window.onload = triggerAlert;
  	// Remove the event handler that was just assigned
  	window.onload = null;
  </script>
  ```

#### 7.3.2 事件处理阶段

- 在DOM兼容浏览器中，事件流分为3个阶段：

  - 捕获阶段：事件从Document节点自上而下向目标节点传播的阶段； 
  - 目标阶段：真正的目标节点正在处理事件的阶段； 
  - 冒泡阶段：事件从目标节点自下而上向Document节点传播的阶段。

- 在现代浏览器中，默认情况下，所有事件处理程序都在冒泡阶段进行注册。

  | DOM事件流<br>[![pSmfkvT.png](https://s1.ax1x.com/2023/01/10/pSmfkvT.png)](https://imgse.com/i/pSmfkvT) |
  | :----------------------------------------------------------: |

#### 7.3.3 事件流

- 每个事件都有⼀个目标节点，可以通过事件访问该目标

  ```javascript
  element.onclick = handle(e);
  function handler(e){
      if(!e) var e = window.event;
      // e refers to the event
      // see detail of event
      var original = e.eventTarget;
  }
  ```

- 每个事件都起源于浏览器，并传递给DOM

- 职责链模式

  ​											[![pSmfWin.png](https://s1.ax1x.com/2023/01/10/pSmfWin.png)](https://imgse.com/i/pSmfWin)

#### 7.3.4 DOM 2

[![pSmfyqg.png](https://s1.ax1x.com/2023/01/10/pSmfyqg.png)](https://imgse.com/i/pSmfyqg)

- 浏览器兼容性（表中的数字指定了完全支持这些方法的第一个浏览器版本）

[![pSmfgaj.png](https://s1.ax1x.com/2023/01/10/pSmfgaj.png)](https://imgse.com/i/pSmfgaj)

#### 7.3.5 阻止默认行为

- 停止事件的传播

  - event.stopPropagation()
  - cancelBubble = true  (IE某些版本)

- 禁止默认行为

  - event.preventDefault()

  ```javascript
  video.onclick = function(e) {
  	e.stopPropagation();
  	video.play();
  };
  ```

[![pSmh3Yn.png](https://s1.ax1x.com/2023/01/10/pSmh3Yn.png)](https://imgse.com/i/pSmh3Yn)

#### 7.3.6 Microsoft-specific 模型

- 微软直到Internet Explorer 8才遵循W3C模型，因为它自己的模型是在W3C标准批准之前创建的。Internet Explorer 9遵循DOM3 事件，Internet Explorer 11删除了对微软特定模型的⽀持。

  <table>
      <tr>
      	<th>Name</th>
          <th>Description</td>
          <th>Argument type</th>
          <th>Argument name</th>
      </tr>
      <tr>
  		<td rowspan="2">attachEvent</td>
          <td rowspan="2">Similar to W3C's addEventListener method.</td>
          <td>String</td>
          <td>sEvent</td>
  	</tr>
  	<tr>
  		<td>Pointer</td>
          <td>fpNotify</td>
  	</tr>
  	<tr>
  		<td rowspan="2">detachEvent</td>
          <td rowspan="2">Similar to W3C's removeEventListener method.</td>
          <td>String</td>
          <td>sEvent</td>
  	</tr>
  	<tr>
  		<td>Pointer</td>
          <td>fpNotify</td>
  	</tr>
  	<tr>
  		<td rowspan="2">fireEvent</td>
          <td rowspan="2">Similar to W3C's dispatchEvent method.</td>
          <td>String</td>
          <td>sEvent</td>
  	</tr>
  	<tr>
  		<td>Event</td>
          <td>oEventObject</td>
  	</tr>
  </table>

- IE曾经的特定操作
  - 为了防⽌事件冒泡，开发⼈员必须设置事件的cancelBubble属性。 
  - 为了防⽌事件的默认动作被调⽤，开发⼈员必须设置事件的 “returnValue”属性。
  - 避免使用！！

[![pSmhrf1.png](https://s1.ax1x.com/2023/01/11/pSmhrf1.png)](https://imgse.com/i/pSmhrf1)

#### 7.3.7 事件处理程序的绑定

- 内联

  ```html
  <a href="somewhere.html" onClick="myFunction()">
  ```

- 传统

  ```html
  element.onclick = myFunction;
  ```

- DOM 2

  ```html
  element.addEventListener(“click", myFunction);
  ```

- IE：（evil enough!）

  ```html
  element.attachEvent('onclick', myFunction);
  ```

- JQuery，Prorotype... and so on

  ```html
  jQuery.on()
  Event.observe('target', 'click', myFunction);
  ```

  

