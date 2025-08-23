# CSS

- **定义和作用**：

  **CSS（Cascading Style Sheets）** 是一种用来描述 HTML 或 XML（包括各种基于 XML 的语言，如 SVG、MathML 或 XHTML）文档的样式表语言。CSS 在 Web 开发中的作用是控制网页的外观和布局。

  - **样式和美化**：通过 CSS，开发者可以对 HTML 元素进行样式设计，如颜色、字体、边距、边框、背景等。
  - **布局和排版**：CSS 允许开发者实现复杂的网页布局，控制元素的位置和对齐方式。
  - **响应式设计**：通过 CSS 媒体查询，可以创建响应式网站，使其在不同设备和屏幕尺寸下都能有良好的显示效果。

- **基本语法**：

  CSS 由选择器和声明块组成。声明块包含一个或多个声明，每个声明由一个属性和值组成。

  **示例**：

  ```css
  selector {
    property: value;
  }
  ```

  **例子**：

  ```css
  body {
    background-color: #f0f0f0;
    font-family: Arial, sans-serif;
  }

  h1 {
    color: #333;
    text-align: center;
  }
  ```

- **选择器**：

  CSS 选择器用于选择要应用样式的 HTML 元素。常见的选择器有：

  - **元素选择器**：选择所有指定元素。

    ```css
    p {
      color: blue;
    }
    ```

  - **类选择器**：选择所有带有指定类的元素。

    ```css
    .classname {
      font-size: 14px;
    }
    ```

  - **ID 选择器**：选择带有指定 ID 的元素。

    ```css
    #idname {
      margin: 10px;
    }
    ```

  - **属性选择器**：选择具有指定属性的元素。

    ```css
    input[type="text"] {
      border: 1px solid #ccc;
    }
    ```

  - **伪类选择器**：选择特定状态的元素，如`:hover`、`:active`、`:focus`等。

    ```css
    a:hover {
      color: red;
    }
    ```

- **盒模型**：

  CSS 盒模型描述了元素的内容、内边距（padding）、边框（border）和外边距（margin）的组成方式。理解盒模型对布局和设计至关重要。

  - **内容（content）**：元素的实际内容显示区域。
  - **内边距（padding）**：围绕内容的内间距，透明。
  - **边框（border）**：围绕内边距的边框。
  - **外边距（margin）**：元素与其他元素之间的外间距，透明。

  **示例**：

  ```css
  div {
    width: 200px;
    padding: 10px;
    border: 5px solid black;
    margin: 20px;
  }
  ```

- **布局方式**：

  CSS 提供多种布局方式，用于实现复杂的网页布局。

  - **浮动布局（Float Layout）**：通过`float`属性实现。

    ```css
    .left {
      float: left;
    }
    .right {
      float: right;
    }
    ```

  - **弹性盒布局（Flexbox Layout）**：通过`display: flex`实现灵活的单行或多行布局。

    ```css
    .container {
      display: flex;
    }
    .item {
      flex: 1;
    }
    ```

  - **网格布局（Grid Layout）**：通过`display: grid`实现复杂的二维网格布局。

    ```css
    .grid-container {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 10px;
    }
    .grid-item {
      background-color: lightgray;
    }
    ```

  - **定位（Positioning）**：通过`position`属性控制元素的定位方式，如`static`、`relative`、`absolute`、`fixed`、`sticky`。

    ```css
    .absolute {
      position: absolute;
      top: 50px;
      left: 50px;
    }
    ```

- **响应式设计**：

  通过媒体查询（media queries），CSS 可以根据不同的屏幕尺寸和设备特性调整布局和样式。

  **示例**：

  ```css
  @media (max-width: 600px) {
    .container {
      flex-direction: column;
    }
  }
  ```

- **总结**：

  CSS 是 Web 开发中不可或缺的一部分，负责网页的样式和布局。通过选择器、盒模型、布局方式和响应式设计，开发者可以创建美观且功能丰富的网页。了解和掌握 CSS 的基本概念和用法，是前端开发者的重要技能。

  这样回答能够展示你对 CSS 的全面理解和应用能力，符合面试官对基础知识掌握的期望。

## 1. 盒子模型

在标准盒子模型中，一个盒子由以下几个部分组成：

- **Content（内容区）**：显示实际内容的区域，比如文本或图像。它的大小由 `width` 和 `height` 属性决定。

- **Padding（内边距）**：内容区与边框之间的空间。它是透明的，用来增加内容与边框之间的距离。可以通过 `padding` 属性设置四个方向的内边距。

- **Border（边框）**：围绕内容和内边距的边框。可以设置边框的宽度、样式和颜色。通过 `border` 属性进行设置。

- **Margin（外边距）**：边框与相邻元素之间的空间。它是透明的，用来控制元素与其他元素之间的距离。可以通过 `margin` 属性设置四个方向的外边距。

盒子模型的总宽度和高度可以通过以下公式计算：

```txt
  总宽度 = content width + padding-left + padding-right + border-left + border-right + margin-left + margin-right
  总高度 = content height + padding-top + padding-bottom + border-top + border-bottom + margin-top + margin-bottom
```

### 2. **IE 怪异盒子模型（有时称为 Quirks 模型）**

在 IE 的怪异盒子模型中，计算盒子的宽度和高度略有不同：

- **Content（内容区）**：与标准盒子模型相同。

- **Padding（内边距）**、**Border（边框）**、**Margin（外边距）**：在怪异盒子模型中，这些属性的计算方式有一些不同。

怪异盒子模型的宽度和高度计算公式如下：

```txt
总宽度 = width + padding-left + padding-right + border-left + border-right + margin-left + margin-right
总高度 = height + padding-top + padding-bottom + border-top + border-bottom + margin-top + margin-bottom
```

### 3. **盒子模型的影响**

- **CSS `box-sizing` 属性**：可以用来控制盒子模型的计算方式。常用的值有：
  - `content-box`：标准盒子模型（默认值）。
  - `border-box`：包含 padding 和 border 在内的宽度和高度计算，使得元素的总尺寸固定。

使用 `border-box` 可以更容易地控制元素的大小，因为它将 padding 和 border 包含在 `width` 和 `height` 内部。例如：

```css
/* 标准盒子模型 */
.box-standard {
  width: 200px;
  padding: 20px;
  border: 5px solid black;
  /* 内容区的实际宽度是 200px - 20px - 20px - 5px - 5px = 150px */
}

/* IE 怪异盒子模型 */
.box-ie {
  width: 200px;
  padding: 20px;
  border: 5px solid black;
  /* 内容区的实际宽度是 200px - 20px - 20px - 5px - 5px = 150px */
}

/* 使用 border-box */
.box-border-box {
  box-sizing: border-box;
  width: 200px;
  padding: 20px;
  border: 5px solid black;
  /* 内容区的实际宽度是 200px - 20px - 20px - 5px - 5px = 150px */
}
```

通过 `box-sizing: border-box`，你可以避免因 `padding` 和 `border` 导致的宽度和高度计算问题，使布局更加稳定。

## 2.选择器，优先级

