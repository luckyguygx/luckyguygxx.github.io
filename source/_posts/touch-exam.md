---
title: css世界-css选择器
date: 2018-06-27 11:23:01
tags:
---


#### 关系选择器


| 选择符        | 名称   |  描述  |
| --------   | -----:  | :----:  |
| E F     | 包含选择符 |   选择所有被E元素包含的F元素     |
| E > F         |   子选择符   |  选择所有作为E元素的子元素F   |
| E + F          |   相邻选择符 |  选择紧贴在E元素之后的F元素 该选择符只能选择两个相邻兄弟元素中的第二个元素  |
| E ~ F         |   兄弟选择符 |  选择E元素后面的所有兄弟元素F |


------

#### 属性选择器

| 选择符  |  描述  |
| -------- |  ----:  |
| E[attr] | 选择具有attr属性的E元素 |  
| E[attr = 'val'] |  选择具有attr属性并且属性值等于val的E元素|  
| E[attr$ = 'val']|  选择具有attr属性并且属性值以val结尾的字符串的E元素 | 
| E[attr* = 'val']|  选择具有attr属性并且属性值包含val字符串的E元素 |


------

#### 案例

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>元素选择器</title>
    <style type="text/css">
        .u1 li{
            border: 1px solid orange;
        }
        .u2>li{
            border: 1px solid orange;
        }
        .u3 li+li{
             border: 1px solid orange;
        }
        .u4 li~li{
            border: 1px solid orange;
        }
    </style>
</head>
<body>
     <h6>第一个ul</h6>
    <ul class="u1">
        <li>我是li1</li>
        <li>我是li2</li>
        <li>我是li3</li>
        <li>我是li4</li>
        <li>
            <ul>
                <li>我是第二级别的li</li>
                <li>我是第二级别的li</li>
                <li>我是第二级别的li</li>
            </ul>
        </li>
    </ul>
    <h6>第二个ul</h6>
    <ul class="u2">
        <li>我是li1</li>
        <li>我是li2</li>
        <li>我是li3</li>
        <li>我是li4</li>
        <li>
            <ul>
                <li>我是第二级别的li</li>
                <li>我是第二级别的li</li>
                <li>我是第二级别的li</li>
            </ul>
        </li>
    </ul>
    <h6>第三个ul</h6>
    <ul class="u3">
        <li>我是li1</li>
        <li>我是li2</li>
        <li>我是li3</li>
        <li>我是li4</li>
        <li>
            <ul>
                <li>我是第二级别的li</li>
                <p>隔断会发生什么</p>
                <li>我是第二级别的li</li>
                <p>隔断会发生什么</p>
                <li>我是第二级别的li</li>
            </ul>
        </li>
    </ul>
    <h6>第四个ul</h6>
    <ul class="u4">
        <li class="firstli">我是li1</li>
        <li>我是li2</li>
        <li>我是li3</li>
        <li>我是li4</li>
        <li>
            <ul>
                <li>我是第二级别的li</li>
                <p>隔断会发生什么</p>
                <li>我是第二级别的li</li>
                <p>隔断会发生什么</p>
                <li>我是第二级别的li</li>
            </ul>
        </li>
    </ul>
</body>
</html>
```

#### 案例效果图

![css选择器案例效果图](/img/css-img1.jpg)



