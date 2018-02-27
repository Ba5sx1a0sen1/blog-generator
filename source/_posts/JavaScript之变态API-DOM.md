---
title: JavaScript之变态API-DOM
date: 2018-02-25 14:40:20
tags:
    - DOM
---
### DOM是啥玩意?
DOM全称叫做Document Object Model,老是听人说dom树dom树到底是什么?
document和object之间的映射关系就是model,形成了一棵树

### DOM的元素对象
看以下代码
```HTML
    <!Doctype html>
    <html lang='zh-Hans'>
        <head>
        </head>
        <body>
            <h1>hahaha<!--aaa--></h1>
        <body>
    </html>    
```
这个简单的例子中有三种节点对象,分别是Element,Text,Document,Comment,都继承于顶层Node对象,
Document是最牛逼最顶层的,指代的是html文档最顶层的`html`对象

### DOM的child相关API
`.childNodes`属性是返回子节点的集合,`.children`则返回的是子**标签**的集合
`firstChild`返回的是第一个节点,是由Node对象提供的;`firstElementChild`返回的是第一个子标签,由Element对象提供
`lastChild`,`lasttElementChild`

### DOM的sibling相关API
`nextSibling`,`previousSibling`返回相邻的节点,`nextElementSibling`,`previousElementSibling`返回相邻的标签

### nodeType,nodeValue,nodeName
Node.Element_Node == 1 表示元素的nodeType == 1
Node.Text_Node == 3 表示文本节点的nodeType == 3
Node.Comment_Node == 8 表示注释节点的nodeType == 8

### parentNode,parentElement
一个返回节点,一个返回元素,如果不存在则返回`null`

### innerText,textContent的区别看这篇文章
https://developer.mozilla.org/zh-CN/docs/Web/API/Node/textContent

### Node接口提供的方法
`appendChild()`,参数为节点,可以是ElementNode和TextNode
`cloneChild()`,接收一个参数`true`或者`false`,进行深拷贝还是浅拷贝,在最新标准中是缺省默认值是`false`
`contains()`,接收一个节点做参数,判断是否被包含,返回`true`或`false`
`hasChildNodes()`,判断是否有子节点,返回`true`或者`false`
`insertBefore()`,插入节点,接收两个参数,一个是新插入节点,一个是用于相对插入当前节点的后一个节点
`isEqualNode()`,`isSameNode()`
`removeChild()`,接收一个节点参数,用于删除子节点
```JavaScript
    // 先定位父节点,然后删除其子节点
    var d = document.getElementById("top");
    var d_nested = document.getElementById("nested");
    var throwawayNode = d.removeChild(d_nested);

    // 无须定位父节点,通过parentNode属性直接删除自身
    var node = document.getElementById("nested");
        if (node.parentNode) {
        node.parentNode.removeChild(node);
    }

    // 移除一个元素节点的所有子节点
    var element = document.getElementById("top");
        while (element.firstChild) {
        element.removeChild(element.firstChild);
    }
```
`replaceChild()`,接收两个参数,用于替换子节点


### Document提供的部分接口
以下是个人认为应用场景多的,需要牢记的,还需记住那些属性是只读的,是可改的,那些API是访问器还是修改器
完整的请参考 https://developer.mozilla.org/zh-CN/docs/Web/API/Document
1. 属性:
   1. `document.documentElement` 对于HTML 文档来说，返回的一般是 HTML 元素。
   2. `document.anchor` 返回当前 document 的所有的锚点的列表
      > 由于向后兼容的原因,该属性只返回那些拥有name属性的a元素,而不是那些拥有id属性的a元素.
   3. `Document.body` 返回当前文档的 `<body>` 元素.
   4. `Document.cookie` 返回文档的由分号分隔的cookie列表，或者设置一个单独的cookie值.
      https://developer.mozilla.org/zh-CN/docs/Web/API/Document/cookie
   5. `Document.forms ` 返回当前文档中的`<form>`元素列表,是一个集合
   6. `Document.head`   返回当前文档的`<head>`元素
   7. `Document.images` 返回当前文档的图像列表,也是集合,伪数组
   8. `Document.links` 返回文档中所有超链接的列表
   9. `Document.location` 返回当前文档的URI
   10. `Document.title` 设置或获取当前文档的标题
   11. `Document.URL` 返回文档的地址字符串
   12. `Document.characterSet` 返回文档使用的字符集。
   13. `ParentNode.childElementCount` 返回一个无符号长整型，给出对象含有的后代数量
   14. `Document.doctype` 返回当前文档的 Document Type Definition (DTD)。
   15. `Document.domain` 获取/设置当前文档的原始域部分, 用于同源策略.
   16. `Document.referrer` 返回着链接到当前页面的那个页面的 URL
   17. `Document.scripts` 返回文档中所有的`<script>`元素
   18. `Document.scrollingElement` 返回滚动 document 的 Element 的一个引用。 
   19. `Document.styleSheets` 返回当前 document 的样式表对象的列表。
2. 方法:
   1. `Document.close()` 关闭文档写入流.
   2. `Document.open()` 打开文档写入流.
   3. `document.write()` 将一个文本字符串写入由 document.open() 打开的一个文档流。
    > 注意: 因为 document.write 写入文档流，在关闭(已加载)的文档上调用 document.write 会自动调用              document.open，这将清除该文档。
   4. `document.writeln()` 向文档中写入一串文本，并紧跟着一个换行符。
   5. 创建相关API:
        1. `Document.createDocumentFragment()` 创建一个新的文档片段
        2. `Document.createElement()` 用给定的标签名创建一个新的元素
        3. `Document.createComment()` 创建一个新的注释节点并返回它
        4. `Document.createTextNode()` 创建一个文字节点
   6. 查询获取类相关API:
        1. `getElementById()`
        2. `getElementsByClassName()`
        3. `getElementsByName()`
        4. `getElementsByTagName()`
        5. `getSelection()` 返回文档中与选中文本相关的Selection对象.
        6. `querySelector()`
        7. `querySelectorAll()`
   7. `Document.hasFocus()` 如果焦点在当前指定的文档的内部,返回 true .