优先级：A、B、C、D

A：内敛

B：ID 选择器

C：类选择器、伪类选择器、属性选择器

D：标签选择器、伪元素选择器

## 3.rem em px vh vw

## 4.隐藏页面的方式

在平常的样式排版中，我们经常遇到将某个模块隐藏的场景

通过 css 隐藏元素的方式有很多种，它们看起来实现的效果是一致的。

但实际上每一种方法都有一丝轻微的不同，这些不同决定了在一些特定场合下使用哪一种方法。

### 实现方式

通过 css 实现隐藏元素方法有如下：

- display:none

  - 设置元素的 diplay 为 none 是最常用的隐藏元素的方法

    ```css
    .hide {
      display: none;
    }
    ```

  - 将元素设置为 display:none 后，元素在页面上将彻底消失
  - 元素本身占有的空间就会被其他元素占有，也就是说他会导致浏览器的重排和重绘
  - 消失后，自身绑定的事件不会触发，也不会有过渡效果
  - 特定：元素不可见，不占据空间，无法响应点击事件

- visibility:hidden

  - 设置元素的 visibility 为 hidden 也是一种常用的隐藏元素的方法
  - 从页面上仅仅是隐藏该元素，DOM 结果均会存在，只是当时在一个不可见的状态，不会触发重排，但是会触发重绘

  ```css
  .hidden {
    visibility: hidden;
  }
  ```

  - 给人的效果是隐藏了，所以他自身的事件不会触发
  - 特点：元素不可见，占据页面空间，无法响应点击事件

- opacity:0

  - opacity 属性表示元素的透明度，将元素的透明度设置为 0 后，在我们用户眼中，元素也是隐藏的
  - 不会引发重排，一般情况下也会引发重绘

  > 如果利用 animation 动画，对 opacity 做变化（animation 会默认触发 CPU 加速），则会触发 GPU 层面的 composite，不会触发重绘。

  ```css
  .transparent {
    opacity: 0;
  }
  ```

  - 由于其仍然是存在于页面上的，所以他自身的事件仍然是可以触发的，但被他遮挡的元素是不能触发其事件的
  - 需要注意的是：其子元素不能设置 opacity 来达到显示的效果
  - 特点：改变元素透明度，元素不可见，占据页面空间，可以响应点击事件

- 设置 height、width 模型属性为 0

  - 将元素的 margin，border，padding，height 和 width 等影响元素盒模型的属性设置成为 0，如果元素内有子元素或内容，还应该设置其 overflow：hidden 来隐藏其子元素。

  ```css
  .hiddenBox {
    margin: 0;
    border: 0;
    padding: 0;
    height: 0;
    width: 0;
    overflow: hidden;
  }
  ```

  - 特点：元素不可见，不占据页面空间，无法响应点击事件。

- position:absolute

  ```css
  .hide {
    position: absolute;
    top: -9999px;
    left: -9999px;
  }
  ```

  - 特点：元素不可见，不影响页面布局。

- clip-path

  - 通过裁剪的形式。

  ```css
  .hide {
    clip-path: polygon(0px 0px, 0px 0px, 0px 0px, 0px 0px);
  }
  ```

  - 特点：元素不可见，占据页面空间，无法响应点击事件。

### 小结

最常用的还是 display:none 和 visibility:hidden，其他的方式只能认为是奇招，它们的真正用途并不是用于隐藏元素，所以并不推荐使用它们。

### 区别

关于 display:none、visibility:hidden、opacity:0 的区别，如下表所示：

|                        | display:none | visibility:hidden | opacity:0 |
| :--------------------: | :----------: | :---------------: | :-------: |
|         页面中         |    不存在    |       存在        |   存在    |
|          重排          |      会      |       不会        |   不会    |
|          重绘          |      会      |        会         |  不一定   |
|      自身绑定事件      |    不触发    |      不触发       |  可触发   |
|       transition       |    不支持    |       支持        |   支持    |
|      子元素可复原      |     不能     |        能         |   不能    |
| 被遮挡的元素可触发事件 |      能      |        能         |   不能    |

## 5.BFC

### 是什么？

我们在页面布局的时候，经常出现以下情况：

- 这个元素高度怎么没了？
- 这两栏布局怎么没法自适应？
- 这两个元素的间距怎么有点奇怪的样子？
- ......

原因是元素之间相互的影响，导致了意料之外的情况，这里就涉及到 BFC 概念

BFC（Block Formatting Context），即块级格式化上下文，它是页面中的一块渲染区域，并且有一套属于自己的渲染规则：

- 内部的盒子会在垂直方向上一个接一个的放置
- 对于同一个 BFC 的俩个相邻的盒子的 margin 会发生重叠，与方向无关。
- 每个元素的左外边距与包含块的左边界相接触（从左到右），即使浮动元素也是如此
- BFC 的区域不会与 float 的元素区域重叠
- 计算 BFC 的高度时，浮动子元素也参与计算
- BFC 就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素，反之亦然

BFC 目的是形成一个相对于外界完全独立的空间，让内部的子元素不会影响到外部的元素

### 里面的规则

触发 BFC 的条件包含不限于：

- 根元素，即 HTML 元素
- 浮动元素：float 值为 left、right
- overflow 值不为 visible，为 auto、scroll、hidden
- display 的值为 inline-block、inltable-cell、table-caption、table、inline-table、flex、inline-flex、grid、inline-grid
- position 的值为 absolute 或 fixed

### 可以用这个来干什么？

1. 实现两栏布局
2. 清除浮动
3. 边缘 margin 塌陷
4. 父元素失去高度

## 6.flex 布局

### 是什么

弹性盒模型，Flexible box(简称 flex)，可以简便、完整、响应式地完成页面

采用 flex 的元素称为父容器

### 属性

#### 父属性

- flex-direction 主轴方向
- flex-wrap 是否换行
- flex-flow 上面两个简写
- justify-content 主轴方向的对齐方式
- alain-items 交叉轴上的对齐方式
- alain-content 多根轴线的对齐方式

#### 子属性

- order 定义排列
- flex-grow 上面讲到当容器设为 flex-wrap: nowrap;不换行的时候，容器宽度有不够分的情况，弹性元素会根据 flex-grow 来决定
- flex-shrink 如果所有项目的 flex-shrink 属性都为 1，当空间不足时，都将等比例缩小如果一个项目的 flex-shrink 属性为 0，其他项目都为 1，则空间不足时，前者不缩小
- flex-basis 设置的是元素在主轴上的初始尺寸，所谓的初始尺寸就是元素在 flex-grow 和 flex-shrink 生效前的尺寸浏览器根据这个属性，计算主轴是否有多余空间，默认值为 auto，即项目的本来大小，如设置了 width 则元素尺寸由 width/height 决定（主轴方向），没有设置则由内容决定
- flex 属性是 flex-grow, flex-shrink 和 flex-basis 的简写，默认值为 0 1 auto，也是比较难懂的一个复合属性
  - flex: 1 = flex: 1 1 0%
  - flex: 2 = flex: 2 1 0%
  - flex: auto = flex: 1 1 auto
  - flex: none = flex: 0 0 auto，常用于固定尺寸不伸缩
