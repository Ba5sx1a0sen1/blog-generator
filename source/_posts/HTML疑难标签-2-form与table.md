---
title: HTML疑难标签(2)-form与table
date: 2018-02-08 01:11:45
tags: 
    - HTML
---
## form
可以这么说，`a`标签发起的请求是get请求，由`form`发起的请求是post请求，`method`一般为post，不会无聊到使用`get`，而`action`也仅仅只是路径而已，路径而已，路径而已。

当`form`里有数据填充并发送时，浏览器会以http格式`content-type:x-www-form-urlencoded`拼凑数据并加到http请求的第四部分。

如果没有提交按钮，你是无法提交你的表单的，所以一定要有提交按钮，除非你使用js进行提交，如果是`GET`请求，不会把数据参数填充到第四部分，而是带到查询参数上，这就很不好，`POST`默认没有查询参数，但是可以预先在`action`写好。

巨坑：如果`form`里面没有提交按钮如`<input type="submit">`，则其中的一个`<button>submit</button>`，自动升级为提交按钮。

`<label for="xxx">用户名</label><input type="text" name="username" id="xxx">`
老司机写法：`<label>用户名<input type="text" name="username"></label>`

默认`checkbox`选中提交的值是`on`,可以在`value`属性自定义值。`radio`类似。

`select`：`name`,`disabled`,`selected`,`multiple`

`textarea`:`name`,`resize:none`,`col="30"`,`row="10"`

## table
在HTML中规定，`<table>`标签里只能有三个子标签分别是：`<thead>`,`<tbody>`,`<tfoot>`。
三个子标签的顺序任意摆放浏览器会自动纠正
在以上三个子标签中，都可以写`<tr>`用来开一行,在`<tr>`中可以开多个`<td>`填充数据。
一般在`thead`中使用`<th>`表示表头

```HTML
<colgroup>
    <col width=100>
    <col bgcolor=red width=200>
    <col width=300>    
</colgroup>
```

`border=1`:展示表格边框，如果需要将边框合并则在样式中编写`border-collapse:collapse;`
