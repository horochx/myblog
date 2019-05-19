+++
title = "HTML 基础知识"
date = 2019-05-13T22:18:47+08:00
author = "horochx" 
cover = ""
tags = ["前端基础知识", "HTML"]
description = '1980 年，欧洲核子研究中心的承包商物理学家 _蒂姆·伯纳斯-李（Tim Berners-Lee）_ 提出了一个构想：创建一个以超文本系统为基础的项目，方便研究人员分享及更新讯息。同时，他创建了一个原型系统，叫 _ENQUIRE_ 。_蒂姆·伯纳斯-李_ 后来用与 _ENQUIRE_ 相似的概念，创建了万维网，完成了世界上第一个浏览器，成立了 <abbr title="World Wide Web Consortium">W3C</abbr> 并担任主席。这就是 <abbr title="HyperText Markup Language">HTML</abbr> 和万维网最初的起源。'
showFullContent = false
+++

1980 年，欧洲核子研究中心的承包商物理学家 _蒂姆·伯纳斯-李（Tim Berners-Lee）_ 提出了一个构想：创建一个以超文本系统为基础的项目，方便研究人员分享及更新讯息。同时，他创建了一个原型系统，叫 _ENQUIRE_ 。_蒂姆·伯纳斯-李_ 后来用与 _ENQUIRE_ 相似的概念，创建了万维网，完成了世界上第一个浏览器，成立了 <abbr title="World Wide Web Consortium">W3C</abbr> 并担任主席。这就是 <abbr title="HyperText Markup Language">HTML</abbr> 和万维网最初的起源。

经过多年的发展， HTML 已经成为了互联网世界最重要的基石之一。HTML 自身也在不断发展，提供新功能的同时逐步完善标准。现今，HTML 最新的修订版本是 HTML5。

## HTML5 技术集

HTML5 实际上是一组用于构建更多样化和更强大的应用程序的技术集合（不知为何，中文语境中的 H5 常常指移动端的 HTML 页面 🤔）。本文会简单地介绍一下 HTML5 包含的技术集，然后再具体地介绍一下 _常用_ 的 HTML 元素。

HTML5 包含以下几个内容：

- **语义** ：提供更准确的语义用于描述内容。
- **连通性** ：提供新技术让页面与服务器进行通信。
- **离线 & 存储** ：能够让页面在客户端本地存储数据以及更高效地离线运行。
- **多媒体** ：使 video 和 audio 成为了在所有 Web 中的一等公民。
- **2D/3D 绘图 & 效果** ：提供了一个范围更加广泛的视图呈现选择。
- **性能 & 集成** ：提供了非常显著的性能优化和更有效的计算机硬件使用。
- **设备访问** ：能够处理各种输入和输出设备。
- **样式设计** ：让作者们可以创作更加复杂的页面主题。

### 语义

HTML5 提供了新的元素，如 `<article>`、`<header>`、`<footer>` 等。

### 连通性

Web Sockets 允许页面和服务器建立持久的连接，同时进行双向通信。

Server-sent events 允许页面监听服务器推送的事件，进行服务器到页面的单向通信。

<abbr title="Web Real-Time Communication">WebRTC</abbr> 允许页面与页面之间建立连接，实现即时通信。

### 离线 & 存储

Service Workers 可以充当 Web 应用程序与浏览器之间的代理服务器，实现离线应用。

`navigator.onLine` 及 `online` 与 `offline` 事件用于监听浏览器的网络连接状态。（实际上浏览器对这个接口的实现各不相同，并不能通过这个接口准确判断浏览器的网络状态）

Storage 接口允许在本地以键值对的方式存储字符串数据。

IndexedDB 是一个事务型数据库系统，可以在客户端存储大量结构化数据(包括 `Blob`)。

### 多媒体

`<audio>` 和 `<video>` 元素用于支持多媒体资源，`<track>` 元素可以作为 `<audio>` 和 `<video>` 的子元素来使用，用于字幕显示。

Camera API 可以调用手机摄像头拍照，并把照片发送到当前页面。

