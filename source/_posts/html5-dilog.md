---
title: HTML 5.2新特性
date: 2018-01-18 17:31:55
type: "tags"
tags: [html]
---
HTML 5.2 正式成为了 W3C 的推荐标准（REC）。REC 阶段意味着它已经得到了W3C的认可。并且 W3C 将正式推荐浏览器厂商部署、web 开发者实现此规范。在HTML5.2版本中增加或删除了一些特性，比如新增了dialog，多个main元素，body里可以写style样式等等。我觉得最能让前端开发者感到开心的就是diolag这个点儿了。

直接上代码：

```
<html>
<head>
    <meta charset="utf-8">
    <title>dialog</title>
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
    <meta name="description" content="">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <style>
        .dialog-warp {
            width: 300px;
            height: 200px;
            padding: 20px;
            border: 1px solid #ccc;
            box-sizing: border-box;
            left: 50%;
            top: 50%;
            margin-left: -150px;
            margin-top: -100px;
        }
    </style>
</head>

<body>
    <button id="open">Open Dialog</button>
    <button id="close">Close Dialog</button>
    <dialog id="dialog" class="dialog-warp">
        <h2>Dialog Title</h2>
        <p>Dialog content and other stuff will go here</p>
    </dialog>
    <script>  
        const dialog = document.getElementById("dialog");
        document.getElementById("open").addEventListener("click", () => {
            dialog.show();
        });
        document.getElementById("close").addEventListener("click", () => {
            dialog.close();
        });
    </script>
</body>

</html>
```

浏览器支持情况：虽然支持率不怎么样但还是值得开心的
   ![支持情况](/img/html1.jpg)