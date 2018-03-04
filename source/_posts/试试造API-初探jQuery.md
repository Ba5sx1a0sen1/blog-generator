---
title: '试试造API,初探jQuery'
date: 2018-02-27 20:38:17
tags:
    - JavaScript
    - DOM
    - API
---

### HTML代码
今天学习的时候是学习自己去封装API,先装逼写出ul>li#item${选项$}*5然后按下`tab`,我们的HTML代码就出来啦
```HTML
    <!DOCTYPE html>
    <html>
    <head>
    <meta charset="utf-8">
    <title>xxx</title>
    </head>
    <body>
    <ul>
        <li id="item1">选项1</li>
        <li id="item2">选项2</li>
        <li id="item3">选项3</li>
        <li id="item4">选项4</li>
        <li id="item5">选项5</li>
    </ul>
    </body>
    </html>
```
展示出来的效果如图所示![](/images/testjq-html.png)

### 初尝试
http://js.jirengu.com/xahoyeheja/1/edit?html,js,output
好了HTML代码写好了我们来造API吧,我们的需求是给这五个`li`的任意其中一个找出他的所有兄弟姐妹,还有就是为一个`li`添加class,那我们就上我们的第一版js代码
```JavaScript
    //获取节点的兄弟姐妹但不包括自己
    function getSiblings(node){
        var allChild = node.parentNode.children
        var array = {length:0}
        for(let i = 0; i<allChild.length; i++){
            if(allChild[i] !== node){
            array[array.length] =allChild[i];
            array.length++
            }
        }
        return array
    }

    function addClass(node,classes){
        for(let key in classes){
            var value = classes[key]
            var methodName = value?'add':'remove'
            node.classList[methodName](key)
        }
    }

    window.ssdom = {} //命名空间,仿照dom操作放在Document上,用来装逼,说是自己写的库,让别人知道库名和防止变量冲突,知名的雅虎的YUI库就是这么实现的
    ssdom.getSiblings = getSiblings
    ssdom.addClass = addClass

    ssdom.getSiblings(item2)
    ssdom.addClass(item3,{'a':true,'b':false})
```
这个代码里面我们在window上声明了一个叫做ssdom的对象,用来把我们的API扔进去,这玩意就叫命名空间,可以当做是一个库名,并防止变量冲突

### 再试试能不能挂载到元素上,让元素调用
http://js.jirengu.com/xufanibobe/1/edit?js,output
上面的代码我们其实是实现了造API的功能,但是呢,我们能不能把API直接给元素调用,而不用我们把元素节点传进去?答案是可以的,
我们便改造以下代码出来
```JavaScript
    Node.prototype.getSiblings = function(){
        var allChild = this.parentNode.children
        var array = {length:0}
        for(let i = 0; i<allChild.length; i++){
            if(allChild[i] !== this){
            array[array.length] =allChild[i];
            array.length++
            }
        }
        return array
    }

    Node.prototype.addClass= function(classes){
        for(let key in classes){
            var value = classes[key]
            var methodName = value?'add':'remove'
            this.classList[methodName](key)
        }
    }

    console.log(item1.getSiblings.call(item1))
    //相当于item1.getSiblings()
    item3.addClass.call(item3,{'a':true,'b':true})
    //相当于与item3.addClass({'a':true,'b':true})
```
这样做又有个弊端,原型上不小心写同名的函数又会覆盖,所以又回到类似命名空间的场景,而且,js代码很不推荐直接在原型上添加方法,这种做法是十分危险的

### 那能不能做的更好?
我们可以采取另一种封装方式,直接上我们的代码
```JavaScript
    window.Node2 = function(node){
        return {
            getSiblings(){
                var allChild = node.parentNode.children
                var array = {length:0}
                for(let i = 0; i<allChild.length; i++){
                    if(allChild[i] !== node){
                    array[array.length] =allChild[i];
                    array.length++
                    }
                }
                return array
            },
            addClass(classes){
                for(let key in classes){
                    var value = classes[key]
                    var methodName = value?'add':'remove'
                    node.classList[methodName](key)
                }
            }
        }  
    }

    node2 = Node2(item3)
    console.log(node2.getSiblings())
```
这样的封装方式,是很不错的,我们只要传入一个节点参数,然后返回一个方法对象用于操作这个节点,把我们这个方法名Node2改成jQuery,就能理解jQuery内部大致就是这样实现,返回给你一个对象,并附带api给你调用