### 2D/3D 绘图 & 效果

Canvas 可以使用 JavaScript 来绘制位图。

WebGL 把 JavaScript 和 OpenGL ES 2.0 结合在一起，在 `<canvas>` 元素中呈现交互式的 2D、3D 图形。

SVG 是一种可以直接嵌入到 HTML 中的矢量图像格式，使用 XML 描述图像及相关行为。

### 性能 & 集成

Web Workers 能够创建后台线程，以避免复杂的 JavaScript 计算阻塞页面交互。（实际上 Web Workers 与页面的通信本身也是有开销的，需要酌情使用）

XMLHttpRequest Level 2 为 Ajax 实现了新的功能，如请求超时时限、跨域请求、二进制数据传输、传输进度信息等。

History API 允许对浏览器历史记录进行操作，结合 Ajax 用于交互地加载新信息的页面（现代单页应用）。

`contentEditable` 属性被标准化，用以实现富文本编辑器。

`Drag​Event` 接口让 Web 应用程序可以实现拖放功能。

`document.activeElement` 与 `document.hasFocus()` 用于管理页面焦点。

`navigator.registerProtocolHandler()` 方法可以把 Web 应用程序注册为一个协议处理程序，实现类似 DeepLink 的功能。

`requestAnimationFrame` 用于向浏览器请求一个渲染帧，可以实现高性能的 JavaScript 动画。

Fullscreen API 可以简单地控制浏览器，让一个元素及其子元素全屏显示。

Pointer Lock API 提供了一种新的输入方法，访问鼠标随着时间推移的运动的量，而非光标在屏幕中的位置，使得光标移到浏览器或者屏幕区域之外时依然可以被检测到。

### 设备访问

`TouchEvent` 允许对用户按下触控屏的事件做出反应。

`navigator.geolocation` 允许访问用户的地理位置（需要 HTTPS 环境）。

`DeviceOrientationEvent` 用于检测设备方向的变化，`DeviceMotionEvent` 用于检测设备加速度的变化，二者结合可以监听设备的运动。

`MediaDevices` 接口用于访问设备的音视频输入设备。（它实际上是 WebRTC 的一部分）

### 样式设计

<abbr title="Cascading Style Sheets">CSS</abbr> 经过了扩展，能够给元素设置更丰富的样式，如阴影、边框圆角、过渡与动画、弹性布局、多栏布局与网格布局，这通常被称为 CSS3 。但实际上，CSS3 标准自身已经不存在了，每个模块都被独立的标准化，现在标准 CSS 包括了修订后的 CSS2.1 以及完整模块对它的扩充，模块的 level（级别）数并不一致。

## 常用 HTML 元素

一份常见的 HTML 文档，其结构大致如下所示：

```html
<!DOCTYPE html>
<html>
  <!-- 文档头部 -->
  <head>
    <!-- 字符编码必须写在第一行，以保证后续的字符能够被正确解析 -->
    <meta charset="utf8" />
    <meta name="keywords" content="关键字" />
    <meta name="description" content="页面描述" />
    <meta name="viewport" content="width=device-width" />
    <title>页面标题</title>
    <link rel="shortcut icon " href="favicon.ico " />
    <link rel="sytlesheet " href="style.css" />
  </head>
  <!-- 页面内容 -->
  <body></body>
</html>
```

`DOCTYPE` 就是 document type，用于区分浏览器的标准模式与<a href="https://quirks.spec.whatwg.org/" target="_blank">怪异模式</a>。在 HTML 标准不那么统一的年代，还用于告知浏览器使用哪个标准渲染页面。对于 HTML5，使用 `<!DOCTYPE html>` 即可。

`body` 中的内容用于页面呈现。

### 内容分区

内容分区元素允许开发者将文档内容以逻辑的方式进行划分，使用如页眉、页脚等元素为页面内容创建明确的大纲，以便区分各个区域的内容。常用的内容分区元素如下：

