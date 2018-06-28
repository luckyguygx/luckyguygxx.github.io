---
title: svg贝塞尔曲线
date: 2018-06-28 11:19:17
tags:
---

官方定义：贝塞尔曲线(Bézier curve)，又称贝兹曲线或贝济埃曲线，是应用于二维图形应用程序的数学曲线。一般的矢量图形软件通过它来精确画出曲线，贝兹曲线由线段与节点组成，节点是可拖动的支点，线段像可伸缩的皮筋，我们在绘图工具上看到的钢笔工具就是来做这种矢量曲线的。贝塞尔曲线是计算机图形学中相当重要的参数曲线，在一些比较成熟的位图软件中也有贝塞尔曲线工具，如PhotoShop等。
 曲线定义：起始点、终止点（也称锚点）、控制点。通过调整控制点，贝塞尔曲线的形状会发生变化。 
 1962年，法国数学家Pierre Bézier第一个研究了这种矢量绘制曲线的方法，并给出了详细的计算公式，因此按照这样的公式绘制出来的曲线就用他的姓氏来命名，称为贝塞尔曲线。

#### svg贝塞尔曲线指令
![svg贝塞尔曲线](/img/svg-img1.jpg)

#### 测试小例子
```
<!DOCTYPE html>
<html>

<head>
    <style>
        .circular path {
            fill: none;
        }

        ul {
            padding: 0;
            margin: 0;
            display: flex;
            flex-flow: wrap;
            align-items: center;
            justify-content: space-between;
        }

        li {
            list-style: none;
            width: 300px;
        }
    </style>
</head>

<body>
    <p>SVG中path用来路径绘制，属性名称d由专门的“指令字母+坐标值”组成，如果指令字母是大写，例如M, 则表示坐标位置是绝对位置； 如果指令字母小写，比如m, 则表示坐标位置是相对位置。</p>

    <p>下面是几个测试小例子：</p>

    <ul>
        <li>
            <p>三次贝塞尔曲线：</p>
            <svg width="300" height="300">
                <path id="svg1" d="M20 20 C90,40 130,40 180,20" stroke="#000000" fill="none" style="stroke-width: 2px;"></path>
                <text>
                    <textPath xlink:href="#svg1">三次贝塞尔曲线三次贝塞尔曲线</textPath>
                </text>
            </svg>
        </li>
        <li>
            <p>三次贝塞尔曲线：</p>
            <svg width="300" height="300">
                <defs>
                    <path id="svg1" d="M20 20 C90,40 130,40 180,20" stroke="#000000" fill="none" style="stroke-width: 2px;"></path>
                </defs>
                <text>
                    <textPath xlink:href="#svg1">三次贝塞尔曲线三次贝塞尔曲线</textPath>
                </text>
            </svg>

        </li>
        <li>
            <p>二次贝塞尔曲线：</p>
            <svg width="300" height="300">
                <defs>
                    <path id="circle1" d="M30,70 Q75,0 120,70"></path>
                </defs>
                <text>
                    <textPath xlink:href="#circle1">二次贝塞尔曲线</textPath>
                </text>
            </svg>


        </li>
        <li>
            <p>a指令圆：</p>
            <div class='circular'>
                <svg width="300" height="300">
                    <path id="circle" d="M30,70 a50,50 1 1,1  0,1 z"></path>
                    <text>
                        <textPath xlink:href="#circle">圆形圆形圆形圆形圆形圆形圆形圆形圆形圆形</textPath>
                    </text>
                </svg>
            </div>

        </li>
        <li>
            <p>a指令圆弧：</p>
            <svg width="300" height="300">
                <defs>
                    <path id="circle" d="M30,70 a1,1 0 0,1 100,0"></path>
                </defs>
                <text>
                    <textPath xlink:href="#circle">圆弧文字形成了哈哈哈</textPath>
                </text>
            </svg>

        </li>
        <li>
            <p>直线：</p>
            <svg width="300" height="300">
                <path d="M10,10 L90,90" stroke="#000000" style="stroke-width: 5px;"></path>
            </svg>
        </li>
        <li>
            <p>水平线：</p>
            <svg width="300" height="300">
                <path d="M10,10 H90" stroke="#000000" style="stroke-width: 5px;"></path>
            </svg>
        </li>
        <li>

            <p>垂直线：</p>
            <svg width="300" height="300">
                <path d="M10,10 V90" stroke="#000000" style="stroke-width: 5px;"></path>
            </svg>
        </li>

        <li>

            <p>多次贝塞尔曲线：</p>
            <svg width="300" height="300">
                <defs>
                    <path id="bse" d="M 0 20 
                        C 20 10 ,30 0, 40 10
                        C 50 20, 60 30 ,70 20
                        C 80 10 ,90 10 ,100 20" />
                </defs>

                <use xlink:href="#bse" fill="none" stroke="red" />

                <text font-family="Verdana" font-size="12">
                    <textPath xlink:href="#bse">
                        多次贝塞尔多次贝塞尔多次贝塞尔多次贝塞尔多次贝塞尔
                    </textPath>
                </text>
            </svg>
        </li>

    </ul>

</body>

</html>

```

#### 效果图
![svg贝塞尔曲线](/img/svg-img3.jpg)

#### 参考文档
> * [深度掌握SVG路径path的贝塞尔曲线指令](https://www.zhangxinxu.com/wordpress/2014/06/deep-understand-svg-path-bezier-curves-command/)
> * [一些SVG向下兼容优雅降级技术](https://www.zhangxinxu.com/wordpress/2013/09/svg-fallbacks/)
 