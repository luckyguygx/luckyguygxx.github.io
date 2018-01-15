---
title: BFC
date: 2016-01-19 00:34:14 
type: "tags"
tags: [css]
---
### 什么是 BFC
 Block Formatting Contexts（BFC）：块级元素格式化上下文
###  BFC布局规则
> *  内部的Box会在垂直方向，一个接一个地放置。
> *  Box垂直方向的距离由margin决定。** 属于同一个BFC的两个相邻Box的margin会发生重叠 **
> *  每个元素的margin box的左边， 与包含块border box的左边相接触( 对于从左往右的格式化，否则相反)。**即使存在浮动也是如此**。
> *  BFC的区域不会与float box重叠。
> *  BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
> *  计算BFC的高度时，浮动元素也参与计算

### 触发BFC的方式（一下任意一条就可以）
> *  float属性不为none
> *  position为absolute或fixed
> *  display为inline-block, table-cell, table-caption, flex, inline-flex
> *  overflow不为visible

### BFC应用场景
1.之前面试的时候被问到频率比较高的一道css题就是：写出几种实现一个div内分两列，左边一列固定宽度，右边一列自适应布局的方法，以及每种方法实现的原理是什么？ 其中有一种就可以利用BFC实现，代码如下：
```
<!DOCTYPE HTML>
<html>
<head>
    <style>
        .con {
            width: 100%;
            background-color: #c0c0c0;
            position: relative;
            box-sizing: border-box;
            border: 10px solid #999;
        }
        .left {
            width: 100px;
            height: 50px;
            float: left;
            background: #ff8000;
        }
        .main {
            height: 100px;
            overflow: hidden;/*将右边元素设置为BFC元素即可*/
            background: #ffc68c;
        }
    </style>
</head>
<body>
    <div class="con">
        <div class="left"></div>
        <div class="main"></div>
    </div>
</body>
</html>
```
右边不设置为bfc元素时的效果如下：
![bfc1.jpg](http://upload-images.jianshu.io/upload_images/4315733-4248be2c7e27492e.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
原因就是bfc的这条规则： `每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。`

右边设置为BFC元素可以利用`BFC的区域不会与float box重叠规则`实现。效果如下：
![bfc2.jpg](http://upload-images.jianshu.io/upload_images/4315733-f4c521ea169efaba.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2.利用BFC( `计算BFC的高度时，浮动元素也参与计算`)轻松清楚内部浮动:
```
<!DOCTYPE HTML>
<html>
<head>
    <style>
        .con {
            width: 100%;
            background-color: #ffffff;
            position: relative;
            box-sizing: border-box;
            border: 1px solid #999;
            overflow: hidden;/*使其成为BFC*/
        }
        .left {
            width: 100px;
            height: 50px;
            float: left;
            background: #ff8000;
        }
    </style>
</head>
<body>
    <div class="con">
        <div class="left"></div>
        <div class="left"></div>
    </div>
</body>
</html>
```