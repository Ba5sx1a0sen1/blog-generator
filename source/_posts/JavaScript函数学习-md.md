---
title: JavaScript函数学习.md
date: 2018-02-24 13:32:29
tags:
    - JavaScript
---
1. 具名函数赋值
   ```JavaScript
         var f
         f = function f2(x,y){ return x+y }
         f.name // 'f2'
         console.log(f2) // not defined报错
   ```
2. `this`就是函数的`.call()`方法的第一个参数,在默认情况下(1)不传值与(2)给undefined,会转成`window`,
    在严格模式`user strict`则不会