但是现在还长得不像jQuery,jQuery可以通过选择器找到节点,我们能不能再进一步优化我们的代码做的更像jQuery呢?我们的改动如下

### 改的像jQuery
http://js.jirengu.com/jucutasaku/1/edit?js,output
我们可以采取另一种封装方式,直接上我们的代码
```JavaScript
    window.jQuery = function(nodeOrSelector){
        let node
        typeof nodeOrSelector === 'string' 
        ? node = document.querySelector(nodeOrSelector)//这API很棒,兼容到IE8,但是在IE8下只能支持css2.1的选择器
        : node = nodeOrSelector
        return {
            getSiblings(){
                var allChild = node.parentNode.children
                var array = {length:0}
                for(let i = 0; i<allChild.length; i++){
                    if(allChild[i] !== node){
                    array[array.length] =allChild[i];
                    array.length++
                    }
                }
                return array
            },
            addClass(classes){
                for(let key in classes){
                    var value = classes[key]
                    var methodName = value?'add':'remove'
                    node.classList[methodName](key)
                }
            }
        }  
    }

    node2 = jQuery('item3')
    console.log(node2.getSiblings())
```
我们只需要使用Queryselector这个方法去模拟获取选择器,就很不错了,目前高版本的jquery也已经舍弃对低版本的ie的支持,jQuery的1.7版本兼容到ie7,这里我们不考虑如何做到兼容性更好,所以我们可以这么说,jQuery实质是一个构造函数,接收一个参数,这个参数可能是节点,然后返回一个方法对象去操作节点


### 虽然支持选择器,但是只能找到单个元素节点啊?
http://js.jirengu.com/gahamemece/1/edit?html,js,output
然而,需求又变得变态了,如果我想同时操作多个节点,怎么搞?上面的代码明显变得不行了,我们得重新写让他能支持多节点操作,上面的代码只支持单节点操作啊,原因就在于我们使用的是`querySelector`这个API,我们只要改进为`querySelectorAll`即可
```JavaScript
    window.jQuery = function(nodeOrSelector){
        let nodes = {}
        if(typeof nodeOrSelector === 'string'){
            let temp = document.querySelectorAll(nodeOrSelector) //伪数组
            for(let i=0;i<temp.length;i++){
                nodes[i] = temp[i]
            }
            nodes.length = temp.length
        }else if(nodeOrSelector instanceof Node){
            nodes = {
                0:nodeOrSelector,
                length:0
            }
        }
  
        nodes.addClass = function(classes){
            for(let key in classes){
                var value = classes[key]
                var methodName = value?'add':'remove'
                for(let i=0;i<nodes.length;i++){
                    nodes[i].classList[methodName](key)
                }
            }
        }
  
        nodes.getTexts = function(){
            let texts = []
            for(let i = 0;i<nodes.length;i++){
                texts.push(nodes[i].textContent)
            }
            return texts
        }
  
        nodes.setTexts = function(text){
            for(let i = 0;i<nodes.length;i++){
                nodes[i].textContent = text
            }
        }
  
        nodes.text = function(text){
            if(text === undefined){
            let texts = []
            for(let i = 0;i<nodes.length;i++){
                texts.push(nodes[i].textContent)
            }
                return texts
            }else{
                for(let i = 0;i<nodes.length;i++){
                    nodes[i].textContent = text
                }
            }
        }
  
        return nodes;
    }

    var nodes2 = jQuery('ul > li')
    nodes2.addClass({'blue':true})
    console.log(nodes2.getTexts())
    nodes2.setTexts('hihi')
    console.log(nodes2.getTexts())
```