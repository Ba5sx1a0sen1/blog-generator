---
title: Javascript学习笔记
date: 2018-02-18 01:34:59
tags:
    - JavaScript
---

1. `switch`与`case`比较时采用的是严格相等运算符`===`,而不是相等`==`运算符,这意味着此时没有进行类型转换
2. 存在多层循环时,不带参数的`break`和`continue`语句都只针对最内层循环(需要结合`label`才能跳出多层)
3. 变量提升要记住
4. `vh`全称为`viewport height`
5. 获取页面的高度`var height = document.documentElement.clientHeight`
6. 获取页面的宽度`var width = document.documentElement.clientWidth` //不兼容IE
7. 深刻理解`null`与`undefined`,在`if`语句中,都会转变为`false`值,`==`时返回`true`,`===`时返回`false`
   > ```JavaScript
        Number(null) // 0
        5 + null // 5

        Number(undefined) // NaN
        5 + undefined // NaN
     ```
8. JS中有以下六个值在预期返回布尔值时转换为`false`,其他返回`true`
    > ```JavaScript
            undefined
            null
            false
            0
            NaN
            ""或''（空字符串）

            特例:
            []//true
            {}//true
      ```
9. `NaN`
    > ```JavaScript
        5 - 'x' //NaN
        
        0 / 0   //NaN

        Math.acos(2) // NaN
        Math.log(-1) // NaN
        Math.sqrt(-1) // NaN
        
        typeof NaN // 'number'
        
        NaN === NaN // false
        
        [NaN].indexOf(NaN) // -1

        Boolean(NaN) // false

        NaN + 32 // NaN
        NaN - 32 // NaN
        NaN * 32 // NaN
        NaN / 32 // NaN
      ```      
10. `infinity`是一种骚东西
11. `parseInt()`如果字符串的第一个字符不能转化为数字（后面跟着数字的正负号除外），返回`NaN`
    坑点:```JavaScript
                 对于那些会自动转为科学计数法的数字，parseInt会将科学计数法的表示方法视为字符串，因此导致一些奇怪的结果。

                parseInt(1000000000000000000000.5) // 1
                // 等同于
                parseInt('1e+21') // 1

                parseInt(0.0000008) // 8
                // 等同于
                parseInt('8e-7') // 8
        ```
12. `delete`用来删除对象的属性,无法删除继承而来的属性
13. `Object.keys()`方法用于查看对象本身的所有属性
14. `in`用于判断对象是否具备某一属性,`for...in`用于遍历一个对象的全部属性(包括继承属性)
15. 五个`falsy`: `''`,`Nan`,`undefined`,`null`,`0`