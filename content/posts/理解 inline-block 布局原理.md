+++
title = "理解 inline-block 布局原理"
date = "2018-01-05T20:12:33+08:00"
author = "horochx" 
cover = ""
tags = ["CSS"]
description = "博主近日在开发中运用到了大量的 `display: inline-block` 来处理布局问题，踩了许多坑，出现了诸多预料之外的显示效果。在解决了所有 inline-block 的疑难杂症之后，写下了这篇博客，作为一个总结。"
showFullContent = false
+++

博主近日在开发中运用到了大量的 `display: inline-block` 来处理布局问题，踩了许多坑，出现了诸多预料之外的显示效果。在解决了所有 inline-block 的疑难杂症之后，写下了这篇博客，作为一个总结。

## 布局方案的选择

对于常用的 HTML 的页面布局，有 table、float、position、flex 四种。

- tabel 作为古老而经典的布局方案，代码复杂、可读性差，已经成为了历史。
- postion 可以用于实现类似 PS 图层的显示效果，具有不可替代的作用。
- flex 作为一种现代化的布局方案，可以优雅的解决自适应布局、响应式布局、水平居中、垂直居中等等一系列复杂的问题，对我来说它有数不清的优点。阻碍我使用它的唯一原因，就是低版本 IE 浏览器对于 flex 的糟糕支持度，没有 IE 就没有伤害。
- float 作为一种常用的布局手段，可以快速实现诸如导航栏、水平列表等等需求。但是 float 元素会脱离普通流，带来诸如父元素高度塌陷等等问题。虽然可以通过 CSS 伪元素来优雅地清除浮动，但是终究有些不美。float 样式的本意，是用来实现类似于 word 的“文字环绕图片”的效果。基于

  > CSS 的可维护性源自对于设计意图的准确表达

  的原则，我决定使用 inline-block 来处理块级元素的水平排列（因此踏进了一个天坑）。

## inline-block 元素的基本特征

- 具有行内元素水平排列的特点，不同的是，当前行剩余宽度不足时会整块换行。
- 具有块级元素的盒模型，可以设置宽高，具有 margin 和 padding 属性。如果未设置宽高则会自适应内容大小。
- inline-block 可以使用行内元素的样式属性(如 vertical-align)
- 如果书写 HTML 时在 inline-block 元素间留下了空白符（空格、tab、回车），那么在 HTML 文档的最终呈现中会在 inline-block 元素间留出空白。为什么呢？因为 inline-block 元素具备了行内元素的特征。而行内元素间的空白符在 HTML 的最终呈现中会被合并为一个空白元素。因此我们需要对 inline-block 元素的父容器设置 `font-size: 0`，以隐藏空白符。

通常而言，我们**需要通过空白符来隔开 inline-block 元素**，使得 inline-block 在应用行内样式的时候，每个 inline-block 可以具有和字符一样的布局效果，这就是 inline-block 布局的基本实现思路。

## 基于 text-align 的 inline-block 水平布局

### 水平居中

简单地在父元素设置 `text-align: center` 即可。

```HTML
<style>
  .demo-parent,
  .demo-child {
    outline: 1px dashed #f00;
    background: linear-gradient(
        90deg,
        rgba(255, 255, 255, 0.5) 50%,
        rgba(0, 0, 0, 0.5) 50%
      ),
      linear-gradient(rgba(255, 255, 255, 0.5) 50%, rgba(0, 0, 0, 0.5) 50%);
  }
  .demo-parent {
    width: 100%;
    height: 300px;
    text-align: center;
  }
  .demo-child {
    display: inline-block;
    width: 100px;
    height: 100px;
  }
</style>
<div class="demo-parent">
  <div class="demo-child"></div>
</div>
```

<style>
  .demo-parent,
  .demo-child {
    outline: 1px dashed #f00;
    background: linear-gradient(
        90deg,
        rgba(255, 255, 255, 0.5) 50%,
        rgba(0, 0, 0, 0.5) 50%
      ),
      linear-gradient(rgba(255, 255, 255, 0.5) 50%, rgba(0, 0, 0, 0.5) 50%);
  }
  .demo-parent {
    width: 100%;
    height: 300px;
    text-align: center;
  }
  .demo-child {
    display: inline-block;
    width: 100px;
    height: 100px;
  }
</style>
<div class="demo-parent">
  <div class="demo-child"></div>
</div>

### 水平分散

在父元素设置 `text-align: justify` 即可。需要注意的是 justify 对最后一行无效，单行的时候第一行即是最后一行，因此 justify 对单行也无效。但是，我们可以通过伪元素选择器 `::after` 创建一个宽度为 100%、高度为 0 的伪元素，使得单行变为两行，以实现水平分散的效果。