| 元素                                 | 描述                                                                                                                                 |
| :----------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------- |
| `<header>`                           | 定义内容的头部，经常包含 logo、页面标题和导航性的目录。                                                                              |
| `<nav>`                              | 定义页面中只包含导航链接的区域，通常置于 `<header>` 中。                                                                             |
| `<footer>`                           | 定义内容的尾部。它经常包含版权信息、法律信息链接和反馈建议用的地址。                                                                 |
| `<address>`                          | 定义联系方式，通常置于 `<footer>` 中。                                                                                               |
| `<main>`                             | 定义了页面的主体内容。主体内容在一系列文档中应当是 **独一无二** 的，不包含导航栏等重复的内容。                                       |
| `<aside>`                            | 定义和页面内容关联度较低的内容，如果被删除，不会使文档的完整性受到影响。                                                             |
| `<h1>, <h2>, <h3>, <h4>, <h5>, <h6>` | 定义页面中的六层文档标题。                                                                                                           |
| `<article>`                          | 定义页面中的一个可以独立于内容其余部分的 **完整独立或可复用** 内容块。（其中使用的 `<h1>` ~ `<h6>`，标题层级独立于页面的其它部分。） |
| `<section>`                          | 定义文档中的一个区域或节，子元素中通常包含一个 `<h1>` ~ `<h6>`。                                                                     |

### 组织内容

组织内容元素用于组织块或章节里的内容，用于标识内容的宗旨或结构，这对于 <abbr title="Web Accessibility Initiative">WAI</abbr> 与 <abbr title="Search Engine Optimization">SEO</abbr> 很重要。

| 元素           | 描述                                                                                                                                           |
| :------------- | :--------------------------------------------------------------------------------------------------------------------------------------------- |
| `<p>`          | 表示一个段落。                                                                                                                                 |
| `<hr>`         | 表示段落级元素之间的主题转换（例如章节中的主题改变了），通常表现为一条分割线。但它被定义为 **语义上的**，而不是表现层面上。                    |
| `<pre>`        | 表示内容已经经过排版，格式（空白符）应当保留。                                                                                                 |
| `<blockquote>` | 表示引用自其它来源的内容。如果来源于网络，可以把来源内容设置在 `cite` 属性上。如果把来源以文本的形式显示出来，则需要使用 `<cite>` 元素。       |
| `<ol>`         | 表示一个有序列表。                                                                                                                             |
| `<ul>`         | 表示一个无须列表。                                                                                                                             |
| `<li>`         | 表示一个列表中的项，必须是一个列表元素(`<ol>`、`<ul>`)的子元素。                                                                               |
| `<dl>`         | 表示一个包含术语定义以及描述(键-值对)的列表。                                                                                                  |
| `<dt>`         | 表示术语定义列表项中声明的一个术语，其后可以跟随多个 `<dd>` 元素用于解释此条术语。                                                             |
| `<dd>`         | 表示术语定义列表项中术语的解释，必须紧跟在 `<dt>` 或其它 `<dd>` 之后。                                                                         |
| `<figure>`     | 表示一段与文档有关但独立内容，转移到其他页面时不会影响到主体。其内容可以是文档中引用的插图、图标、代码示例等。通常与 `<figcaption>` 配合使用。 |
| `<figcaption>` | 表示 `<figure>` 的标题或是说明，必须是 `<figure>` 的第一个或是最后一个子元素。                                                                 |
| `<div>`        | 表示一个通用的容器，当没有其它适合的内容组织元素时使用。                                                                                       |

### 文本语义

文本语义元素用于定义任意文字的语义、结构或样式。