- align-self
  允许单个项目有与其他项目不一样的对齐方式，可覆盖 align-items 属性，默认值为 auto，表示继承父元素的 align-items 属性，如果没有父元素，则等同于 stretch

### flex：1 完整写法？是什么意思？

`flex: 1;` 的完整写法是 `flex-grow: 1;`，它是 CSS 中用于设置 flex 容器内 flex 项目的放大比例的属性。

具体含义如下：

- `flex-grow` 属性指定了 flex 项目的放大比例，默认值为 0，表示不放大。
- 如果所有的 flex 项目的 `flex-grow` 值都为 1，则它们将等分剩余空间，即它们将在容器内平均分配可用空间。
- 如果一个 flex 项目的 `flex-grow` 值大于其他 flex 项目的 `flex-grow` 值，则它将占据更多的可用空间。
- 如果一个 flex 项目的 `flex-grow` 值为 0，则它不会占据剩余空间，即它不会增长。

因此，`flex: 1;` 等同于 `flex-grow: 1;`，表示该 flex 项目将等分剩余空间，即它会占据尽可能多的空间，以填满剩余空间。

## 7.回流重绘

### 7.1 是什么

在 HTML 中每个元素都可以被理解为盒子，在浏览器绘制页面的时候，就会涉及到回流与重绘：

- 回流：布局引擎会根据各种样式计算每个盒子在页面上的大小位置。
- 重绘：当计算好盒模型的位置、大小及其他属性后，浏览器会根据每个盒子特性进行绘制。

具体浏览器的渲染机制如下：

1. **解析 HTML 和 CSS**：浏览器首先会解析 HTML 生成 DOM 树，同时解析 CSS 生成 CSSOM 树。

2. **合成渲染树**：将 DOM 树和 CSSOM 树合并成为渲染树（Render Tree），这个过程中会忽略不需要渲染的内容，比如隐藏的元素或者不可见的元素。

3. **回流（Layout）**：根据渲染树，进行回流（也称为布局或重排），这个过程浏览器会计算每个节点在屏幕上的大小和位置，然后确定页面的几何布局。回流可能会影响到整个页面的布局，因为每个节点的位置和大小可能会相互影响。因此，回流是一项比较昂贵的操作，应该尽量避免多次触发。

4. **重绘（Repaint）**：在布局之后，浏览器会根据渲染树和回流得到的位置信息，进行绘制（Paint），得到元素的绝对像素。这个过程也称为重绘。与回流不同，重绘只涉及到页面的外观样式，不会影响布局。

5. **显示（Display）**：最后，浏览器会将绘制好的页面内容发送给 GPU（Graphics Processing Unit），由 GPU 进行渲染，最终显示在屏幕上。

需要注意的是，这个过程是一个渐进式的过程，并不是一次性完成的。浏览器在接收到 HTML 和 CSS 后会逐步完成这些步骤，同时也会优化渲染过程，尽量减少不必要的回流和重绘，以提高页面的渲染性能。

### 7.2 如何触发

#### 7.2.1 回流

- 元素大小、位置、内容发生变化
- 添加 DOM
- 浏览器的窗口尺寸
- 获取一些特定值：offsetTop、offsetLeft、offsetWidth、offsetHight、、、这些元素的共同特点就是需要时时获取

#### 7.2.2 重绘

- 颜色
- 方向
- 阴影

#### 7.2.3 如何避免

由于每次重排都会造成额外的计算消耗，因此大多数浏览器都会通过队列化修改并批量执行来优化重排过程。浏览器会将修改操作放入到队列里，直到过了一段时间或者操作达到了一个阈值，才清空队列

当你获取布局信息的操作的时候，会强制队列刷新，包括前面讲到的 offsetTop 等方法都会返回最新的数据

因此浏览器不得不清空队列，触发回流重绘来返回正确的值

- 应用元素的动画，使用 position 属性的 fixed 值或 absolute 值(如前文示例所提)
- 避免使用 table 布局，table 中每个元素的大小以及内容的改动，都会导致整个 table 的重新计算
- 对于那些复杂的动画，对其设置 position: fixed/absolute，尽可能地使元素脱离文档流，从而减少对其他元素的影响
- 使用 css3 硬件加速，可以让 transform、opacity、filters 这些动画不会引起回流重绘

## 8.css 的优化

### 8.1 前言

每一个网页都离不开 css，但是很多人又认为，css 主要是用来完成页面布局的，像一些细节或者优化，就不需要怎么考虑，实际上这种想法是不正确的

作为页面渲染和内容展现的重要环节，css 影响着用户对整个网站的第一体验

因此，在整个产品研发过程中，css 性能优化同样需要贯穿全程

### 8.2 实现方式

实现方式有很多种，主要有如下：

- 内联首屏关键 CSS
- 异步加载 CSS
- 资源压缩
- 合理使用选择器
- 减少使用昂贵的属性
- 不要使用@import

#### 内联首屏关键 CSS

在打开一个页面，页面首要内容出现在屏幕的时间影响着用户的体验，而通过内联 css 关键代码能够使浏览器在下载完 html 后就能立刻渲染

而如果外部引用 css 代码，在解析 html 结构过程中遇到外部 css 文件，才会开始下载 css 代码，再渲染

所以，CSS 内联使用使渲染时间提前

注意：但是较大的 css 代码并不合适内联（初始拥塞窗口、没有缓存），而其余代码则采取外部引用方式

#### 异步加载 CSS

在 CSS 文件请求、下载、解析完成之前，CSS 会阻塞渲染，浏览器将不会渲染任何已处理的内容

前面加载内联代码后，后面的外部引用 css 则没必要阻塞浏览器渲染。这时候就可以采取异步加载的方案，主要有如下：

- 使用 javascript 将 link 标签插到 head 标签最后

  ```js
  // 创建 link 标签 const myCSS = document.createElement( "link" ); myCSS.rel =
  "stylesheet";
  myCSS.href = "mystyles.css"; // 插入到 header 的最后位置
  document.head.insertBefore(
    myCSS,
    document.head.childNodes[document.head.childNodes.length - 1].nextSibling
  );
  ```

- 设置 link 标签 media 属性为 noexis，浏览器会认为当前样式表不适用当前类型，会在不阻塞页面渲染的情况下再进行下载。加载完成后，将 media 的值设为 screen 或 all，从而让浏览器开始解析 CSS

  ```html
  <link
    rel="stylesheet"
    href="mystyles.css"
    media="noexist"
    onload="this.media='all'"
  />
  ```

- 通过 rel 属性将 link 元素标记为 alternate 可选样式表，也能实现浏览器异步加载。同样别忘了加载完成之后，将 rel 设回 stylesheet

  ```html
  <link
    rel="alternate stylesheet"
    href="mystyles.css"
    onload="this.rel='stylesheet'"
  />
  ```

#### 资源压缩

利用 webpack、gulp/grunt、rollup 等模块化工具，将 css 代码进行压缩，使文件变小，大大降低了浏览器的加载时间

