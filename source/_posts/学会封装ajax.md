---
title: 学会封装ajax
date: 2018-03-09 14:34:48
tags:
- JavaScript
- AJAX
---
学会封装ajax，提炼出同样的代码来封装，给出两种实现方式：
    ```JavaScript
            window.myAjax.ajax = function(options){
                let {url,method,body,successFn,failFn,headers} = options //解构（析构）赋值
                let request = new XMLHttpRequest
                request.open(method,url)    //要先open才能设置请求头
                for(key in headers){
                    request.setRequestHeader(key,headers[key])
                }
                request.onreadystatechange=()=>{
                    if(request.readyState===4){
                        if(request.status >=200 && request.status<300){
                            successFn.call(undefined,request.responseText) //成功回调
                        }else if(request.status >= 400){
                            failFn.call(undefined,request) //失败回调
                        }
                    }
                }
                request.send(body)
            }
     ```
    ```JavaScript
        window.myAjax.ajax = function({url,method,body,headers}){
            //返回一个Promise对象，接收一个函数作为参数
            return new Promise(function(resolve,reject){
                let request = new XMLHttpRequest
                request.open(method,url)    //要先open才能设置请求头
                for(key in headers){
                    request.setRequestHeader(key,headers[key])
                }
                request.onreadystatechange=()=>{
                    if(request.readyState===4){
                        if(request.status >=200 && request.status<300){
                            resolve.call(undefined,request.responseText) //成功回调
                            }else if(request.status >= 400){
                               reject.call(undefined,request) //失败回调
                        }
                    }
                }
                request.send(body)
                //Promise链式调用的关键
            })
        }
    ```
