---
layout:     post
title:      Web前端-Lec05 CSS布局
subtitle:   Web前端笔记
date:       2023-04-17
author:     ukrys
header-img: img/post-bg-js-version.jpg
catalog: 	 true
tags:
    - Web
    - Notes
    - css
---

## Lecture5 CSS布局

### 5.1 盒模型

盒模型本质上是一个盒子，封装周围的HTML元素，它包括：边距，边框，填充，和实际内容。它允许我们在其它元素和周围元素边框之间的空间放置元素。

[![zNI6iT.png](https://s1.ax1x.com/2022/11/27/zNI6iT.png)](https://imgse.com/i/zNI6iT)

#### 5.1.1 元素的宽度和高度

- 元素的总宽度计算公式：
  - 总元素的宽度=宽度+左填充+右填充+左边框+右边框+左边距+右边距
- 元素的总高度计算公式：
  - 总元素的⾼度=⾼度+顶部填充+底部填充+上边框+下边框+上边距+下边距

#### 5.1.2 标准盒模型

​	标准盒模型又称W3C标准盒模型，其中标准盒模型的 width 等于 content 的宽度，标准盒模型的 height 等于 content 的高度。

​	标准盒大小计算公式：`width(content) + padding + border + margin`

​						[	![zNImGD.png](https://s1.ax1x.com/2022/11/27/zNImGD.png)](https://imgse.com/i/zNImGD)

#### 5.1.3 IE怪异盒模型

​	怪异盒模型又称IE盒子模型，其中怪异盒子模型的 width 等于 content + padding + border 的宽度，怪异盒子模型的 height 等于 content + padding + border 的高度。

​	怪异盒大小的计算公式：`width(content + padding + border) + margin`

​							[![zNI0Ln.png](https://s1.ax1x.com/2022/11/27/zNI0Ln.png)](https://imgse.com/i/zNI0Ln)

### 5.2 Position

​	定位的基本思想很简单，它允许你定义元素框相对于其正常位置应该出现的位置，或者相对于⽗元素、另⼀个元素甚⾄浏览器窗口本身的位置。这个功能⾮常强大，用户代理对CSS2中定位的⽀持远胜于对其它⽅⾯的⽀持。

- CSS position属性⽤于指定⼀个元素在⽂档中的定位⽅式

#### 5.2.1 static

- HTML 元素的默认值，即没有定位，遵循正常的文档流对象。

- 静态定位的元素不会受到 top, bottom, left, right影响。


#### 5.2.2 relative

- 相对定位元素的定位是相对其正常位置。

  ```css
  h2.pos_left
  {
      position:relative;
      left:-20px;
  }
  h2.pos_right
  {
      position:relative;
      left:20px;
  }
  /*
   *移动相对定位元素，但它原本所占的空间不会改变。
   *相对定位元素经常被用来作为绝对定位元素的容器块。
   */
  ```

#### 5.2.3 fixed

- 元素的位置相对于浏览器窗口是固定位置。

- 即使窗口是滚动的它也不会移动

  ```css
  p.pos_fixed
  {
      position:fixed;
      top:30px;
      right:5px;
  }
  /*
   *注意： Fixed 定位在 IE7 和 IE8 下需要描述 !DOCTYPE 才能支持。
   *Fixed定位使元素的位置与文档流无关，因此不占据空间。
   *Fixed定位的元素和其他元素重叠。
   */
  ```

#### 5.2.4 absolute

- 绝对定位的元素的位置相对于最近的已定位父元素，如果元素没有已定位的父元素，那么它的位置相对于`<html>`

  ```css
  h2
  {
      position:absolute;
      left:100px;
      top:150px;
  }
  /*
   *absolute 定位使元素的位置与文档流无关，因此不占据空间。
   *absolute 定位的元素和其他元素重叠。
   */
  ```

#### 5.2.5 sticky

- sticky 英文字面意思是粘，粘贴，所以可以把它称之为粘性定位。

  **position: sticky;** 基于用户的滚动位置来定位。

  粘性定位的元素是依赖于用户的滚动，在 **position:relative** 与 **position:fixed** 定位之间切换。

  它的行为就像 **position:relative;** 而当页面滚动超出目标区域时，它的表现就像 **position:fixed;**，它会固定在目标位置。

  元素定位表现为在跨越特定阈值前为相对定位，之后为固定定位。

  这个特定阈值指的是 top, right, bottom 或 left 之一，换言之，指定 top, right, bottom 或 left 四个阈值其中之一，才可使粘性定位生效。否则其行为与相对定位相同。

  ```css
  div.sticky {
      position: -webkit-sticky; /* Safari */
      position: sticky;
      top: 0;
      background-color: green;
      border: 2px solid #4CAF50;
  }
  /*
   *注意：Internet Explorer, Edge 15 及更早 IE 版本不支持 sticky 定位。 Safari 需要使用 -webkit- prefix。
   */
  ```

#### 5.2.6 重叠的元素

- 元素的定位与文档流无关，所以它们可以覆盖页面上的其它元素

- z-index属性指定了一个元素的堆叠顺序（哪个元素应该放在前面，或后面）

- 一个元素可以有正数或负数的堆叠顺序

  ```css
  img{
      position:absolute;
      left:0px;
      top:0px;
      z-index:-1;
  }
  /*
   *具有更高堆叠顺序的元素总是在较低的堆叠顺序元素的前面。
   *如果两个定位元素重叠，没有指定z - index，最后定位在HTML代码中的元素将被显示在最前面。
   */
  ```

### 5.3 页面正常流

#### 5.3.1 默认布局

- 默认的，**⼀个块级元素的内容宽度是其父元素的 100%，其高度与其内容高度⼀致**。内联元素的 height width 与内容⼀致。你⽆法设置内联元素的 height width —— 它们就那样置于块级元素的内容⾥。**如果你想控制内联元素的尺⼨，你需要为元素设置 display: block**; （或者，display: inline-block; inline-block 混合了 inline 和 block 的特性。)
- 正常布局流是⼀套在浏览器视口内放置、组织元素的系统。默认的，块级元素按块流向布置，即基于其⽗元素的书写顺序(默认值：horizontal-tb)。 每个块级元素会在上⼀个元素下⾯另起⼀⾏，它们会被设置好的 margin 分隔。以英语为例，或者其他的水平书写、⾃上⽽下模式⾥，块级元素被垂直组织的。
- 内联元素的表现有所不同 —— 它们不会另起⼀⾏；**只要在其父级块级元素的宽度内有⾜够的空间**，它们与其他内联元素、相邻的⽂本内容（或者被包裹的）被安排在同⼀⾏。如果空间不够，溢出的⽂本或元素将移到新的⼀⾏。
- 如果两个相邻的元素都设置了 margin 并且两个 margin 有重叠，那么更大的设置会被保留，小的则会消失 —— 这被称为**外边距叠加**。（只有垂直方向的外边距会发生外边距叠加。水平方向的外边距不存在叠加的情况。）
  - 只有普通文档流中块框的垂直外边距才会发生外边距合并。行内框、浮动框或绝对定位之间的外边距不会合并

| [![zNvlUH.png](https://s1.ax1x.com/2022/11/27/zNvlUH.png)](https://imgse.com/i/zNvlUH) | [![zNvKbD.png](https://s1.ax1x.com/2022/11/27/zNvKbD.png)](https://imgse.com/i/zNvKbD) |
| :----------------------------------------------------------: | :----------------------------------------------------------: |

| [![zNvwVg.png](https://s1.ax1x.com/2022/11/27/zNvwVg.png)](https://imgse.com/i/zNvwVg) | [![zNv0aQ.png](https://s1.ax1x.com/2022/11/27/zNv0aQ.png)](https://imgse.com/i/zNv0aQ) | [![zNvB5j.png](https://s1.ax1x.com/2022/11/27/zNvB5j.png)](https://imgse.com/i/zNvB5j) |
| :----------------------------------------------------------: | ------------------------------------------------------------ | ------------------------------------------------------------ |

#### 5.3.2 Float

- 浮动的框可以向左或向右移动，直到它的外边缘碰到包含框或另⼀个浮动框的边框为⽌。
- 由于浮动框不在⽂档的普通流中，所以⽂档的普通流中的块框表现得就像浮动框不存在⼀样。
- 所有主流浏览器都支持 float 属性。主要属性值为：left（左浮动）、none（不浮动）、right（右浮动）、inherit（继承父元素浮动）

| [![zNxgfA.png](https://s1.ax1x.com/2022/11/27/zNxgfA.png)](https://imgse.com/i/zNxgfA) | [![zNxWlt.png](https://s1.ax1x.com/2022/11/27/zNxWlt.png)](https://imgse.com/i/zNxWlt) | [![zNxf6P.png](https://s1.ax1x.com/2022/11/27/zNxf6P.png)](https://imgse.com/i/zNxf6P) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |

### 5.4 Formatting Context

- Formatting context 是 W3C CSS2.1 规范中的⼀个概念。它是⻚⾯中的⼀块渲染区域，并且有⼀套渲染规则，它决定了其⼦元素将如何定位，以及和其他元素的关系和相互作⽤。最常⻅的 Formatting context 有 Block fomatting context (简称BFC)和 Inline formatting context (简称IFC)。
- BFC是⼀个独⽴的布局环境，其中的元素布局是不受外界的影响，并且在⼀个BFC中，块盒与⾏盒（⾏盒由⼀⾏中所有的内联元素所组成）都会垂直的沿着其⽗元素的边框排列。

### 5.5 BFC

- 定义：BFC(Block formatting context)直译为"块级格式化上下⽂"。它是⼀个独立的渲染区域，只有Block level box参与， 它规定了内部的Block-level Box如何布局，并且与这个区域外部毫不相干。


#### 5.5.1 BFC的形成

下列方式会创建块格式化上下文：

- 根元素（`<html>`）
- 浮动元素（`float` 值不为 `none`）
- 绝对定位元素（`position` 值为 `absolute` 或 `fixed`）
- 行内块元素（`display` 值为 `inline-block`）
- 表格单元格（`display` 值为 `table-cell`，HTML 表格单元格默认值）
- 表格标题（`display` 值为 `table-caption`，HTML 表格标题默认值）
- 匿名表格单元格元素（`display` 值为 `table`、`table-row`、 `table-row-group`、`table-header-group`、`table-footergroup`（分别是 HTML table、tr、tbody、thead、tfoot 的默认值）或 inline-table）
- `overflow` 值不为 `visible`、`clip` 的块元素
- `display` 值为 `flow-root` 的元素
- `contain` 值为 `layout`、`content` 或 `paint` 的元素
- 弹性元素（`display` 值为 `flex` 或 `inline-flex` 元素的直接⼦元素），如果它们本身既不是 `flex`、`grid` 也不是 table 容器
- ⽹格元素（`display` 值为 `grid` 或 `inline-grid` 元素的直接⼦元素），如果它们本身既不是 `flex`、`grid` 也不是 table 容器
- 多列容器（`column-count` 或 `column-width` (en-US) 值不为 auto，包括column-count 为 1）
- `column-span` 值为 `all` 的元素始终会创建⼀个新的 BFC，即使该元素没有包裹在⼀个多列容器中 (规范变更, Chrome bug)

#### 5.5.2 BFC的布局规则

- 内部的Box会在垂直⽅向，⼀个接⼀个地放置。
- Box垂直⽅向的距离由margin决定。属于同⼀个BFC的两个相邻Box的margin会发⽣重叠。
- 每个盒⼦（块盒与⾏盒）的margin box的左边，与包含块 border box的左边相接触(对于从左往右的格式化，否则相 反)。即使存在浮动也是如此。
- BFC的区域不会与float box重叠。
- BFC就是页面上的⼀个隔离的独立容器，容器里面的子元素不会影响到外⾯的元素。反之也如此
- 计算BFC的⾼度时，浮动元素也参与计算。

#### 5.5.3 格式化上下文影响布局

- 通常，我们会为定位和清除浮动创建新的 BFC，⽽不是更改布局，因为它将：
  - 包含内部浮动 
  - 排除外部浮动 
  - 阻止外边距重叠

#### 5.5.4 高度塌陷

- 当⽗元素未设置⾼度时，所有⼦元素浮动后，造成子元素脱离文档流进而无法把父元素撑开，父元素⾼度为0 产生高度塌陷，称为⾼度塌陷问题。

  [![zNzl9A.png](https://s1.ax1x.com/2022/11/27/zNzl9A.png)](https://imgse.com/i/zNzl9A)

- （一些补充）

  -  [《CSS学习笔记》之display、浮动float，及其四种解决父级元素塌陷问题的方法](https://blog.csdn.net/weixin_45947938/article/details/122077798?spm=1001.2101.3001.6650.6&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EOPENSEARCH%7ERate-6-122077798-blog-127798764.pc_relevant_recovery_v2&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EOPENSEARCH%7ERate-6-122077798-blog-127798764.pc_relevant_recovery_v2&utm_relevant_index=7)

  - display 也是一种实现行内元素排列的方式，（但是我们很多情况都是用float）

    - block 块元素
    - inline 行内元素
    - inline-block 是块元素，但是可以内联，在一行
    - none

  - **display 方向不可以控制； float需要解决父级元素高度塌陷问题**

  - 解决高度塌陷问题

    - 增加父级元素的高度

      ```css
      #father{
      	border: 1px #000 solid;
      	height: 800px;
      }
      ```

    - 增加一个空的div标签，清楚浮动

      ```  css
      <div class="clear"></div>
      
      .clear{
      	clear: both;
      	margin: 0;
      	padding: 0;
      }
      /*
       * clear: right; 右侧不允许有浮动元素
       * clear: left;	 左侧不允许有浮动元素
       * clear: both;  两侧不允许有浮动元素
       * clear: none;
       */
      ```

    - overflow：在父级元素中增加属性

      ```css
      overflow: hidden;
      /* 触发了BFC机制，块级执行上下文，父级变为封闭的独立空间，子元素跑不出去 */
      ```

    - 添加伪类 `after` （没有副作用，推荐）

      ```css
      #father:after{
      	content: '';
      	display: block;
      	clear: both;
      }
      ```


### 5.6 IFC

#### 5.6.1 IFC的形成

​	当多个内联（块级）元素排列在⼀起的时候就会形成⼀个IFC，之间不能穿插有块级元素，否则会被切割成多个IFC（当IFC中有块级元素插入时，会产生两个匿名块将父元素分割开来，产生两个IFC）。

#### 5.6.2 IFC的影响

- IFC对布局产⽣的影响主要有以下三个方面：

  - ⼀个IFC内的元素都是水平排列的。

  - 横向的margin、border、padding属性对于这些元素都是有效的。

  - 垂直方向可以调整对齐方式(vertical-align)。

    ​				[![zUShdS.png](https://s1.ax1x.com/2022/11/27/zUShdS.png)](https://imgse.com/i/zUShdS)

#### 5.6.3 IFC的布局规则（补充）

- 子元素水平方向横向排列，并且垂直方向起点为元素顶部。
- 子元素**只会计算横向样式空间**，【padding、border、margin】，垂直方向样式空间不会被计算，【padding、border、margin】。
- 在垂直方向上，子元素会以不同形式来对齐（vertical-align）
- 能把在一行上的框都完全包含进去的一个矩形区域，被称为该行的行框（line box）。行框的宽度是由包含块（containing box）和与其中的浮动来决定。
- IFC中的“line box”一般左右边贴紧其包含块，但float元素会优先排列。
- IFC中的“line box”高度由 CSS 行高计算规则来确定，同个IFC下的多个line box高度可能会不同。
- 当 inline-level boxes的总宽度少于包含它们的line box时，其水平渲染规则由 text-align 属性值来决定。
- 当一个“inline box”超过父元素的宽度时，它会被分割成多个boxes，这些 boxes 分布在多个“line box”中。如果子元素未设置强制换行的情况下，“inline box”将不可被分割，将会溢出父元素。

```css
.warp { border: 1px solid red; display: inline-block; }
.text { margin: 20px; background: green; }

<div class="warp">
    <span class="text">文本一</span>
    <span class="text">文本二</span>
</div>

/*左右margin撑开，上下margin并未撑开，符合IFC规范，只计算横向样式控件，不计算纵向样式空间。*/
```

[![zUpPQ1.png](https://s1.ax1x.com/2022/11/27/zUpPQ1.png)](https://imgse.com/i/zUpPQ1)

```css
.warp { border: 1px solid red; width: 200px; text-align: center; }
.text { background: green; }

<div class="warp">
    <span class="text">文本一</span>
    <span class="text">文本二</span>
</div>

/*
 * 多个元素水平居中
 * 水平排列规则根据IFC容器的text-align值来排列，可以用来实现多个子元素的水平居中。
 */
```

[![zUpVoD.png](https://s1.ax1x.com/2022/11/27/zUpVoD.png)](https://imgse.com/i/zUpVoD)

```css
.warp { border: 1px solid red; width: 200px; }
.text { background: green; }
.f-l { float: left; }

<div class="warp">
    <span class="text">这是文本1</span>
    <span class="text">这是文本2</span>
    <span class="text f-l">这是文本3</span>
    <span class="text">这是文本4</span>
</div>

/*
 * float元素优先排列
 * IFC中具备float属性值的元素优先排列，在很多场景中用来在文章段落开头添加“tag”可以用到。
 */
```

[![zUpeFe.png](https://s1.ax1x.com/2022/11/27/zUpeFe.png)](https://imgse.com/i/zUpeFe)

### 5.7 复杂的div嵌套

- 代码复杂度高，网页加载速度慢

- | [![zUptYQ.png](https://s1.ax1x.com/2022/11/27/zUptYQ.png)](https://imgse.com/i/zUptYQ) | [![zUpNWj.png](https://s1.ax1x.com/2022/11/27/zUpNWj.png)](https://imgse.com/i/zUpNWj) |
  | ------------------------------------------------------------ | ------------------------------------------------------------ |

  

### 5.8 最佳可访问性和可读性

- 编码时保持良好的html源码顺序⾮常重要，原因： 
  - ⽹站技术故障时不能正确显示css样式，或移动和⽆线⽹络环境下， 带宽有限，导致浏览器中出现没有样式的HTML。 
  - 资源顺序对⽹站的可访问性起着重要作⽤，因为对于盲⼈⽤户，当代码有⼀定的逻辑顺序时，能够快速跳过⻚眉和导航区域，直达⻚⾯的 主要内容。 
  - 确保⽹站的主导航链接和主要⽹⻚内容在资源排序中排在最前⾯，这 样可以帮助搜索引擎优化。

​		[![zUpgfJ.png](https://s1.ax1x.com/2022/11/27/zUpgfJ.png)](https://imgse.com/i/zUpgfJ)

### 5.9 响应式Web设计 （Responsive Web Design）

- ⾃适应⽹⻚设计（英语：Responsive web design，通常缩 写为RWD）是⼀种⽹⻚设计⽅法，该设计可使⽹站在多种浏览设备（从桌⾯电脑显示器到移动电话或其他移动产品设 备）上阅读和导航，同时减少缩放、平移和滚动。

#### 5.9.1 响应式布局

- 曾经流⾏，不再是必不可少，原因 
  - 公司研发⼈员越来越充⾜，可以在pc端和移动端实现两套布局，分项⽬进⾏维护。
  - 响应式布局在适配上越来越简单。
- 仍有存在的价值：
  - 移动端碎⽚化的现象将会⽆限期存在 
  - 前端也必然进⼊物联⽹领域，任何设备界⾯的响应布局都将会成为关键挑战。
  - 响应式布局是CSS逐步发展中的⼀环，体现了CSS的灵活性。

#### 5.9.2 优缺点

- 优势：
  - ⽹站可⽤性得到提升，同时与移动优先设计以及内容策略能 够⾮常好的融合在⼀起。
  - 简化服务器端 
  - 更容易维护 
  - 只提供⼀个⼊⼝给搜索引擎 
  - 能够⽀持未知设备
- 缺点：
  - 性能
    - 兼容各种设备⼯作量⼤，效率低下 
    - 代码累赘，会出现隐藏⽆⽤的元素，加载时间加⻓
  - 限制应⽤的复杂性
    - 折衷性质的设计解决⽅案，多⽅⾯因素影响⽽达不到最佳效果
  - ⼀定程度上改变了⽹站原有的布局结构，会出现⽤户混淆的情况

#### 5.9.3 响应式网页设计

- 围绕着三个概念建⽴：
  - 流畅或灵活的⻚⾯布局，根据浏览器窗⼝⼤⼩成⽐例缩放。
  - 灵活、⽐例适中的图像和视听媒体。
  - 使⽤CSS3媒体查询（media query），确定浏览器屏幕的宽度并作出相应的调整。

##### 5.9.3.1 流式布局和比例度量

- ⻚⾯固定宽度布局：
  - ⼏年前流⾏ 
  - 复杂⻚⾯布局中，有助于⽤户更好地了解⻚⾯上的信息。 
  - 尺⼨固定，不能适应当今屏幕⼤⼩各异的互联⽹世界。
- 不设定为⼀个固定宽度

[![zU9k1s.png](https://s1.ax1x.com/2022/11/27/zU9k1s.png)](https://imgse.com/i/zU9k1s)

##### 5.9.3.2 流体表格（Fluid Grid）

- 流体表格将⻚⾯栅格化，使⽤em相对单位取代px绝对单位
- https://alistapart.com/article/fluidgrids/

[![zU9m7T.png](https://s1.ax1x.com/2022/11/27/zU9m7T.png)](https://imgse.com/i/zU9m7T)

##### 5.9.3.3 em排版尺寸

> https://www.cnblogs.com/kunmomo/p/11649893.html

- 单纯成⽐例的流式布局并不能完全解决屏幕尺⼨问题，因为 在⼩屏幕上⻚⾯布局可能会被压扁，⽽在⼤屏幕上会被拉伸变形。

- 使⽤em排版尺⼨就⾮常重要，原因：

  - 当设备屏幕上的排版太⼤或太⼩时，⽤户都可以很容易地进⾏调整，，这对于有视⼒障碍的⽤户来说是⼀个重要的可访问特性。
  - 在CSS控制下，相对类型的⼤⼩可以很容易地缩放，在`<html>`或`<body>`标签中使⽤font-size元素，就可以很容易地对整个⻚⾯排版尺⼨进⾏缩放。通过调整em的值，可以⽴刻放⼤或缩⼩⻚⾯上的所 有排版，这在响应式设计中是⼀种⾮常有⽤的功能，可以快速缩放⻚⾯排版，以轻松匹配整个屏幕尺⼨和分辨率。

- 使用em尺寸

  [![zU9UAO.png](https://s1.ax1x.com/2022/11/27/zU9UAO.png)](https://imgse.com/i/zU9UAO)

##### 5.9.3.4 HTML`<picture>`元素

- picture 元素允许我们在不同的设备上显示不同的图⽚，⼀般⽤于响应式。 

- HTML5 引⼊了 元素，该元素可以让图⽚资源的调整更加灵活。 

- `<picture>`元素零或多个`<source>`元素和⼀个`<img>`元素， 每个`<source>`元素匹配不同的设备并引⽤不同的图像源，如果没有匹配的，就选择`<img>`元素的 src 属性中的 url。

  ```css
  <picture>
   	<source media="(min-width: 650px)" srcset="demo1.jpg">
  	<source media="(min-width: 465px)" srcset="demo2.jpg">
   	<img src="img_girl.jpg">
  </picture>
  ```

##### 5.9.3.5 流体图片（Liquid Image）

- 图⽚是否传达了应该放在alt属性中的⽂本信息? 

  是否想要确保图像总是打印出来，因为没有它打印输出就没有意义或不完整?

  是否需要链接图⽚? 

- 如果以上任何⼀个问题的答案是肯定的，那么图像就是内容， 应该保存在(X)HTML中。

| [![zU9hCQ.png](https://s1.ax1x.com/2022/11/27/zU9hCQ.png)](https://imgse.com/i/zU9hCQ) | [![zU943j.png](https://s1.ax1x.com/2022/11/27/zU943j.png)](https://imgse.com/i/zU943j) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |

##### 5.9.3.6 CSS3 media query

- 有条件地检测⽤户显示屏的各个⽅⾯，然后根据这些条件有选择地加载出样式表，并提供最合适的布局、排版和图形。
- 媒体查询可⽤于检测很多事情 ：
  -  viewport(视窗) 的宽度与⾼度 
  - 设备的宽度与⾼度 
  - 朝向 (智能⼿机横屏，竖屏) 
  - DPI分辨率

#### 5.9.4 独特布局

- 响应式设计不仅仅是拉伸和缩⼩⻚⾯布局，⽽是要将内容和导航的独特布局以最好的⽅式显示到各种尺⼨的屏幕上。
- ⼤部分响应式设计会使⽤⾄少三种不同的布局样式表。

[![zUCk5D.png](https://s1.ax1x.com/2022/11/27/zUCk5D.png)](https://imgse.com/i/zUCk5D)

- 断点测量实例

[![zUCEPe.png](https://s1.ax1x.com/2022/11/27/zUCEPe.png)](https://imgse.com/i/zUCEPe)

- CSS3 media queries

[![zUCQVf.png](https://s1.ax1x.com/2022/11/27/zUCQVf.png)](https://imgse.com/i/zUCQVf)

### 5.10 移动优先

- 优先内容和功能
  - 优先显示最重要的内容和功能，如果空间允许，再逐步加⼊次要内容和功能。

[![zUCsG4.png](https://s1.ax1x.com/2022/11/27/zUCsG4.png)](https://imgse.com/i/zUCsG4)

- 移动优先的好处
  - 通⽤访问
    - 只要移动端做的好，即使⽤户使⽤的是旧版本浏览器、没有Javascript或者关闭了Javascript的浏览器，或为视⼒残障⼈⼠设计的读屏浏览器，也能看到⼀个拥有基本功能的⽹站。 
    - 移动优先是渐进将强理念的良好范例，所有⽤户都能访问核⼼内容和功能。不存在不能访问的情况。

> 渐进渐强基本理念是⾸先基于⼀个具有⼴泛兼容性的核心方案，创建⼀个基线版本，然后再根据可能⽤到的浏览器的特性，慢慢添加⼀些特性和功能。

- 最佳实践

  - 使⽤有效的，⼴泛⽀持的HTML5和CSS3来构建你的站点。 
  - 利⽤HTML5新语义元素和ARIA为内容添加意义、可访问性和搜索可⻅性。 
  - 在布局和排版中使⽤⽐例度量，如百分⽐和em。
  - 根据⽤户的需求、观看设备的可能范围以及特定内容的性质， 计算响应断点并使⽤媒体查询。
  - 使⽤移动优先的⽅法，建⽴最⼩和最基本的体验。
  - 根据屏幕空间、带宽和浏览器功能，逐步提升移动优先的体验。
  - 在研发周期中优先考虑浏览器因素，尽量避免使⽤复杂的、面向桌⾯的Photoshop排版和静态图形设计。花哨的静态设计模型是⼀种过时的思维⽅式，与现代web实现完全脱节。

  [![zUCTRH.png](https://s1.ax1x.com/2022/11/27/zUCTRH.png)](https://imgse.com/i/zUCTRH)

### 5.11 面包屑导航

- 面包屑导航的作用是告诉访问者他们在网站中的位置以及如何返回。

- 作用
  - 让⽤户了解当前所处位置，以及当前⻚⾯在整个⽹站中的位置。
  - 体现了⽹站的架构层级，能够帮助⽤户快速学习和了解⽹站内容和组织⽅式，从⽽形成很好 的位置感。
  - 提供返回各个层级的快速⼊⼝，⽅便⽤户操作。
  - Google已经将⾯包屑导航整合到搜索结果⾥⾯，因此优化⾯包屑导航每个层级的名称，多使⽤关键字，都可以实现SEO优化。⾯包屑路径，对于提⾼⽤户体验来说，是很有帮助的。
  - ⽅便⽤户，⾯包屑主要⽤于为⽤户提供导航⼀个⽹站的次要⽅法，通过为⼀个⼤型多级⽹站 的所有⻚⾯提供⾯包屑路径，⽤户可以更容易的定位到上⼀次⽬录，引导⽤户通⾏；
  - 减少返回到上⼀级⻚⾯的点击或操作，不⽤使⽤浏览器的“返回”按钮或⽹站的主要导航来返回到上⼀级⻚⾯；
  - 不⽤常常占⽤屏幕空间，因为它们通常是⽔平排列以及简单的样式，⾯包屑路径不会占⽤⻚⾯太多的空间。这样的好处是，从内容过载⽅⾯来说，他们⼏乎没有任何负⾯影响；
  - 降低跳出率，⾯包屑路径会是⼀个诱惑⾸次访问者在进⼊⼀个⻚⾯后去浏览这个⽹站的⾮常好的⽅法。⽐如说，⼀个⽤户通过⾕歌搜索到⼀个⻚⾯，然后看到⼀个⾯包屑路径，这将会诱使⽤户点击上⼀级⻚⾯去浏览感兴趣的相关主题。这样，从而，可以降低⽹站的总体跳出率。
  -  有利于百度蜘蛛对⽹站的抓取，蜘蛛直接沿着那个链⾛就可以了，很⽅便。
  - ⾯包屑有利于⽹站内链的建设，⽤⾯包屑⼤⼤增加了⽹站的内部连接，提⾼⽤户体验。
- 适用条件
  - 虽然眼下很多⽹站都流⾏使⽤⾯包屑导航，但是并不是所有 的⽹站都适⽤。符合下⾯两个条件的⽹站才适合使⽤⾯包屑导航。
    - 层级较深的⽹站，⾯包屑导航适合层级较深的⽹站，如果只有⼀级分类的话，通过主导航就可以起到快速定位的作⽤。⽐如“⾖瓣⽹”类型扁平构架的⽹站就没有使⽤⾯包屑导航。
    - 独⽴不交叉的⽹站结构，由于⾯包屑⽹站导航路径是线性结构的，因此⽹站内容必须划分的⾮常清晰，且不存在交叉；否则，⾯包屑导航的路径就不是唯⼀的，同⼀分类可能出现在不同的路径中，让⽤户感到困惑。