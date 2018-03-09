---
title: AJAX离不开HTTP
date: 2018-03-07 15:54:09
tags:
- JavaScript
---
## HTTP与AJAX
AJAX是用于前端发起请求，请求的格式都是以HTTP请求发起，所以AJAX是离不开HTTP的，而HTTP中，请求与响应我又理解为有四部分，请求有：请求头 key-value 回车 带参数，响应有：响应头 key-value 回车 带参数

## AJAX中与HTTP相关的API
在nodejs服务端中，设置响应头的方法使用`response`的`setHeader()`方法，在前端ajax中，即客户端，同样可以使用API设置请求头，这类ajax设置http的API有不少，从mdn查阅有如下

1. HTTP请求相关
    第一部分：`open(method,url,asyncBollean)`，设置请求的第一部分，方法与路径
    第二部分：`setRequestHeader('content-type','application/x-www-form-urlencoded')`，设置第二部分的`key-value`
    第四部分: `send('a=1&b=2')`，设置第四部分的内容`body`
    ```
        GET /xxx HTTP/1.1
        HOST: ccc.com:8888
        Content-type: application/x-www-url-encoded

        a=1&b=2
    ```

    不管是响应还是请求，第四部分永远都是字符串

2. HTTP响应部分（只限于获取）
    第一部分：`request.status`/`request.statusText` 前一个的类型是`unsigned short`（`200`），后一个返回`DOMString`(`'200 OK'`)
    第二部分：`getResponseHeader('content-type')` / `getAllResponseHeaders`
    第四部分：`requese.responseText` 拿到响应体(`body`)的内容