### Element提供的接口
1. 属性:
    - `Element.attributes` 返回一个与该元素相关的所有属性集合
    - `Element.classList` 返回该元素包含的class属性 具备`add()`,`remove()`,`item()`,`toggle()`,`contain()`方法
    - `Element.className` 表示当前元素的class属性的值,可以是由空格分隔的多个class属性值. 
    - `Element.clientHeight` 返回Number 表示内部相对于外层元素的高度
        ![clientHeight](https://developer.mozilla.org/@api/deki/files/185/=Dimensions-client.png)
    - `Element.clientWidth` 返回Number 表示该元素它内部的宽度.
    - `Element.clientLeft` 返回Number表示该元素距离它左边界的宽度.
    - `Element.clientTop` 返回 Number 表示该元素距离它上边界的高度
    - `Element.id` 返回这个元素的id字符串.
    - `Element.innerHTML` 是一个DOMString 表示这个元素的内容文本
    - `Element.scrollHeight`  这个只读属性是一个元素内容高度的度量，包括由于溢出导致的视图中不可见内容。没有垂直滚动条的情况下，scrollHeight值与元素视图填充所有内容所需要的最小值clientHeight相同。包括元素的padding，但不包括元素的border和margin。scrollHeight也包括 ::before 和 ::after这样的伪元素。
        ![scrollHeight](https://developer.mozilla.org/@api/deki/files/840/=ScrollHeight.png)
    - `Element.scrollLeft` 可以读取或设置元素滚动条到元素左边的距离。
    - `Element.scrollTop` 可以获取或设置一个元素的内容垂直滚动的像素数。即滚动了多少的像素数
        ![scrollTop](https://developer.mozilla.org/@api/deki/files/842/=ScrollTop.png)
    - `Element.scrollWidth` 返回类型为： Number ，表示该滚动窗口的宽度 若元素的宽度大于其内容的区域（例如，元素存在滚动条时）, scrollWidth的值要大于clientWidth
    - `Element.TagName` 返回类型为：String，表示该元素的标签名,除了`<svg>`其余都以大写形式返回
2. 方法:
    - 继承自`EventTarget`的方法
        https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget
        1. `EventTarget.addEventListener()` 在EventTarget上注册特定事件类型的事件处理程序。
        2. `EventTarget.removeEventListener()` EventTarget中删除事件侦听器。
        3. `EventTarget.dispatchEvent()` 将事件分派到此EventTarget。
    - `Element.getAttribute()` 返回元素上一个指定的属性值。如果指定的属性不存在，则返回  null 或 "" （空字符串）
        > let attribute = element.getAttribute(attributeName);
    - `Element.getBoundingClientRect()` 返回元素的大小及其相对于视口的位置,返回一个[DOMRect](https://developer.mozilla.org/zh-CN/docs/Mozilla/Tech/XPCOM/Reference/Interface/nsIDOMClientRect)对象,DOMRect 对象包含了一组用于描述边框的只读属性——left、top、right和bottom，单位为像素。除了 width 和 height 外的属性都是相对于视口的左上角位置而言的。
        ![DomRect](https://mdn.mozillademos.org/files/15087/rect.png)
    - `Element.getElementsByClassName()` 
    - `Element.getElementsByTagName()`
    - `Element.hasAttribute()` `var result = element.hasAttribute(attName);`  返回一个布尔值，指示该元素是否包含有指定的属性（attribute）
    - `Element.querySelector()`
    - `Element.querySelectorAll()` 返回一个[NodeList](https://developer.mozilla.org/zh-CN/docs/Web/API/NodeList)
    - `ChildNode.remove()` 把一个节点从它所属的DOM树中删除 
        语法:
        > 
            ```JavaScript
                elementNodeReference.remove(); 
            ```
    - `element.removeAttribute()`  从指定的元素中删除一个属性。
    - `Element.removeAttributeNode()` removeAttributeNode 从当前的 element(元素节点) 删除指定的属性
    - `Element.setAttribute()` 设置指定元素上的一个属性值。如果属性已经存在，则更新该值; 否则将添加一个新的属性用指定的名称和值.要获取属性的当前值，使用 getAttribute(); 要删除一个属性，调用removeAttribute()。
        > element.setAttribute(name, value);

### 简单的看一下HTMLElement
https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement
1. `HTMLElement.offsetHeight` 返回该元素的像素高度，高度包含该元素的垂直内边距和边框，且是一个整数。
2. `HTMLElement.offsetWidth` 返回一个元素的布局宽度。一个典型的offsetWidth是测量包含元素的边框(border)、水平线上的内边距(padding)、竖直方向滚动条(scrollbar)（如果存在的话）、以及CSS设置的宽度(width)的值。
    ![offset](https://developer.mozilla.org/@api/deki/files/186/=Dimensions-offset.png)
    ![client](https://developer.mozilla.org/@api/deki/files/185/=Dimensions-client.png)
    ![scroll](https://developer.mozilla.org/@api/deki/files/840/=ScrollHeight.png)
3. `HTMLElement.offsetParent` 元素的父元素，如果没有就是body元素
4. `HTMLElement.offsetLeft` 返回当前元素左上角相对于`HTMLElement.offsetParent`节点的左边界偏移的像素值
5. `HTMLElement.offsetTop` `HTMLElement.offsetTop`为只读属性，它返回当前元素相对于其`offsetParent`元素的顶部的距离。
