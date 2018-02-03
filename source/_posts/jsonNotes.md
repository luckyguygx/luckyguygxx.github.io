---
title: flex各种使用场景
date: 2018-02-02 16:34:43
type: "tags"
tags: [flex css]
---
1.
效果图：
![flex](/img/flex.jpg)
```
<style>
        p {
            padding: 0;
            margin: 0;
        }

        .test-cell {
            padding: 10px 15px;
            position: relative;
            display: -webkit-box;
            display: -webkit-flex;
            display: flex;
            -webkit-box-align: center;
            -webkit-align-items: center;
            align-items: center;
            min-height: 44px;
            line-height: 44px;
        }

        .test-cell:before {
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
            left: 15px;
        }

        .test-cell:after {
            content: " ";
            position: absolute;
            left: 0;
            bottom: 0;
            right: 0;
            height: 1px;
            border-bottom: 1px solid #D9D9D9;
            color: #D9D9D9;
            -webkit-transform-origin: 0 0;
            transform-origin: 0 0;
            -webkit-transform: scaleY(0.5);
            transform: scaleY(0.5);
            left: 15px;
        }

        /* .test-cell:first-child:before {
            display: none;
        } */

        .test-cell-primary {
            -webkit-box-flex: 1;
            -webkit-flex: 1;
            flex: 1;
            color: #808080;
        }

        .test-label {
            display: block;
            word-wrap: break-word;
            word-break: break-all;
        }

        .test-cell__ft {
            text-align: right;
            color: #999999;
        }

        .test-cell_access {
            -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
            color: inherit;
        }

        .test-cell_access:active {
            background-color: #ECECEC;
        }

        .test-cell_access {
            -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
            color: inherit;
        }

        .test-cell_access:active {
            background-color: #ECECEC;
        }

        .test-cell_access .test-cell__ft:after {
            content: " ";
            display: inline-block;
            height: 6px;
            width: 6px;
            border-width: 2px 2px 0 0;
            border-color: #C8C8CD;
            border-style: solid;
            -webkit-transform: matrix(0.71, 0.71, -0.71, 0.71, 0, 0);
            transform: matrix(0.71, 0.71, -0.71, 0.71, 0, 0);
            position: relative;
            top: -2px;
            position: absolute;
            top: 50%;
            margin-top: -4px;
            right: 2px;
        }

        .test-cell-title {
            text-align: left;
        }

        .test-cell-label {
            text-align: right;
            margin-left: 20px;
        }

        .test-cell-input {
            width: 100%;
            display: block;
            margin: 0;
            padding: 0 10px;
            border: none;
            text-align: right;
            line-height: 44px;

        }

        .mtb-20 {
            margin: 20px 0;
            text-align: center;
        }

        a {
            text-decoration: none;
            -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
            -webkit-touch-callout: none;
        }

        .test-button-group {
            -webkit-touch-callout: none;
            display: box;
            display: -webkit-box;
            display: -webkit-flex;
            display: flex;
        }

        .test-button-group>a.test-button-tab-item-first {
            border-top-left-radius: 32px;
            border-bottom-left-radius: 32px;
        }

        .test-button-group>a {
            display: block;
            position: relative;
            -webkit-box-flex: 1;
            -webkit-flex: 1;
            flex: 1;
            width: 100%;
            height: 30px;
            padding: 0;
            font-size: 14px;
            line-height: 31px;
            text-align: center;
            color: #999;
            white-space: nowrap;
            background: #ddd;
            -webkit-tap-highlight-color: rgba(255, 0, 0, 0);
        }

        .test-button-group>a.test-button-group-current {
            color: #000;
            background: #ff8000;
        }

        .test-button-group>a.test-button-tab-item-last {
            border-top-right-radius: 32px;
            border-bottom-right-radius: 32px;
        }
    </style>

```
```
<body>
    <div class="test-cell test-cell_access">
        <div class="test-cell-primary">
            <p>
                <label class="test-label">测试</label>
            </p>
        </div>
        <div class="test-cell__ft"></div>
    </div>
    <p class="mtb-20">------------分割线-------------</p>

    <div class="test-cell test-cell_access">
        <div class="test-cell-title">金额：</div>
        <div class="test-cell-primary">
            <input type="text" class="test-cell-input" placeholder="请输入金额">
        </div>
        <div class="test-cell-label">元</div>
    </div>
    <p class="mtb-20">------------分割线-------------</p>

    <div class="test-button-group">
        <a href="javascript:" class="test-button-tab-item test-button-tab-item-first">今天</a>
        <a href="javascript:" class="test-button-tab-item test-button-tab-item-middle">本周</a>
        <a href="javascript:" class="test-button-tab-item test-button-group-current test-button-tab-item-last">本月</a>
    </div>
</body>
```

--未完待续--
