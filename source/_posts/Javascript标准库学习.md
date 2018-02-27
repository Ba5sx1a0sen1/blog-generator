---
title: Javasctipt标准库学习
date: 2018-02-23 13:48:58
tags:
    - Javascript
---
### Array

1.  Array的构造函数
    ```JavaScript
        var a = Array(3) // a = [,,]
        var a = Array(3,3) // a = [3,3]
        体现了API的不一致性
        在Array前加new与不加new都一样,因为Array属于复杂数据类型,所以加new与不加都一样效果,
        而基本数据类型Number,String,Boolean,加不加new就不一致
        所以,Function,Object都与Array类似
    ```
2. 数组的实例方法上,会改变数组本身的有`pop()`,`push()`,`shift()`,`unfshift()`,`reverse()`,
    `splice()`,`sort()`;
    不改变原来数组的有`join()`,`concat()`,`slice()`,`map()`,`forEach()`,`filter()`,`some()`,
    `every()`,`reduce() reduceRight()`,`indexOf()`,`lastIndexOf()`