#### 合理使用选择器

css 匹配的规则是从右往左开始匹配，例如#markdown .content h3 匹配规则如下：

- 先找到 h3 标签元素
- 然后去除祖先不是.content 的元素
- 最后去除祖先不是#markdown 的元素
- 如果嵌套的层级更多，页面中的元素更多，那么匹配所要花费的时间代价自然更高

所以我们在编写选择器的时候，可以遵循以下规则：

- 不要嵌套使用过多复杂选择器，最好不要三层以上
- 使用 id 选择器就没必要再进行嵌套
- 通配符和属性选择器效率最低，避免使用

#### 减少使用昂贵的属性

在页面发生重绘的时候，昂贵属性如 box-shadow/border-radius/filter/透明度/:nth-child 等，会降低浏览器的渲染性能

#### 不要使用@import

css 样式文件有两种引入方式，一种是 link 元素，另一种是@import

@import 会影响浏览器的并行下载，使得页面在加载时增加额外的延迟，增添了额外的往返耗时

而且多个@import 可能会导致下载顺序紊乱

比如一个 css 文件 index.css 包含了以下内容：@import url("reset.css")

那么浏览器就必须先把 index.css 下载、解析和执行后，才下载、解析和执行第二个文件 reset.css

#### 其他

- 减少重排操作，以及减少不必要的重绘
- 了解哪些属性可以继承而来，避免对这些属性重复编写
- cssSprite，合成所有 icon 图片，用宽高加上 backgroud-position 的背景图方式显现出我们要的 icon 图，减少了 http 请求
- 把小的 icon 图片转成 base64 编码
- CSS3 动画或者过渡尽量使用 transform 和 opacity 来实现动画，不要使用 left 和 top 属性

## 9.两栏布局

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      .aside {
        width: 100px;
        height: 100px;
        background-color: green;
        float: left;
      }

      .content {
        background-color: red;
        /* margin-left: 100px; */
        /* padding-left: 100px; */
        /* overflow: auto; */
      }
    </style>
  </head>

  <body>
    <div class="container">
      <div class="aside"></div>
      <div class="content">
        内容内容内容内容内容内容内容内容内容内容内内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容
        内容内容内容内容内容内容内容内容内容内容内内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容
      </div>
    </div>
  </body>
</html>
```

## 10.三栏布局

```html

```

## 11.通过 link 进来的 css 会阻塞页面的渲染吗？js 会阻塞吗？如果会如何解决？

通过 `link` 标签引入的 CSS 和通过 `script` 标签引入的 JavaScript 都会阻塞页面的渲染，但它们的影响方式略有不同。

### CSS 的阻塞影响

- **阻塞渲染：** 浏览器会等待 CSS 文件下载、解析和应用到文档树之后，才会继续渲染页面。
- **不阻塞 DOM 树的构建：** HTML 的解析和 DOM 树的构建不会因为 CSS 的加载而受阻。

### JavaScript 的阻塞影响

- **阻塞渲染和 DOM 树构建：** 浏览器会在遇到 JavaScript 文件时停止解析 HTML，开始下载、解析和执行 JavaScript，然后才会继续构建 DOM 树和渲染页面。这会导致页面呈现延迟，用户可能会感觉到页面加载速度慢。
- **阻塞其后资源的下载：** 如果 JavaScript 文件的加载和执行时间较长，会延迟后续资源（如图片、样式表等）的下载和渲染。

### 解决方法

1. **使用 `defer` 属性：** 对于 JavaScript，可以在 `script` 标签中添加 `defer` 属性，使得脚本在 HTML 解析完成后才执行，从而不阻塞渲染。但需要注意，`defer` 属性只对外部脚本有效。

   ```html
   <script src="script.js" defer></script>
   ```

2. **使用 `async` 属性：** 类似于 `defer`，`async` 属性也用于异步加载脚本，但它在下载完成后立即执行，不会按照顺序执行。

   ```html
   <script src="script.js" async></script>
   ```

3. **优化资源加载顺序：** 将 CSS 文件放在 HTML 头部，JavaScript 文件放在 HTML 尾部，可以确保 CSS 在 JavaScript 之前加载和解析，以减少页面渲染的阻塞时间。
4. **使用代码拆分：** 对于大型的 JavaScript 文件，可以将其拆分成多个小文件，并在需要时按需加载，以减少初始加载时的压力。
5. **利用浏览器缓存：** 合理利用浏览器缓存，减少资源重复加载的次数，加快页面加载速度。

## 12.position

在 CSS 中，`position` 属性用于指定元素的定位方式。常见的 `position` 值包括：

1. `static`：默认值，元素遵循正常的文档流，并且不会被特殊地定位。

   - `top`、`right`、`bottom`、`left` 和 `z-index` 属性对 `static` 定位的元素不起作用。

2. `relative`：相对定位，元素相对于其正常位置进行定位，但不会影响其他元素的布局。

   - 可以使用 `top`、`right`、`bottom`、`left` 属性来指定相对偏移值。

3. `absolute`：绝对定位，元素相对于其第一个非 `static` 定位的父元素进行定位，如果没有这样的父元素，则相对于 `<html>` 元素。

   - 绝对定位的元素会脱离正常的文档流，不会影响其他元素的布局。可以使用 `top`、`right`、`bottom`、`left` 属性来指定绝对位置。

4. `fixed`：固定定位，元素相对于视口进行定位，即使页面滚动，元素也会保持固定位置不变。

   - 可以使用 `top`、`right`、`bottom`、`left` 属性来指定固定位置。

5. `sticky`：粘性定位，元素根据用户的滚动位置在 `relative` 和 `fixed` 之间切换定位。

   - 粘性定位的元素会在跨过指定的阈值之前保持 `relative` 定位，之后则变为 `fixed` 定位。可以使用 `top`、`right`、`bottom`、`left` 属性来指定粘性位置，还可以使用 `z-index` 属性指定元素的堆叠顺序。

这些 `position` 值可以与其他定位属性（如 `top`、`right`、`bottom`、`left` 和 `z-index`）结合使用，以实现更精确的定位效果。

### z-index

`z-index` 是 CSS 中用于控制元素堆叠顺序的属性，它决定了一个元素在堆叠上下文中的显示顺序。具体来说，`z-index` 属性的值越大，元素在堆叠顺序中就越靠前，越会出现在其他元素的上面。

#### 用法

1. **设置 `z-index` 值**：可以为元素设置一个整数值作为 `z-index` 的值，用来确定元素在堆叠顺序中的位置。

   ```css
   .element {
     z-index: 100;
   }
   ```

2. **相对定位元素**：对于使用相对定位的元素，`z-index` 可以用来控制相对于其它元素的堆叠顺序。

   ```css
   .element {
     position: relative;
     z-index: 10;
   }
   ```

3. **绝对定位元素**：对于使用绝对定位的元素，`z-index` 也可以用来控制其在堆叠顺序中的位置。

   ```css
   .element {
     position: absolute;
     z-index: 100;
   }
   ```

#### 注意事项

1. **只对定位元素生效**：`z-index` 只对设置了定位属性（如 `position: relative;`, `position: absolute;`, `position: fixed;`）的元素生效。

2. **父子关系影响**：`z-index` 只在同一堆叠上下文中生效，父元素的 `z-index` 值会影响子元素的堆叠顺序。

3. **堆叠上下文**：`z-index` 的表现受到堆叠上下文的影响，例如设置了 `transform` 或 `opacity` 的元素会创建新的堆叠上下文，会影响 `z-index` 的表现。

4. **数值范围**：`z-index` 的数值范围没有明确限制，但应当尽量避免使用过大的数值，以免造成混乱和不可预期的结果。

5. **块级元素和行内元素**：`z-index` 只对块级元素和相对定位的行内块元素生效，对于普通的行内元素是不生效的。

### float 和 postion 的区别

关于`float`和`position`的区别：

1. **float**：

   - 用于使元素浮动到指定的方向（左浮动或右浮动），并脱离文档流。
   - 浮动的元素会影响其后续元素的排列方式，其他元素会围绕浮动元素进行排列。
   - 浮动元素仍然占据文档流中的位置，但位置会根据浮动方向进行调整。
   - 常用于实现多栏布局、图像浮动等效果。

2. **position**：
   - 用于将元素定位到文档中的特定位置，可以与`top`、`right`、`bottom`、`left`属性配合使用。
   - 包括相对定位（`relative`）、绝对定位（`absolute`）和固定定位（`fixed`）三种方式。
   - 相对定位会相对于元素在文档流中的位置进行偏移，不会脱离文档流。
   - 绝对定位会相对于其最近的非静态定位的父元素进行定位，如果没有则相对于初始包含块进行定位，完全脱离文档流。
   - 固定定位会相对于浏览器窗口进行定位，固定在页面的指定位置，不会随页面滚动而变化。

## 13.css3 的新特性

- flexbox 布局
- grid 布局
- 响应式支持：媒体查询、弹性布局
- 过渡动画：通过 CSS3 的 transition 和 animation
- 边框和阴影效果
- 渐变效果
- 字体控制

## 14.transform 动画和直接进行使用 left、top 改变位置有什么不同

- 性能优化：
  - 使用 transform 进行动画通常会比直接改变位置的方式性能更好。因为 tansform 可以触发硬件加速，使得动画更加流畅，尤其在涉及大量元素的复杂动画时效果更明显
  - 直接改变位置的方式可能会引起浏览器的重排和重绘，性能较差
- 动画的应用范围：
  - transform 不仅可以用于改变位置，还可以用于旋转、缩放、倾斜等变换效果，因此更加灵活，适用范围更广
  - 直接改变位置只能实现位置的移动，缺少其他变化效果
- 对布局的影响：
  - 使用 transform 进行动画不会改变元素的布局流，即不会影响其他元素的位置和尺寸，只是在视觉上对元素进行变换
  - 直接改变位置可能会影响元素的布局，可能会导致其他元素的位置发生变化。
- 坐标系统的变化：
  - 使用 transform 改变元素的位置时，元素的定位是相对于自身的原点进行的，而不是相对于父元素或文档的原点
  - 直接改变元素位置是相对于父元素或文档进行的

## 15.什么是响应式设计？响应式设计的基本原理是什么？如何做？

根据用户的行为、以及设备环境（系统平台、屏幕尺寸、屏幕定向等）进行响应的调整和响应。

### 实现方式

响应式设计的基本原理是通过媒体查询检测不同的设备屏幕尺寸做处理，为了处理移动端，页面头部必须有 meta 声明 viewport。

## 16.元素水平垂直居中的方法有哪些？

### 16.1 背景

在开发中经常遇到这个问题，即让某个元素的内容在水平和垂直方向上都居中，内容不仅限于文字，可能是图片或其他元素

居中是一个非常基础但又是非常重要的应用场景，实现居中的方法存在很多，可以将这些方法分成两个大类：

居中元素（子元素）的宽高已知
居中元素宽高未知

### 16.2 实现方式

实现元素水平垂直居中的方式：

- 利用定位+margin:auto
- 利用定位+margin:负值
- 利用定位+transform
- table 布局
- flex 布局
- grid 布局

#### 利用定位+margin:auto

先上代码：

```html
<style>
  .father {
    width: 500px;
    height: 300px;
    border: 1px solid #0a3b98;
    position: relative;
  }
  .son {
    width: 100px;
    height: 40px;
    background: #f0a238;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    margin: auto;
  }
