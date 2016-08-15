---
layout:     post
title:      用CSS3绘制圆弧
description: 用CSS3绘制圆弧
categories: blog
tag: html css3
---

在w3cfuns前端网上看到了css3制作的加载loading，<a target="_blank" href="http://www.w3cfuns.com/notes/28003/56008504355cf20cfaa08dcc022b6e25.html">传送门</a>

记录下用css3制作圆弧的方法。

1、简单的方法：

可绘制不同方向的90度、180度、270度小圆弧，90度的大圆弧

代码：

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<title></title>
	<style>
		.borderArc {
			width: 200px;
			height: 200px;
			border: 6px solid transparent;
			border-top: 6px solid #ccc;
			border-radius: 50%;
		}
		.borderArc2 {
			width: 200px;
			height: 200px;
			border: 6px solid #ccc;
			border-bottom-color: transparent;
			border-radius: 50%;
		}
        .borderArc3 {
            width: 200px;
            height: 200px;
            border: 6px solid transparent;
            border-left: 6px solid #ccc;
            border-radius: 100% 0 0 0;
        }
	</style>
</head>
<body>
	<div class="borderArc"></div>
	<div class="borderArc2"></div>
  	<div class="borderArc3"></div>
</body>
</html>
```
效果图：
![img](/images/blog/arc.png)


2、使用clip()、rect()的方法绘制不同角度的圆弧

代码

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<title></title>
	<style>
		.arc {
			position: fixed;
			width: 220px;
			height: 220px;
			background-color: transparent;
			border-radius: 50%;
			border: 6px solid transparent;
		}
		.arc:before {
			content: "";
			display: block;
			position: absolute;
			top: -6px;
			left: -6px;
			width: 220px;
			height: 220px;
			border: 6px solid #ccc;
			border-radius: 50%;
			transform: rotate(230deg);
			clip: rect(60px, 232px, 172px, 100px);
		}
		.arc:after {
			content: "";
			display: block;
			position: absolute;
			top: -6px;
			left: -6px;
			width: 220px;
			height: 220px;
			border: 6px solid #ccc;
			border-radius: 50%;
			transform: rotate(120deg);
			clip: rect(80px, 232px, 152px, 100px)
		}
	</style>
</head>
<body>
	<div class="arc"></div>
</body>
</html>
```
效果图：
![img](/images/blog/arc2.png)