```HTML
<style>
  .demo-parent-justify {
    text-align: justify;
  }
  .demo-parent-justify::after {
    content: "";
    display: inline-block;
    width: 100%;
  }
</style>
<div class="demo-parent demo-parent-justify">
  <div class="demo-child"></div>
  <!-- 这里留下了空白符 -->
  <div class="demo-child"></div>
</div>
```

<style>
  .demo-parent-justify {
    text-align: justify;
  }
  .demo-parent-justify::after {
    content: "";
    display: inline-block;
    width: 100%;
  }
</style>
<div class="demo-parent demo-parent-justify">
  <div class="demo-child"></div>
  <!-- 这里留下了空白符 -->
  <div class="demo-child"></div>
</div>

### 水平自适应分散

在父元素设置 `text-align: justify; letter-spacing: 0px;` 即可，letter-spacing 可用于设置两两元素之间的最小间距。需要注意的是，letter-spacing 是可继承样式，需要在子元素中设置 `letter-spacing: normal` 来修复字符间距。

```HTML
<style>
  .demo-parent-letterspacing {
    letter-spacing: 20px;
  }
</style>
<div class="demo-parent demo-parent-justify demo-parent-letterspacing">
  <div class="demo-child"></div>
  <div class="demo-child"></div>
  <div class="demo-child"></div>
  <div class="demo-child"></div>
  <div class="demo-child"></div>
  <div class="demo-child"></div>
</div>
```

<style>
  .demo-parent-letterspacing {
    letter-spacing: 20px;
  }
</style>
<div class="demo-parent demo-parent-justify demo-parent-letterspacing">
  <div class="demo-child"></div>
  <div class="demo-child"></div>
  <div class="demo-child"></div>
  <div class="demo-child"></div>
  <div class="demo-child"></div>
  <div class="demo-child"></div>
</div>

<p>
  <input
    id="rang-letterspacing"
    type="range"
    value="20"
    min="20"
    max="80"
  />拖动滑块增加元素最小间距，直到元素换行
</p>
<script>
  (function () {
    var range = document.getElementById("rang-letterspacing");
    var node = document.querySelector(".demo-parent-letterspacing");
    range.addEventListener("input", function () {
      node.style.letterSpacing = range.value + "px";
    });
  })();
</script>

## 基于 vertical-align 的 inline-block 垂直布局

在谈及 inline-block 的垂直布局之前，要先了解 line-box 的概念，否则无法理解 inline-block 中 vertical-align 的复杂表现。

line-box 是什么呢？每当存在一个行内元素（这里泛指 inline、inline-\* 与可替换行内元素），就会产生一个不可见的 line-box 将其包裹。同一行的行内元素，会被同一个 line-box 包裹。 line-box 的高度是当前行的行内元素的最高处至当前行的行内元素的最低处的高度。

- 对于 `display: inline` 的元素而言，这个最高处与最低处是指字符占据的的空间高度(virtual-area)——line-height 的高度。line-height 是以字符的内容区域(content-area)的中心为中心，向上下两边扩张的。那么内容区域的高度是什么呢？内容区域的高度是由字体所决定的，是字体设计师在设计字体时所指定的值，即字符的内容区域高度与 font-family 及 font-size 有关。vertical-align 的 text-top 与 text-bottom 就是以内容区域作为基准，而 top 与 bottom 则是以 line-box 作为基准。

  ![inline 元素具有两个不同的高度](/img/line-height.png)

- 对于 inline-block 元素(以及其它 inline-\* 元素、可替换行内元素) 而言，其占据的的空间高度由盒模型的 margin、padding、height 计算得到。如果未指定 height(`height: auto`)，那么则由 line-height 参与计算。且其内容高度严格等于空间高度。

  ![inline-block 元素具有与高度相容的内容区域](/img/line-height-inline-block.png)

- 同时，浏览器进行布局计算时认为 **line-box 的起始位置有一个宽度为 0 的名为 strut 的字符**。strut 不可见，但参与布局，其高度同样要计入 line-box 的高度中。

  ![strut 参与布局](/img/vertical-align-strut.png)

理解了 line-box 的存在之后，才能理解 vertical-align 的所有表现。

### 默认情况下的表现(`vertical-align: baseline`)

```HTML
<style>
<style>
  .demo-parent-v {
    height: auto;
  }
</style>
<div class="demo-parent demo-parent-v">
  <div class="demo-child"></div>
</div>
```

<style>
  .demo-parent-v {
    height: auto;
  }
</style>
<div class="demo-parent demo-parent-v">
  <div class="demo-child"></div>
</div>

