---
title: Javascript学习笔记
date: 2018-02-18 01:34:59
tags:
    - JavaScript
---

1. `switch`与`case`比较时采用的是严格相等运算符`===`,而不是相等`==`运算符,这意味着此时没有进行类型转换
2. 存在多层循环时,不带参数的`break`和`continue`语句都只针对最内层循环(需要结合`label`才能跳出多层)
3. 变量提升要记住