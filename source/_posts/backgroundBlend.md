---
title: css黑魔法：backgroundBlend
date: 2018-01-05 16:59:40
type: "tags"
tags: [css]
---
布静态页面时如果需要多个不同颜色的同一个图标时，如果不用字体图标的话就需要引入多个图片，而css3的background-blend-mode只需要一张**白底黑色主体**的图片（图片格式JPG、PNG、GIF 都可以）就可以实现在图片下叠加多一层其他颜色，改变图片主体颜色（黑色）变成其它颜色的目的。

##### 代码 
```
<!DOCTYPE HTML>
<html>

<head>
  <style>
    .pic {
      width: 50px;
      height: 50px;
      background-image: url('../img/css1.png');
      background-size: cover;
    }

    .pic1 {
      width: 50px;
      height: 50px;
      background-image: url('../img/css1.png'), linear-gradient(#eeeeee, #000);
      background-blend-mode: lighten;
      background-size: cover;
    }

    .pic2 {
      width: 50px;
      height: 50px;
      background-image: url('../img/css1.png'), linear-gradient(#eee, #eee);
      background-blend-mode: lighten;
      background-size: cover;
    }
  </style>

</head>

<body>
  <div>
    <!-- 原图 -->
    <div class="pic"></div>
    <!-- 渐变 -->
    <div class="pic1" style="margin-top:20px;"></div>
    <!-- 单色 -->
    <div class="pic2" style="margin-top:20px;"></div>
  </div>

</body>

</html>
```

##### 效果
![css实现不同颜色背景](/img/cssbac1.jpg)

##### 兼容性
![兼容性](/img/cssbac2.jpg)