</style>
<div class="father">
  <div class="son"></div>
</div>
```

父级设置为相对定位，子级绝对定位 ，并且四个定位属性的值都设置了 0，那么这时候如果子级没有设置宽高，则会被拉开到和父级一样宽高

这里子元素设置了宽高，所以宽高会按照我们的设置来显示，但是实际上子级的虚拟占位已经撑满了整个父级，这时候再给它一个 margin：auto 它就可以上下左右都居中了

#### 利用定位+margin:负值

绝大多数情况下，设置父元素为相对定位， 子元素移动自身 50%实现水平垂直居中

```html
<style>
  .father {
    position: relative;
    width: 200px;
    height: 200px;
    background: skyblue;
  }
  .son {
    position: absolute;
    top: 50%;
    left: 50%;
    margin-left: -50px;
    margin-top: -50px;
    width: 100px;
    height: 100px;
    background: red;
  }
</style>
<div class="father">
  <div class="son"></div>
</div>
```

整个实现思路如下图所示：

- 初始位置为方块 1 的位置
- 当设置 left、top 为 50%的时候，内部子元素为方块 2 的位置
- 设置 margin 为负数时，使内部子元素到方块 3 的位置，即中间位置

这种方案不要求父元素的高度，也就是即使父元素的高度变化了，仍然可以保持在父元素的垂直居中位置，水平方向上是一样的操作

但是该方案需要知道子元素自身的宽高，但是我们可以通过下面 transform 属性进行移动

#### 利用定位+transform

实现代码如下：

```html
<style>
  .father {
    position: relative;
    width: 200px;
    height: 200px;
    background: skyblue;
  }
  .son {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 100px;
    height: 100px;
    background: red;
  }
</style>
<div class="father">
  <div class="son"></div>
</div>
```

translate(-50%, -50%)将会将元素位移自己宽度和高度的-50%

这种方法其实和最上面被否定掉的 margin 负值用法一样，可以说是 margin 负值的替代方案，并不需要知道自身元素的宽高

#### table 布局

设置父元素为 display:table-cell，子元素设置 display: inline-block。利用 vertical 和 text-align 可以让所有的行内块级元素水平垂直居中

```html
<style>
  .father {
    display: table-cell;
    width: 200px;
    height: 200px;
    background: skyblue;
    vertical-align: middle;
    text-align: center;
  }
  .son {
    display: inline-block;
    width: 100px;
    height: 100px;
    background: red;
  }
</style>
<div class="father">
  <div class="son"></div>
