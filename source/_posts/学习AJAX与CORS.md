---
title: 学习AJAX与CORS
date: 2018-03-07 08:41:42
tags: 
- JavaScript
---
今天写了两个前后端通讯的小的demo，后端主要使用node来做简单的服务器响应，前端非常简单只是用于研究获取数据的方式：
1. `JSONP` https://github.com/Ba5sx1a0sen1/node-jsonp
2. `AJAX` 结合CORS https://github.com/Ba5sx1a0sen1/node-ajax

两种方式对比：
1. `JSONP`上一篇文章已经提到过，`JSONP`方式前端动态创建一个`<script>`标签，然后`src`属性指向另一个源的接口，然后接口只要返回一串`JavaScript`代码调用前端的函数
2. `AJAX -CORS`，是现代前端使用的与后端通讯的重要方法，AJAX有四句话相当重要，如下：
    ```JavaScript
        let request = new XMLHttpRequest //声明一个xmlhttprequest对象
        request.onreadystatechange=()=>{} //响应成功后相关的处理函数
        request.open('GET','/xxx')    //重要API，用于设置方法与接口路径
        request.send() //重要API，可传入HTTP第四部分需要的数据，另有一个方法可以设置HTTP第二部分的key-value值：setRequestHeader()
    ```
    
CORS是什么，CORS的全称是Cross-Origin Resource Sharing，翻译为中文意思为跨域资源共享。同源安全策略( same-origin security policy)默认禁止“跨域”请求. CORS 给予Web服务器跨域访问控制, 启用安全的跨域数据传输。

即只需要我们在后端代码中设置允许前端的访问的源网站地址，在node中的设置方法为如下：
    ```JavaScript
        response.setHeader('Access-Control-Allow-Origin','http://localhost:8888')
    ```
上面这句代码的用处是在服务端设置对地址为`http://localhost:8888`放通访问控制，让该地址可以调用到该异源的接口获取数据，这边是大家口口声声中说的CORS CORS CORS

