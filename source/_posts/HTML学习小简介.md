---
title: HTML学习小简介
date: 2018-02-07 13:59:07
categories: 前端
tags: 
    - HTML
---
## W3C是啥
> W3C是指万维网联盟（World Wide Web Consortium，W3C），又称W3C理事会，是万维网的主要国际标准组织
  W3C是由Tim Beners Lee（李爵士）于1994年离开CERN（欧洲核子研究中心）后成立的。

## MDN是啥
学前端你不知道MDN，那你完了，MDN是这个世界上除了[w3.org](https://www.w3.org)之外的最权威的前端技术文档，并且通俗易懂，学习前端开发，是不得不查MDN文档的，特别是涉及到Web API。
> MDN Web Docs（旧称Mozilla Developer Network、Mozilla Developer Center，简称MDN）是一个汇集众多Mozilla基金会产品和网络技术开发文档的免费网站，于2005年创立

## HTML的所有列表标签有那些呢？
HTML中提供的代码标签有有序列表，无序列表，描述列表，他们对应的代码形式分别如下
```
自定义列表

<dl>
    <dt>我是术语定义元素</dt>
    <dd>我是描述元素</dd>
</dl>

有序列表
<ol>
    <li>1</li>
    <li>2</li>    
</ol>

无序列表
<ul>
    <li>1</li>
    <li>2</li>
</ul>
```
## 什么是空标签（空元素）？

> 没有HTML内容的标签就是空标签，空标签只需要写一个开始标签,一个空元素（empty element）可能是 HTML，SVG，或者 MathML 里的一个不可能存在子节点（例如内嵌的元素或者元素内的文本）的element。

>在 HTML 中，通常在一个空元素上使用一个闭标签是无效的。例如，` <input type="text"></input> `的闭标签是无效的 HTML。

>以下元素是HTML中的空元素
`<area>` `<base>` `<br>` `<col>` `<colgroup>` `<command>` `<embed>`
`<hr>` `<img>` `<input>` `<keygen>` `<link>` `<meta>` `<param>`
`<source>` `<track>` `<wbr>`

## 可替换元素又是啥啥啥？

>CSS 里，可替换元素（replaced element）的展现不是由CSS来控制的。这些元素是一类 外观渲染独立于CSS的 外部对象。 典型的可替换元素有 `<img>`、 `<object>`、 `<video>` 和 表单元素，如`<textarea>`、 `<input>` 。 某些元素只在一些特殊情况下表现为可替换元素，例如 `<audio>` 和 `<canvas>` 。 通过 CSS content 属性来插入的对象 被称作 匿名可替换元素（anonymous replaced elements）。

>CSS在某些情况下会对可替换元素做特殊处理，比如计算外边距和一些auto值。

>需要注意的是，一部分（并非全部）可替换元素，本身具有尺寸和基线（baseline），会被像vertical-align之类的一些 CSS 属性用到。