| 元素           | 描述                                                                                                                                                        |
| :------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `<a>`          | 代表链接，可以用于其它 URL。                                                                                                                                |
| `<em>`         | 代表需要用户着重阅读的文字。`<em>` 可以嵌套，嵌套层级越深，着重程度越高。                                                                                   |
| `<strong>`     | 代表文本特别重要。                                                                                                                                          |
| `<small>`      | 代表注释和附属细则，包括版权和法律文本等，对理解文本无用的内容。某种程度上与 `<strong>` 是相反的语义。                                                      |
| `<q>`          | 代表引用自其它来源的内容。等同 `<blockquote>` ，不过是 `<q>` 内联的。                                                                                       |
| `<cite>`       | 代表一个作品的引用来源，可以是作品标题、URL 乃至 ISBN 等。                                                                                                  |
| `<abbr>`       | 代表省略或单词缩写，完整形式在 `title` 属性中给出。                                                                                                         |
| `<time>`       | 代表日期或时间值，机器可读的等价形式通过 `datetime` 属性指定。                                                                                              |
| `<code>`       | 代表计算机代码。                                                                                                                                            |
| `<var>`        | 代表代码中的变量或是由用户提供的值。                                                                                                                        |
| `<samp>`       | 代表计算机程序的输出。                                                                                                                                      |
| `<kbd>`        | 代表用户的输入。通常而言是键盘按键输入，但也可以是其它输入，如语音。                                                                                        |
| `<sub>, <sup>` | 代表上标和下标。                                                                                                                                            |
| `<i>`          | 代表因某些原因需要和普通文本进行区分的一系列文本。例如技术术语、外文短语或是小说中人物的思想活动等。                                                        |
| `<b>`          | 代表需要吸引读者的注意的文本。 无其它特殊语义，仅在 `<em>` 、`<strong>` 都不合适的时候使用。                                                                |
| `<mark>`       | 代表在 **特定的上下文中** 需要被特别标记的内容。 `<strong>` 用来表示文本在上下文中的重要性， 而 `<mark>` 是用来表示上下文的关联性。                         |
| `<ruby>`       | 代表有注音的东亚文字，需要结合 `<rp>` 与 `<rt>` 使用。                                                                                                      |
| `<rt>`         | 代表字符的发音。必须作为 `<ruby>` 的子元素使用。                                                                                                            |
| `<rp>`         | 用于不支持 `<ruby>` 元素的情况，在 `<rt>` 的前后显示注释性文本，通常是圆括号。                                                                              |
| `<br>`         | 代表换行符，常用于诗歌或地址。                                                                                                                              |
| `<wbr>`        | 代表文本中一个建议换行的位置，浏览器可以选择来换行，虽然它的换行规则可能不会在这里换行。 它可以避免过长的 URL 在标点(如 /)处换行，导致读者搞错 URL 的结尾。 |
| `<span>`       | 代表一段没有特殊含义的文本， 类似 `<div>`，在没有其它适合的文本语义元素时使用。                                                                             |

### 编辑标识

编辑标识元素用于标识出文本中被更改过的部分。

| 元素    | 描述                     |
| :------ | :----------------------- |
| `<ins>` | 代表增加到文档中的内容。 |
| `<del>` | 代表从文档中删除的内容。 |

### 嵌入内容

嵌入内容元素通常用于插入媒体内容，且嵌入内容通常是<a href="https://html.spec.whatwg.org/multipage/rendering.html#replaced-elements" target="_blank">可替换元素</a>。

| 元素       | 描述                                                                                                                                             |
| :--------- | :----------------------------------------------------------------------------------------------------------------------------------------------- |
| `<img>`    | 嵌入一张图片。                                                                                                                                   |
| `<map>`    | 与 `<area>` 一起使用来定义一个图像映射(一组可点击的链接区域)。                                                                                   |
| `<area>`   | 作为 `<map>` 的子元素使用，在图片上定义一个可关联超链接的可点击区域。                                                                            |
| `<iframe>` | 嵌入另一个 HTML 页面。                                                                                                                           |
| `<embed>`  | 嵌入由外部应用程序或交互式内容（插件）的提供支持的资源。 大多数现代浏览器已经弃用并取消了对浏览器插件的支持，因此依靠 `<embed>` 通常是不明智的。 |
| `<object>` | 嵌入外部资源的对象，使用此元素可在网页中嵌入多媒体（如 Flash）。类似 `<embed>` ， `<object>` 也是不可靠的。                                      |
| `<param>`  | 为 `<object>` 的资源对象定义参数。                                                                                                               |
| `<video>`  | 嵌入一段视频。                                                                                                                                   |  |
| `<audio>`  | 嵌入一段音频。                                                                                                                                   |
| `<source>` | 作为 `<video>` 或 `<audio>` 的子元素使用，以提供多个媒体资源，浏览器会使用第一个可用的资源。                                                     |
| `<track>`  | 作为 `<video>` 或 `<audio>` 的子元素使用，以提供基于时间的文本轨道（字幕）。                                                                     |
| `<canvas>` | 嵌入一张位图画布。                                                                                                                               |
| `<svg>`    | 嵌入一张矢量图。                                                                                                                                 |
| `<math>`   | 嵌入一段数学公式。                                                                                                                               |

