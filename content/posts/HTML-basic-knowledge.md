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

HTML5 实际上是一组用于构建更多样化和更强大的应用程序的技术集合。（不知为何，中文语境中的 H5 常常指移动端的 HTML 页面 🤔）本文会简单地介绍一下 HTML5 包含的技术集，然后详细的阐述常用的 HTML 元素。

HTML5 包含以下几个内容：

- **语义** ：能够让你更恰当地描述你的内容是什么。
- **连通性** ：能够让你和服务器之间通过创新的新技术方法进行通信。
- **离线 & 存储** ：能够让网页在客户端本地存储数据以及更高效地离线运行。
- **多媒体** ：使 video 和 audio 成为了在所有 Web 中的一等公民。
- **2D/3D 绘图 & 效果** ：提供了一个更加分化范围的呈现选择。
- **性能 & 集成** ：提供了非常显著的性能优化和更有效的计算机硬件使用。
- **设备访问 Device Access** ：能够处理各种输入和输出设备。
- **样式设计** ：让作者们来创作更加复杂的主题吧！

## 语义

HTML5 提供了新的语义化文档的元素，如 `article`、`header`、`footer` 等。

## 连通性

Web Sockets 允许页面和服务器建立持久的连接，同时进行双向通信。

Server-sent events 允许页面监听服务器推送的事件，进行服务器到页面的单向通信。

<abbr title="Web Real-Time Communication">WebRTC</abbr> 允许页面与页面之间建立连接，实现即时通信。