</div>
```

#### flex 弹性布局

还是看看实现的整体代码：

```html
<style>
  .father {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 200px;
    height: 200px;
    background: skyblue;
  }
  .son {
    width: 100px;
    height: 100px;
    background: red;
  }
</style>
<div class="father">
  <div class="son"></div>
</div>
```

css3 中了 flex 布局，可以非常简单实现垂直水平居中

这里可以简单看看 flex 布局的关键属性作用：

- display: flex 时，表示该容器内部的元素将按照 flex 进行布局

- align-items: center 表示这些元素将相对于本容器水平居中

- justify-content: center 也是同样的道理垂直居中

#### grid 网格布局

```html
<style>
  .father {
    display: grid;
    align-items: center;
    justify-content: center;
    width: 200px;
    height: 200px;
    background: skyblue;
  }
  .son {
    width: 10px;
    height: 10px;
    border: 1px solid red;
  }
</style>
<div class="father">
  <div class="son"></div>
</div>
```

这里看到，gird 网格布局和 flex 弹性布局都简单粗暴

#### 小结

上述方法中，不知道元素宽高大小仍能实现水平垂直居中的方法有：

- 利用定位+margin:auto
- 利用定位+transform
- flex 布局
- grid 布局

### 总结

根据元素标签的性质，可以分为：

- 内联元素居中布局
- 块级元素居中布局

#### 内联元素居中布局

- 水平居中

  - 行内元素可设置：text-align: center
  - flex 布局设置父元素：display: flex; justify-content: center

- 垂直居中

  - 单行文本父元素确认高度：height === line-height
  - 多行文本父元素确认高度：display: table-cell; vertical-align: middle

#### 块级元素居中布局

- 水平居中

  - 定宽: margin: 0 auto
  - 绝对定位+left:50%+margin:负自身一半

- 垂直居中

  - position: absolute 设置 left、top、margin-left、margin-top(定高)
  - display: table-cell
  - transform: translate(x, y)
  - flex(不定高，不定宽)
  - grid(不定高，不定宽)，兼容性相对比较差

## 17.grid 布局

### 17.1 是什么

Grid 布局即网格布局，是一个二维的布局方式，由纵横相交的两组网格线形成的框架性布局结构，能够同时处理行与列

擅长将一个页面划分为几个主要区域，以及定义这些区域的大小、位置、层次等关系

这与之前讲到的 flex 一维布局不相同

设置 display:grid/inline-grid 的元素就是网格布局容器，这样就能出发浏览器渲染引擎的网格布局算法

```html
<div class="container">
  <div class="item item-1">
    <p class="sub-item"></p>
  </div>
  <div class="item item-2"></div>
  <div class="item item-3"></div>
