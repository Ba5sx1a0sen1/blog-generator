---
title: 啥是MVC
date: 2018-03-09 20:47:55
tags:
- JavaScript
- MVC
---
丢一张图：
![MVC](/images/MVC.png)

https://github.com/Ba5sx1a0sen1/resume

把个人简历全部用MVC封装了，这就很舒服，MVC是什么：如上图

MVC是按功能划分代码的思想，即M(Model)，V(View)，C(Controller)。分别为数据，视图，控制器，用户操作视图View，View通知控制器Controller，Controller去调用Model ，Model去请求Server；Server响应数据给Model，Model再返回数据给Controller，Controller再监听View去进行更新。View只跟Controller沟通，Controller负责和Model与View沟通，Model负责与Server和Controller沟通，但是View不直接与Model和Server沟通，Controller不直接与Server沟通。