<script>
  (function () {
    var node = document.getElementsByClassName("demo-parent-v")[0];
    var child = node.querySelector(".demo-child");
    node.style.color = "red";
    child.textContent = "";
    node.addEventListener("click", function () {
      if (child.textContent === "") {
        child.style.verticalAlign = "top";
        child.textContent = "vertical-align:top;";
      } else {
        child.style.verticalAlign = "baseline";
        child.textContent = "";
      }
    });
  })();
</script>

元素与父容器的底边存在一个微小的边距，这是为什么呢？因为 vertical-align 的默认设置是 baseline。所以对齐的是 strut 的 baseline。 我们理解了下边距存在是由于 `vertical-align: baseline` 和 struct 的共同作用之后，很自然的就可以找到办法解决它：更改 vertical-align，不管是 top 也好，bottom 也好，只要不再基于 baseline，都能解决这个问题。（点击上面的 demo 试试看吧~）

PS: 对于没有内容的 inline-block 元素，baseline 是它的 margin-bottom 的边缘。对于有内容的 inline-block 元素，baseline 是它的内容的 baseline。

### 设置 `vertical-align: middle` 时的表现

如果 inline-block 元素需要进行垂直居中对齐，我们会很自然地想到通过 `vertical-align: middle` 这个属性来进行设置。想到就做，让我们试试看吧！<br>

```HTML
<style>
  .demo-parent-middle {
    font-size: 80px;
  }
  .demo-parent-middle .demo-child {
    vertical-align: middle;
  }
  .demo-child-higher {
    height: 150px;
  }
</style>
<div class="demo-parent demo-parent-middle">
  <div class="demo-child"></div>
  <div class="demo-child demo-child-higher"></div>
</div>
```

<style>
  .demo-parent-middle {
    font-size: 80px;
  }
  .demo-parent-middle .demo-child {
    vertical-align: middle;
  }
  .demo-child-higher {
    height: 150px;
  }
  .demo-x {
    outline: 1px dashed #f00;
    background: linear-gradient(
      rgba(255, 255, 255, 0.5) 50%,
      rgba(0, 0, 0, 0.5) 50%
    );
    color: red;
  }
</style>
<div class="demo-parent demo-parent-middle">
  <div class="demo-child"></div>
  <div class="demo-child demo-child-higher"></div>
</div>

<script>
  (function () {
    var node = document.querySelector(".demo-parent-middle");
    var x = document.createElement("span");
    x.className = "demo-x";
    x.textContent = "x";

    var step1 = function () {
      node.insertBefore(x, node.firstChild);
      node.removeEventListener("click", step1);
      node.addEventListener("click", step2);
    };
    var step2 = function () {
      node.className += " demo-fix";
      node.removeEventListener("click", step2);
      node.addEventListener("click", stepRest);
    };
    var stepRest = function () {
      node.removeChild(x);
      node.className = node.className.replace(" demo-fix", "");
      node.removeEventListener("click", stepRest);
      node.addEventListener("click", step1);
    };
    node.addEventListener("click", step1);
  })();
</script>

实际的效果有些令人失望。。为什么呢？首先，我们要正确理解 `vertical-align: middle` 这个属性。MDN 中是这么描述的：

> 元素中垂线与父元素的基线加上小写 x 一半的高度值对齐。

当元素的高度小于 x 的时候，很容易就能想象得到显示效果——元素的中垂线对齐于小写字母 x 的中垂线。当元素高度大于小写字母 x 的情形下呢？让我们点击上面的 demo 看看吧！我们注意到 line-box 被撑开了，除了小写字母 x，其它元素均相对于 line-box 垂直居中对齐啦！那么只要让 line-box 的高度等于父元素高度，就实现了垂直居中效果。我们很自然的想到，只要有一个看不见的元素撑开 line-box，使得 line-box 的高度等于父容器的高度，不就行了吗？虽然说设置父元素的 line-height 等于父元素的容器高度就可以简单的做到，但是 line-height 是可继承属性，我们可以通过一个伪元素来简单地实现这一切：

```HTML
<style>
  .demo-fix::before {
    content: "";
    display: inline-block;
    width: 0;
    height: 100%;
    vertical-align: middle;
  }
</style>
```

<style>
  .demo-fix::before {
    content: "";
    display: inline-block;
    width: 0;
    height: 100%;
    vertical-align: middle;
  }
</style>

再次点击上面的 demo 就可以看到效果啦~

## 结语

至此，inline-block 布局就告一段落了。就个人感受而言，line-box 的模型真是比盒模型复杂得多。inline-block 可以使用 text-align 和 vertical-align 属性进行便利的布局，然而有内容时和没有内容时的 baseline 会发生变化，从而导致 vertical-align 的表现变得异常复杂。但是，我依然喜欢 inline-block \_(:з)∠)\_