</div>
```

上述代码实例中，.container 元素就是网格布局容器，.item 元素就是网格的项目，由于网格元素只能是容器的顶层子元素，所以 p 元素并不是网格元素

这里提一下，网格线概念，有助于下面对 grid-column 系列属性的理解

网格线，即划分网格的线。

### 17.2 属性

同样，Grid 布局属性可以分为两大类：

- 容器属性，
- 项目属性

关于容器属性有如下：

#### display 属性

文章开头讲到，在元素上设置 display：grid 或 display：inline-grid 来创建一个网格容器

- display：grid 则该容器是一个块级元素

- display: inline-grid 则容器元素为行内元素

#### grid-template-columns 属性，grid-template-rows 属性

grid-template-columns 属性设置列宽，grid-template-rows 属性设置行高

```css
.wrapper {
display: grid;
/_ 声明了三列，宽度分别为 200px 200px 200px _/
grid-template-columns: 200px 200px 200px;
grid-gap: 5px;
/_ 声明了两行，行高分别为 50px 50px _/
grid-template-rows: 50px 50px;
}
```

以上表示固定列宽为 200px 200px 200px，行高为 50px 50px

上述代码可以看到重复写单元格宽高，通过使用 repeat()函数，可以简写重复的值

第一个参数是重复的次数
第二个参数是重复的值
所以上述代码可以简写成

```css
.wrapper {
  display: grid;
  grid-template-columns: repeat(3, 200px);
  grid-gap: 5px;
  grid-template-rows: repeat(2, 50px);
}
```

除了上述的 repeact 关键字，还有：

auto-fill：示自动填充，让一行（或者一列）中尽可能的容纳更多的单元格
grid-template-columns: repeat(auto-fill, 200px) 表示列宽是 200 px，但列的数量是不固定的，只要浏览器能够容纳得下，就可以放置元素

fr：片段，为了方便表示比例关系
grid-template-columns: 200px 1fr 2fr 表示第一个列宽设置为 200px，后面剩余的宽度分为两部分，宽度分别为剩余宽度的 1/3 和 2/3

minmax：产生一个长度范围，表示长度就在这个范围之中都可以应用到网格项目中。第一个参数就是最小值，第二个参数就是最大值
minmax(100px, 1fr)表示列宽不小于 100px，不大于 1fr

auto：由浏览器自己决定长度
grid-template-columns: 100px auto 100px 表示第一第三列为 100px，中间由浏览器决定长度

#### grid-row-gap 属性， grid-column-gap 属性， grid-gap 属性

grid-row-gap 属性、grid-column-gap 属性分别设置行间距和列间距。grid-gap 属性是两者的简写形式

- grid-row-gap: 10px 表示行间距是 10px

- grid-column-gap: 20px 表示列间距是 20px

- grid-gap: 10px 20px 等同上述两个属性

#### grid-template-areas 属性

用于定义区域，一个区域由一个或者多个单元格组成

```css
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;
  grid-template-areas:
    "a b c"
    "d e f"
    "g h i";
}
```

上面代码先划分出 9 个单元格，然后将其定名为 a 到 i 的九个区域，分别对应这九个单元格。

多个单元格合并成一个区域的写法如下

```
grid-template-areas: 'a a a'
'b b b'
'c c c';
```

上面代码将 9 个单元格分成 a、b、c 三个区域

如果某些区域不需要利用，则使用"点"（.）表示

## 18.CSS3 新增了哪些新特性?

### 18.1 是什么

css，即层叠样式表（Cascading Style Sheets）的简称，是一种标记语言，由浏览器解释执行用来使页面变得更美观

css3 是 css 的最新标准，是向后兼容的，CSS1/2 的特性在 CSS3 里都是可以使用的

而 CSS3 也增加了很多新特性，为开发带来了更佳的开发体验

### 18.2 选择器

CSS3 引入了许多新的选择器，使得样式规则的应用更加灵活和强大。以下是一些常用的 CSS3 新增选择器：

#### 1. 属性选择器（Attribute Selectors）

- **[attribute]**：选择具有指定属性的元素。

  ```css
  input[required] {
    border: 1px solid red;
  }
  ```

- **[attribute=value]**：选择具有指定属性且属性值等于给定值的元素。

  ```css
  input[type="text"] {
    border: 1px solid blue;
  }
  ```

- **[attribute^=value]**：选择属性值以给定值开头的元素。

  ```css
  a[href^="https"] {
    color: green;
  }
  ```

- **[attribute$=value]**：选择属性值以给定值结尾的元素。

  ```css
  a[href$=".pdf"] {
    color: red;
  }
  ```

- **[attribute*=value]**：选择属性值包含给定值的元素。

  ```css
  a[href*="example"] {
    color: orange;
  }
  ```

#### 2. 结构伪类选择器（Structural Pseudo-classes）

- **:nth-child(n)**：选择属于其父元素的第 n 个子元素，可以是特定数字、odd（奇数）或 even（偶数）。

  ```css
  tr:nth-child(even) {
    background-color: #f2f2f2;
  }
  ```

- **:nth-last-child(n)**：选择属于其父元素的倒数第 n 个子元素。

  ```css
  li:nth-last-child(2) {
    color: red;
  }
  ```

- **:nth-of-type(n)**：选择属于其父元素的特定类型的第 n 个子元素。

  ```css
  p:nth-of-type(2) {
    font-weight: bold;
  }
  ```

- **:first-of-type** 和 **:last-of-type**：选择属于其父元素的特定类型的第一个和最后一个子元素。

  ```css
  p:first-of-type {
    color: blue;
  }
  p:last-of-type {
    color: green;
  }
  ```

- **:only-child**：选择属于其父元素的唯一子元素。

  ```css
  p:only-child {
    background-color: yellow;
  }
  ```

#### 3. UI 伪类选择器（UI Pseudo-classes）

- **:focus**：选择获得焦点的元素。

  ```css
  input:focus {
    border-color: blue;
  }
  ```

- **:enabled** 和 **:disabled**：选择启用和禁用的表单元素。

  ```css
  input:enabled {
    background-color: white;
  }
  input:disabled {
    background-color: grey;
  }
  ```

- **:checked**：选择被选中的复选框或单选按钮。

  ```css
  input:checked {
    background-color: yellow;
  }
  ```

#### 4. 伪元素选择器（Pseudo-elements）

- **::before** 和 **::after**：在元素内容的前后插入内容。

  ```css
  p::before {
    content: "Note: ";
    color: red;
  }
  p::after {
    content: " (end)";
    color: blue;
  }
  ```

#### 示例回答

“CSS3 引入了许多新的选择器，使我们在选择和应用样式规则时更加灵活和强大。常用的 CSS3 新增选择器包括：

1. **属性选择器**：例如 `[attribute]` 可以选择具有指定属性的元素。
2. **结构伪类选择器**：如 `:nth-child(n)` 可以选择父元素的第 n 个子元素。
3. **UI 伪类选择器**：如 `:focus` 可以选择获得焦点的元素。
4. **伪元素选择器**：如 `::before` 和 `::after` 可以在元素内容的前后插入内容。

这些选择器极大地增强了 CSS 的选择能力，使我们能够更精确地对元素应用样式。”

通过这样的回答，可以展示你对 CSS3 新增选择器的理解和实际应用，同时保持简洁明了，适合在面试中使用。

### 18.3 新样式

#### 边框

css3 新增了三个边框属性，分别是：

- border-radius：创建圆角边框

- box-shadow：为元素添加阴影

- border-image：使用图片来绘制边框

#### box-shadow

设置元素阴影，设置属性如下：

- 水平阴影
- 垂直阴影
- 模糊距离(虚实)
- 阴影尺寸(影子大小)
- 阴影颜色
- 内/外阴影

其中水平阴影和垂直阴影是必须设置的

#### 背景

新增了几个关于背景的属性，分别是 background-clip、background-origin、background-size 和 background-break

##### background-clip

用于确定背景画区，有以下几种可能的属性：

- background-clip: border-box; 背景从 border 开始显示
- background-clip: padding-box; 背景从 padding 开始显示
- background-clip: content-box; 背景显 content 区域开始显示
- background-clip: no-clip; 默认属性，等同于 border-box

通常情况，背景都是覆盖整个元素的，利用这个属性可以设定背景颜色或图片的覆盖范围

##### background-origin

当我们设置背景图片时，图片是会以左上角对齐，但是是以 border 的左上角对齐还是以 padding 的左上角或者 content 的左上角对齐? border-origin 正是用来设置这个的

- background-origin: border-box; 从 border 开始计算 background-position
- background-origin: padding-box; 从 padding 开始计算 background-position
- background-origin: content-box; 从 content 开始计算 background-position

默认情况是 padding-box，即以 padding 的左上角为原点

##### background-size

background-size 属性常用来调整背景图片的大小，主要用于设定图片本身。有以下可能的属性：

- background-size: contain; 缩小图片以适合元素（维持像素长宽比）
- background-size: cover; 扩展元素以填补元素（维持像素长宽比）
- background-size: 100px 100px; 缩小图片至指定的大小
- background-size: 50% 100%; 缩小图片至指定的大小，百分比是相对包 含元素的尺寸

##### background-break

元素可以被分成几个独立的盒子（如使内联元素 span 跨越多行），background-break 属性用来控制背景怎样在这些不同的盒子中显示

- background-break: continuous; 默认值。忽略盒之间的距离（也就是像元素没有分成多个盒子，依然是一个整体一样）
- background-break: bounding-box; 把盒之间的距离计算在内；
- background-break: each-box; 为每个盒子单独重绘背景

#### 文字

##### word-wrap

语法：word-wrap: normal|break-word

- normal：使用浏览器默认的换行
- break-all：允许在单词内换行

##### text-overflow

text-overflow 设置或检索当当前行超过指定容器的边界时如何显示，属性有两个值选择：

- clip：修剪文本
- ellipsis：显示省略符号来代表被修剪的文本

##### text-shadow

text-shadow 可向文本应用阴影。能够规定水平阴影、垂直阴影、模糊距离，以及阴影的颜色

##### text-decoration

CSS3 里面开始支持对文字的更深层次的渲染，具体有三个属性可供设置：

- text-fill-color: 设置文字内部填充颜色

- text-stroke-color: 设置文字边界填充颜色

- text-stroke-width: 设置文字边界宽度

#### 颜色

css3 新增了新的颜色表示方式 rgba 与 hsla

- rgba 分为两部分，rgb 为颜色值，a 为透明度
- hsla 分为四部分，h 为色相，s 为饱和度，l 为亮度，a 为透明度

### 18.4 transition 过渡

transition 属性可以被指定为一个或多个 CSS 属性的过渡效果，多个属性之间用逗号进行分隔，必须规定两项内容：

- 过度效果
- 持续时间

语法如下：

```css
transition： CSS 属性，花费时间，效果曲线(默认 ease)，延迟时间(默认 0)
```

上面为简写模式，也可以分开写各个属性

- transition-property: width;
- transition-duration: 1s;
- transition-timing-function: linear;
- transition-delay: 2s;

### 18.5 transform 转换

- transform 属性允许你旋转，缩放，倾斜或平移给定元素

- transform-origin：转换元素的位置（围绕那个点进行转换），默认值为(x,y,z):(50%,50%,0)

使用方式：

- transform: translate(120px, 50%)：位移
- transform: scale(2, 0.5)：缩放
- transform: rotate(0.5turn)：旋转
- transform: skew(30deg, 20deg)：倾斜

### 18.6 animation 动画

动画这个平常用的也很多，主要是做一个预设的动画。和一些页面交互的动画效果，结果和过渡应该一样，让页面不会那么生硬

animation 也有很多的属性

- animation-name：动画名称
- animation-duration：动画持续时间
- animation-timing-function：动画时间函数
- animation-delay：动画延迟时间
- animation-iteration-count：动画执行次数，可以设置为一个整数，也可以设置为 infinite，意思是无限循环
- animation-direction：动画执行方向
- animation-paly-state：动画播放状态
- animation-fill-mode：动画填充模式

### 18.7 渐变

颜色渐变是指在两个颜色之间平稳的过渡，css3 渐变包括

- linear-gradient：线性渐变

> background-image: linear-gradient(direction, color-stop1, color-stop2, ...);

- radial-gradient：径向渐变

> linear-gradient(0deg, red, green);

### 18.8 其他

关于 css3 其他的新特性还包括 flex 弹性布局、Grid 栅格布局，这两个布局在以前就已经讲过，这里就不再展示

除此之外，还包括多列布局、媒体查询、混合模式等等......

## 19.CSS3 动画

### 19.1 是什么

CSS 动画（CSS Animations）是为层叠样式表建议的允许可扩展标记语言（XML）元素使用 CSS 的动画的模块

即指元素从一种样式逐渐过渡为另一种样式的过程

常见的动画效果有很多，如平移、旋转、缩放等等，复杂动画则是多个简单动画的组合

css 实现动画的方式，有如下几种：

- transition 实现渐变动画
- transform 转变动画
- animation 实现自定义动画

### 19.2 实现方式

#### transition 实现渐变动画

transition 的属性如下：

- property:填写需要变化的 css 属性
- duration:完成过渡效果需要的时间单位(s 或者 ms)
- timing-function:完成效果的速度曲线
- delay: 动画效果的延迟触发时间

其中 timing-function 的值有如下：

|                       |                                                                  |
| :-------------------: | :--------------------------------------------------------------: |
|          值           |                               描述                               |
|        linear         |                匀速（等于 cubic-bezier(0,0,1,1)）                |
|         ease          |         从慢到快再到慢（cubic-bezier(0.25,0.1,0.25,1)）          |
|        ease-in        |            慢慢变快（等于 cubic-bezier(0.42,0,1,1)）             |
|       ease-out        |            慢慢变慢（等于 cubic-bezier(0,0,0.58,1)）             |
|      ease-in-out      |  先变快再到慢（等于 cubic-bezier(0.42,0,0.58,1)），渐显渐隐效果  |
| cubic-bezier(n,n,n,n) | 在 cubic-bezier 函数中定义自己的值。可能的值是 0 至 1 之间的数值 |

注意：并不是所有的属性都能使用过渡的，如 display:none<->display:block

举个例子，实现鼠标移动上去发生变化动画效果

```html
<style>
  .base {
    width: 100px;
    height: 100px;
    display: inline-block;
    background-color: #0ea9ff;
    border-width: 5px;
    border-style: solid;
    border-color: #5daf34;
    transition-property: width, height, background-color, border-width;
    transition-duration: 2s;
    transition-timing-function: ease-in;
    transition-delay: 500ms;
  }

  /*简写*/
  /*transition: all 2s ease-in 500ms;*/
  .base:hover {
    width: 200px;
    height: 200px;
    background-color: #5daf34;
    border-width: 10px;
    border-color: #3a8ee6;
  }