### 表格内容

表格内容元素用于创建和处理表格数据。

| 元素         | 描述                                                                                            |
| :----------- | :---------------------------------------------------------------------------------------------- |
| `<table>`    | 定义了一个数据表格。                                                                            |
| `<caption>`  | 定义了表格的标题。常常作为 `<table>` 的第一个子元素。                                           |
| `<colgroup>` | 代表表格中的一组列，用于格式化列。置于表格内容之前。                                            |
| `<col>`      | 代表表格中的一列，通常置于 `<colgroup>` 中。                                                    |
| `<thead>`    | 定义了一组代表表格的表头的行。                                                                  |
| `<tbody>`    | 定义了一组代表表格内容的行，可以连续出现多次。如果使用了 `<thead>`，则 `<tbody>` 必须紧随其后。 |
| `<tfoot>`    | 定义了一组代表表格的汇总的行。                                                                  |
| `<tr>`       | 定义了表格的一行。表格行内只能使用 `<td>` 与 `<th>` 。                                          |
| `<td>`       | 定义了一个普通单元格。                                                                          |
| `<th>`       | 定义了一个表头单元格。                                                                          |

### 表单内容

表单元素用于创建一个用户可以填写并提交到服务器的表单。

| 元素         | 描述                                                                                                       |
| :----------- | :--------------------------------------------------------------------------------------------------------- |
| `<form>`     | 定义了一个表单。                                                                                           |
| `<fieldset>` | 定义了一组表单控件。                                                                                       |
| `<legend>`   | 定义了 `<fieldset>` 的标题。                                                                               |
| `<input>`    | 定义了一个输入控件。                                                                                       |
| `<label>`    | 定义了一个表单控件的描述说明。 将 `<label>` 与 `<input>` 结合使用，可以在点击 `<label>` 时触发 `<input>`。 |
| `<button>`   | 定义了一个按钮。                                                                                           |
| `<select>`   | 定义了一个下拉选项控件。需要结合 `<option>` 或 `<optgroup>` 使用。                                         |
| `<option>`   | 定义了一个选项。                                                                                           |
| `<optgroup>` | 定义了一组由 `<option>` 组成的选项。                                                                       |
| `<datalist>` | 定义了一组由 `<option>` 组成数据集，供 `<input list>` 使用。                                               |
| `<textarea>` | 定义了一个多行文本输入框。                                                                                 |
| `<progress>` | 定义了一个进度条控件。                                                                                     |

### 交互元素

交互元素有助于创建交互式用户界面对象。

| 元素        | 描述                                                   |
| :---------- | :----------------------------------------------------- |
| `<details>` | 代表一个用户可以通过点击来获取额外信息或控件的小部件。 |
| `<summary>` | 代表一个 `<details>` 的标题或是内容摘要。              |

## 结语

我作为一个切图仔的时日尚浅，关于 HTML 标准的理解可能也不尽正确。但是 HTML 是前端技术的基础，可以顺着 HTML 的知识延伸出 CSS、JavaScript 与 DOM 的技术。只要我梳理的的内容能够对你有所启发，帮助你更好地拓展自己的前端知识体系，那么我分享的目的就达到了。对于我自身而言，有了工作经验之后回过头来整理前端基础知识，也有温故而知新的意义。但愿我能战胜拖延症，后续能产出 _CSS 基础_ 与 _JavaScript 基础_ 。