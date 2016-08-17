---
layout:     post
title:      HTML5 Canvas 学习笔记
description: 关于Canvas中常用的API接口方法介绍
categories: blog
tags: canvas html5
---

在维基百科中的描述中，Canvas元素是HTML5的一部分，允许脚本语言动态渲染位图像。

以下为学习慕课网上Canvas绘图详解课程总结的笔记

传送门：[ http://www.imooc.com/learn/185](http://www.imooc.com/learn/185) 

感谢老师的详解！

### 在HTML中使用Canvas

HTML

```html
<canvas id="canvas"></canvas>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

<!-- {% highlight html linenos %}
<canvas id="canvas"></canvas>
{% endhighlight %} -->

JavaScript

```javascript
var canvas = document.getElementById('canvas');       //获取canvas的dom节点
var context = canvas.getContext('2d');                //获取canvas的上下文环境

//使用上下文环境进行绘制
//......
context.xx
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

tips: Canvas是基于状态绘制图形

Canvas绘制接口API笔记 ( w3school )：

- Canvas绘制环境设定
  - context.beginPath( )      // 在一个画布中开始子路径的一个新集合
  - context.closePath( )      // 关闭当前打开的子路径
  - context.save( )              // 保存 CanvasRenderingContext2D 对象的属性、剪切区域和变换矩阵。
  - context.restore( )         // 为画布重置为最近保存的图像状态。通常与 save（）成对出现
- 绘制一条直线
  - context.moveTo( x, y )    //把当前的位置移动到一个新的位置而不添加一条连接线段
  - context.lineTo( x, y )       //为当前子路径添加一条直线
  - context.lineWidth = num      // 线条宽度
  - context.strokeStyle             // 线条样式

代码   

```javascript
var canvas = document.getElementById('canvas');

canvas.width = 800;        //设置canvas画布的宽度
canvas.height = 800;       //设置canvas画布的高度

var context = canvas.getContext('2d');

context.moveTo(100, 100);
context.lineTo(700, 700);
context.stroke();             //绘制
```


效果图
 ![img](/images/upload/canvas/canvas_1.png)

给直线加样式宽度

```javascript
var canvas = document.getElementById('canvas');

canvas.width = 800;        //设置canvas画布的宽度
canvas.height = 800;       //设置canvas画布的高度

var context = canvas.getContext('2d');

context.moveTo(100, 100);
context.lineTo(700, 700);
context.lineWidth = 10;
context.strokeStyle = '#f05';
context.stroke();             //绘制
```

![img](/images/upload/canvas/canvas_2.png)

-  线与线之间的连接
  - context.lineCap = butt[ default ] / round / square ( 只用于图形的开始处和结尾处，不能用于连接处 )
  ![img](/images/upload/canvas/canvas_3.png)
  -  context.lineJoin = miter[ default ] / bevel / round   【绘制交点】
    - miter：说明了两条线段的外边缘一直扩展到它们相交。当设置这个值时，还可设置miterLimit的值
    ![img](/images/upload/canvas/canvas_4.png)
    - round：顶点的外边缘应该和一个填充的弧接合，这个弧的直径等于线段的宽度。
    - bevel：顶点的外边缘应该和一个填充的三角形相交。
  ![img](/images/upload/canvas/canvas_5.png)
- 填充
  - context.fillStyle = color / gradient / img / canvas / video
  - context.fill( ) 使用指定颜色、渐变或模式来绘制或填充当前路径的内部。
- 绘制一个矩形
  - context.rect ( x, y, width, height )
  - context.fillrect ( x, y, width, height )
  - context.strokeRect ( x, y, width, height )

代码：

```javascript
var canvas = document.getElementById('canvas');
var context = canvas.getContext('2d');

context.beginPath();
context.rect( 50, 50, 500, 200 );
context.stroke();

context.beginPath();
context.fillStyle = '#f99';
context.fillRect( 50, 300, 500, 200 );

context.beginPath();
context.strokeStyle = '#587';
context.strokeRect( 50, 550, 500, 200 );
```

效果图： 

![img](/images/upload/canvas/canvas_6.png)

- 坐标空间和转换
  - translate( x, y )  转换画布的用户坐标系统。
  - rotate( deg )  旋转画布的坐标系统.
  - scale( sx, sy )  缩放变换
  - transform( a, b, c, d, e, f ) 变换矩阵 【同时使用transform会产生级联效果，即效果叠加】
    -  ( a  c  e )
    -  ( b  d  f )
    -  ( 0  0  1 )
      - a - 水平缩放（1）  
      - b - 水平倾斜（0）
      - c - 垂直倾斜（0）
      - d - 垂直缩放（1）
      - e - 水平位移（0）
      - f - 垂直位移（0）
  - setTransform( a, b, c, d, e, f ) 【可使transform不产生级联效果，重新产生transform效果】
- 渐变效果
  - 线性渐变
    - var grd = createLinearGradient( xstart, ystart, xend, yend );
    - grd.addColorStop ( stop, color );
    - fillStyle = grd;
  - 径向渐变
    - var grd = createRadialGradient( x0, y0, r0, x1, y1, r1 );
    - grd.addColorStop ( stop, color );
    - fillStyle = grd;

代码：

```javascript
var canvas = document.getElementById('canvas');

var context = canvas.getContext('2d');

context.save();
var grd = context.createLinearGradient( 0, 0, 800, 300 );
grd.addColorStop( 0, '#ffffff' );
grd.addColorStop( 0.25, '#eaff56' );
grd.addColorStop( 0.5, '#bce672' );
grd.addColorStop( 0.75, '#ff461f' );
grd.addColorStop( 1, '#70f3ff' );

context.fillStyle = grd;
context.fillRect( 0, 0, 800, 300 );
context.restore();

context.save();
var grd = context.createRadialGradient( 400, 500, 0, 400, 500, 300 );
grd.addColorStop( 0, '#ffffff' );
grd.addColorStop( 0.25, '#eaff56' );
grd.addColorStop( 0.5, '#bce672' );
grd.addColorStop( 0.75, '#ff461f' );
grd.addColorStop( 1, '#70f3ff' );

context.fillStyle = grd;
context.fillRect( 0, 400, 800, 400 );
context.restore();
```


效果图

![img](/images/upload/canvas/canvas_7.png)

- 填充效果
  - context.createPattern( img / canvas / video , repeat-style );
  
![img](/images/upload/canvas/canvas_8.png)

- 圆弧及圆
  - context.arc ( x, y, radius, startAngle, endAngle, counterclockwise= false );
    - x,y : 弧的圆形的圆心的坐标。
    - radius: 弧的圆形的半径。
    - startAngle, endAngle: 沿着圆指定弧的开始点和结束点的一个角度。这个角度用弧度来衡量。沿着 X 轴正半轴的三点钟方向的角度为 0，角度沿着逆时针方向而增加。
    - counterclockwise: 弧沿着圆周的逆时针方向（TRUE）还是顺时针方向（FALSE）遍历。
    ![img](/images/upload/canvas/canvas_9.png)

    ![img](/images/upload/canvas/canvas_10.png)

  -   context.arcTo( x1, y1, x2, y2, radius ) [ 根据两条线的切点绘制圆弧 ]
    ![img](/images/upload/canvas/canvas_11.png)
  

- 贝塞尔曲线：

  - 二次贝塞尔曲线( [http://blogs.sitepointstatic.com/examples/tech/canvas-curves/quadratic-curve.html](http://blogs.sitepointstatic.com/examples/tech/canvas-curves/quadratic-curve.html) )context.moveTo( x0, y0 );context.quadraticCurveTo( x1, y1, x2, y2 );
  - 三次贝塞尔曲线 ( [http://blogs.sitepointstatic.com/examples/tech/canvas-curves/bezier-curve.html](http://blogs.sitepointstatic.com/examples/tech/canvas-curves/bezier-curve.html) )context.moveTo( x0, y0 );context.bezierCurveTo( x1, y1, x2, y2, x3, y3 );

- 文字渲染

  - cxt.font = ' /* 样式 */ font-style/font-variant/font-weight/font-size/font-family  '

    - font-style: normal/italic/oblique
    - font-variant: normal/small-caps[ 英文小写字母转换成小型大写字母 ]
    - font-family: 支持 @font-face

  - cxt.fillText( string, x, y, [ maxlen ] )   —— 实心字

  - cxt.strokeText( string, x, y, [ maxlen ] )   —— 空心字

  - cxt.textAlign = left / center / right

  - cxt.textBaseline = top / middle / bottom / alphabetic[ default ] / ideographic / hanging

    - alphabetic : 针对拉丁语的基准线
    - ideographic ： 针对方块文字的基准线，如中文、日文
    - hanging： 针对印度语的基准线

  - cxt.mearsureText ( string ).width                        ( 文本度量：暂时只支持width宽度 )

    ```javascript
    var canvas = document.getElementById('canvas');

	var context = canvas.getContext('2d');

	context.font = "italic bold 50px arial";

	//实心字
	context.fillStyle = '#963';
	context.fillText( 'canvas fillText', 100,100 );
	//空心字
	context.strokeStyle = '#456';
	context.strokeText( 'canvas strokeText', 100,200 );
	//填充渐变
	var linearGrad = context.createLinearGradient( 0,0,800,0 );
	linearGrad.addColorStop ( 0, '#123' );
	linearGrad.addColorStop ( 0.25, '#456');
	linearGrad.addColorStop ( 0.5, '#789');
	linearGrad.addColorStop ( 0.75, '#147');
	linearGrad.addColorStop ( 1, '#963');
	context.fillStyle = linearGrad;
	context.fillText( 'canvas linearGradientText', 100,300 );
	//填充图片
	var bgImg = new Image();
	bgImg.src = 'img/bg-1.png';
	bgImg.onload = function(){
		var pattern = context.createPattern( bgImg, 'repeat' );
		context.textAlign = 'center';
		context.fillStyle = pattern;
		context.font = "bold 100px arial";
		context.fillText( 'canvas !', 400,450 );
	}
    ```

    ​

    ![img](/images/upload/canvas/canvas_12.png)

    ​

- 阴影

  - context.shadowColor

  - context.shadowOffsetX

  - context.shadowOffsetY

  - context.shadowBlur ( 阴影模糊程度 )

    ```javascript
    var canvas = document.getElementById('canvas');

	var context = canvas.getContext('2d');

	context.fillStyle = '#528';
	context.shadowColor = '#ccc';
	context.shadowOffsetX = 50;
	context.shadowOffsetY = 50;
	context.shadowBlur = 20;
	context.fillRect( 100,100,500,500 );
    ```

    ​

    ![img](/images/upload/canvas/canvas_13.png)

- 合成

  - context.globalAlpha = num; 全局透明度
  - context.globalCompositeOperation = 'opt' ;   图像重叠效果
    - source-over            destination-over
    - source-atop            destination-atop
    - source-in            destination-in
    - source-out            destination-out
    - lighter
    - copy
    - xor

- 剪辑区域

  - context.clip() 从原始画布中剪切任意形状和尺寸.
    ![img](/images/upload/canvas/canvas_14.png)
  
  - 非零环绕原则、
    ![img](/images/upload/canvas/canvas_15.png)
    ![img](/images/upload/canvas/canvas_16.png)


- isPointInPath( x, y )     如果指定的点位于当前路径中，则返回 true，否则返回 false