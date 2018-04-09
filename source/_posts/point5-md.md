---
title: 几种实现0.5像素线的方法
date: 2018-04-09 16:57:19
type: "tags"
tags: [css 0.5像素的线]
---
   最近写了不少移动端项目的样式用到了几种实现0.5像素线的方法，现归纳了几种比较合适的代码如下：

   ```
   <!DOCTYPE HTML>
<html>

<head>
    <meta charset="utf-8">
    <meta name="viewport"
          content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no, minimal-ui">
    <style>
        h4 {
            text-align: center;
            color: #39C2D3;
        }

        .test-line.svg {
            height: 1px;
            background: url("data:image/svg+xml;utf-8,<svg xmlns='http://www.w3.org/2000/svg' width='100%' height='1px'><line x1='0' y1='0' x2='100%' y2='0' stroke='#39C2D3'></line></svg>");
            background: url("data:image/svg+xml;base64,PHN2ZyB4bWxucz0naHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmcnIHdpZHRoPScxMDAlJyBoZWlnaHQ9JzFweCc+CiAgICA8bGluZSB4MT0nMCcgeTE9JzAnIHgyPScxMDAlJyB5Mj0nMCcgc3Ryb2tlPScjMzlDMkQzJz48L2xpbmU+Cjwvc3ZnPg==");
        }

        .normal {
            border-bottom: 1px solid #39C2D3;

        }

        .test-line.scale-half {
            height: 1px;
            transform: scaleY(0.5);
            transform-origin: 50% 100%;
            background: #39C2D3;
        }

        .test-line.boxshadow {
            height: 1px;
            background: none;
            /*-webkit-appearance: none;*/
            box-shadow: 0 0.5px 0 0 #39C2D3;
            -webkit-box-shadow: 0 0.5px 0 0 #39C2D3;
            /*border-radius:1px;*/
        }

        .sd {
            width: 200px;
            height: 240px;
            -webkit-box-shadow: 0 0 20px rgba(0, 0, 0, 0.4);
            -moz-box-shadow: 0 0 10px rgba(0, 0, 0, 0.4);
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.4);
            border: none;
        }

        .cell {
            width: 100%;
            height: 48px;
            line-height: 48px;
            position: relative;
        }

        .cell:before {
            content: " ";
            position: absolute;
            left: 0;
            top: 0;
            right: 0;
            height: 1px;
            border-top: 1px solid #D9D9D9;
            color: #D9D9D9;
            -webkit-transform-origin: 0 0;
            transform-origin: 0 0;
            -webkit-transform: scaleY(0.5);
            transform: scaleY(0.5);
        }

        .cell:after {
            content: " ";
            position: absolute;
            left: 0;
            bottom: 0;
            right: 0;
            height: 1px;
            border-bottom: 1px solid #D9D9D9;
            color: #D9D9D9;
            -webkit-transform-origin: 0 100%;
            transform-origin: 0 100%;
            -webkit-transform: scaleY(0.5);
            transform: scaleY(0.5);
        }

        .cell-svg {
            width: 100%;
            height: 48px;
            line-height: 48px;
            position: relative;
        }

        .cell-svg:before {
            content: " ";
            position: absolute;
            left: 0;
            top: 0;
            right: 0;
            height: 1px;
            background: url("data:image/svg+xml;utf-8,<svg xmlns='http://www.w3.org/2000/svg' width='100%' height='1px'><line x1='0' y1='0' x2='100%' y2='0' stroke='#39C2D3'></line></svg>");
            background: url("data:image/svg+xml;base64,PHN2ZyB4bWxucz0naHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmcnIHdpZHRoPScxMDAlJyBoZWlnaHQ9JzFweCc+CiAgICA8bGluZSB4MT0nMCcgeTE9JzAnIHgyPScxMDAlJyB5Mj0nMCcgc3Ryb2tlPScjMzlDMkQzJz48L2xpbmU+Cjwvc3ZnPg==");

        }

        .cell-svg:after {
            content: " ";
            position: absolute;
            left: 0;
            bottom: 0;
            right: 0;
            height: 1px;
            background: url("data:image/svg+xml;utf-8,<svg xmlns='http://www.w3.org/2000/svg' width='100%' height='1px'><line x1='0' y1='0' x2='100%' y2='0' stroke='#39C2D3'></line></svg>");
            background: url("data:image/svg+xml;base64,PHN2ZyB4bWxucz0naHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmcnIHdpZHRoPScxMDAlJyBoZWlnaHQ9JzFweCc+CiAgICA8bGluZSB4MT0nMCcgeTE9JzAnIHgyPScxMDAlJyB5Mj0nMCcgc3Ryb2tlPScjMzlDMkQzJz48L2xpbmU+Cjwvc3ZnPg==");

        }


    </style>

</head>

<body>
<div class="normal">正常的1像素的线</div>
<br/>
<br/>
<br/>
<h4>0.5像素的线各种实现方式测试：</h4>
<br/>
<br/>
<br/>
<p>svg方式，表现良好，但在火狐里需要把svg转成base64格式 因为火狐里不支持#999这样定义线的颜色只能写类似black之类的 .有好多可以把svg转base64的网站比如这个https://www.css-js.com/tools/base64.html </p>
<div class="test-line svg "></div>
<br/>
<br/>
<br/>
<br/>
<p>scaleY(0.5)方式，表现良好</p>
<div class="test-line scale-half"></div>
<br/>
<br/>
<br/>
<p>box-shadow方式 兼容性不好，在Safari上不支持小于1px的boxshadow，所以用safari浏览器的话就看不到这个0.5了</p>
<div class="test-line boxshadow"></div>
<br/>
<br/>
<br/>

<h4>应用实例</h4>
<div class="cell">测试line-scaleY</div>

<br/>
<br/>
<br/>
<div class="cell">测试svg</div>
<br/>
<br/>
<br/>
<!--<div class="sd"></div>-->
</body>

</html>
   ```