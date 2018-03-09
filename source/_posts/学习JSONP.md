---
title: 学习JSONP
date: 2018-03-06 20:19:03
tags:
    - JSON
---
### JSONP是什么？
1. 请求方动态创建一个`<script>`标签，`src`属性指向响应方，同时传一个查询参数如`?callbackName=xxx`
2. 响应方根据查询参数callbackName，构造形如
    1. xxx.call(undefined,'需要的数据')
    2. xxx.call('需要的数据')
3. 浏览器方接收到响应，就会执行`xxx.call(undefined,'你要的数据 ')`
4. 那么请求方就知道了他要的数据

这就是JSONP

### 行业的约定：
1. callbackName -> callback
2. xxx -> 随机数 xxx随机数

即回调函数的查询参数名称是`callback`，调用的函数名是结合随机数动态生成创建后调用再删除的，jQuery的jsonp方法便是采用这样的约定实现的

### JSONP 为什么不支持 POST

1. 因为jsonp是通过动态创建script标签实现的
2. 动态创建script的时候只能使用get，无法使用post
