---
title: jQueryApi学习记录
date: 2018-03-15 09:33:02
tags:
- jQuery
---
### `.index()`
> 是一个方法有三种用法，1. .index() 2. .index(selector) 3. .index(element)
> 用于返回在同辈元素中的索引

### `.eq()`
> 可接收正整数或负整数做参数，用于匹配元素的集合为指定的索引的某一元素

### `.each(function(index,element))`
> 遍历一个jQuery对象，为每个匹配的元素执行一个函数

### `.find()`
> 返回匹配当前元素的后代元素的集合，不同于`.children()`只返回子元素
> 1. .find(selector) 2. .find(jQuery Obj) 3. .find(element)

### `.children()`
> `.children([selector])`

### `.hover()`
> 绑定两个回调函数在该方法上，分别当指针进入和离开元素时执行
> 调用`$(selector).hover(handlerIn,handlerOut)`，`$(selector).mouseenter(handlerIn).mouseleave(handlerOut)`的简写

### `.filter()`
> 筛选元素集合中匹配表达式的元素，有时会传递回调作为参数测试哪些元素匹配

### `.first()` `.last()`
> 获取匹配元素集合中的第一个元素，最后一个元素

### `.css()`
> 用于设置css属性，可接收一个哈希或者一对键值对

### `.end()`
> 终止当前的链式操作，并返回匹配元素**之前**的状态，要记住是之前的状态

### `.addClass()`和`.removeClass()`
> 顾名思义

### `.remove()`
> 移除元素

### `.empty()`
> 将匹配元素的内容置空

### `.append()`与`.prepend()`,`.before()`,`.after()`,`.insetBefore()`,`.insertAfter()`
> 追加节点

### `.change()`
> 类似`onchange`事件

###`.html()`
> 获取集合中的第一个匹配的元素的html内容或设置每一个匹配元素的html内容

### `.text()`
> 得到匹配元素集合中每个元素合并的文本，或设置匹配元素中每个元素的文本内容为指定内容

### `.offset()`
> 在匹配的元素集合中，获取第一个元素的当前坐标。或设置元素集合中每一个元素的坐标。可用于暂停状态，hide()与show()

### `.one()`
> 为元素的事件添加处理函数。处理函数在每个元素上每种事件类型执行的次数最多一次

### `.siblings([selector])`
> 返回匹配元素集合中每个元素的兄弟元素，可提供一个可选的选择器