</style>
<div class="base"></div>
```

#### transform 转变动画

transform 转变动画
包含四个常用的功能：

- translate：位移
- scale：缩放
- rotate：旋转
- skew：倾斜

一般配合 transition 过度使用

注意的是，transform 不支持 inline 元素，使用前把它变成 block

举个例子

```html
<style>
  .base {
    width: 100px;
    height: 100px;
    display: inline-block;
    background-color: #0ea9ff;
    border-width: 5px;
    border-style: solid;
    border-color: #5daf34;
    transition-property: width, height, background-color, border-width;
    transition-duration: 2s;
    transition-timing-function: ease-in;
    transition-delay: 500ms;
  }
  .base2 {
    transform: none;
    transition-property: transform;
    transition-delay: 5ms;
  }

  .base2:hover {
    transform: scale(0.8, 1.5) rotate(35deg) skew(5deg) translate(15px, 25px);
  }
</style>
<div class="base base2"></div>
```

可以看到盒子发生了旋转，倾斜，平移，放大

### 19.3 animation 实现自定义动画

### 19.4 总结

### 19.5 优化

优化 CSS 动画可以提高页面性能和用户体验，特别是在移动设备上。下面是一些优化 CSS 动画的常见方法：

1. **使用 GPU 加速**：通过使用 CSS 属性如 `transform` 和 `opacity`，可以触发 GPU 加速，从而提高动画性能。避免使用会触发重排和重绘的属性，如 `width`、`height`、`margin`、`padding` 等。

2. **合理使用 `will-change` 属性**：`will-change` 属性告诉浏览器一个元素将要被改变，从而优化渲染性能。但滥用 `will-change` 可能会导致额外的内存消耗和性能问题，因此只应在必要时使用。

   ```css
   .element {
     will-change: transform;
   }
   ```

3. **使用 `translate` 替代 `top` 或 `left`**：`translate` 属性比修改 `top` 或 `left` 属性更高效，因为它可以触发 GPU 加速而不会导致页面重排。

4. **减少动画元素的数量**：减少页面上同时进行动画的元素数量，特别是在移动设备上，可以降低内存和 CPU 的消耗，提高动画性能。

5. **使用 `requestAnimationFrame`**：使用 `requestAnimationFrame` 函数调度动画，以便浏览器在每一帧之前执行动画，以避免掉帧和提高性能。

6. **避免过度绘制**：避免在页面上同时使用大量复杂的动画，因为过多的动画会导致浏览器频繁重绘，降低性能。可以通过分解复杂的动画效果，使用 CSS 动画合成器来减少过度绘制。

7. **使用硬件加速的 `opacity`**：在需要使用 `opacity` 动画时，尽量使用硬件加速，例如使用 `translateZ(0)` 或 `backface-visibility: hidden`。

8. **避免使用 `outline` 和 `box-shadow` 动画**：`outline` 和 `box-shadow` 动画通常性能较差，尽量避免在动画中使用它们，或者尽量减少它们的使用。

9. **优化复杂动画的帧率**：对于复杂的动画，可以降低动画的帧率以提高性能。例如，使用 `animation-timing-function` 属性将帧率从默认的 60fps 降低到 30fps。

10. **使用 CSS 动画库**：使用已经优化过的 CSS 动画库，如 Animate.css 或者 GSAP（GreenSock Animation Platform），这些库经过优化可以提供更好的性能和更丰富的动画效果。

通过这些优化措施，可以有效提高 CSS 动画的性能和流畅度，提升用户体验。
