---
title: css世界--margin:auto实现水平垂直居中
date: 2018-06-25 14:57:24
type: "css"
tags: [css,css世界学习总结]
---

** 一般的垂直居中常用的几个方法无非display：table、css3的transform等常规方式。现分析总结一个不太使用的方式--牛逼的margin:auto.**

#### 原理剖析

 一个绝对定位的元素，如果元素定位方向上有确定数值的时候流体特性就会发生变化。比如一个绝对定位的元素样式是{left:0;right:0}宽度撑满了或者{top:0,bottom:0}高度撑满了再或者四个方向都设置了值为0尺寸会自动填充父级元素的可用尺寸，如果这时候再给元素设置宽度高度，那么原本应该被填充的空间就多余了部分，此时，如果又给该元素设置了margin:auto的话，这种绝对定位元素的margin:auto的填充规则和普通流体元素margin:auto的填充规则就是一样的：



* **如果一侧是定值，一侧是auto那么auto就为剩余空间大小；**
* **如果两侧都是auto，那就是平分剩余的空间；**

#### 代码举例

##### html:

```
<div id="dialog" class="dialog">
    <input type="button" id="button" class="button" value="点击按钮实现水平垂直居中" />
</div>
```

##### css:

```
.dialog { width: 500px; height: 300px; margin: auto; border: 1px solid #ddd; border-radius: 15px; background-color: #fff; box-shadow: 0 3px 18px rgba(0,0,0,.5); }
.dialog_absolute { position: absolute; left: 0; top: 0; right: 0; bottom: 0; z-index: 1; }

/* .dialog_absolute { position: absolute; top: 0; bottom:0; z-index: 1; } */

.button { display: block; margin: 130px auto; width: 190px; height: 40px; font-size: 14px; }
```

##### js:

```
var eleDialog = document.getElementById("dialog"),
    eleButton = document.getElementById("button");

eleButton.onclick = function() {
    if (eleDialog.className === "dialog") {
        eleDialog.className = "dialog dialog_absolute";
        this.value = "居中了，点击返回";    
    } else {
        eleDialog.className = "dialog";
        this.value = "点击按钮实现水平垂直居中";    
    }
};

```
#### 效果截图

![实现效果](/img/margin-auto-img1.jpg)

#### 在线效果查看
[在线效果查看](https://codepen.io/luckyguygx/pen/ERpgZN)

