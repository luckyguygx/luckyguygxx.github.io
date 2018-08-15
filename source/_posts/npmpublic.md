---
title: 测试自己发布一个npm包的流程
date: 2018-08-15 20:21:19
type: "tags"
tags: [npm]
---

记录一下发一个npm包的流程，此文以计算base64格式图片的大小一个小例子做测试。

* 新建一个文件夹：calculate-base64-size 进入目录后初始化一个项目：npm init 初始化一些基础数据
* 新建一个index.js文件放代码： 代码很简单，只是为了测试发布包的功能。
```
'use strict';
// 计算base64有多少KB
var calculateBase64Size = (imgFile) => {
  let tag = "base64,";
  imgFile = imgFile.substring(imgFile.indexOf(tag) + tag.length);
  let eqTagIndex = imgFile.indexOf("=");
  imgFile = eqTagIndex != -1 ? imgFile.substring(0, eqTagIndex) : imgFile;
  let strLen = imgFile.length;
  let fileSize = (strLen - (strLen / 8) * 2) / 1024;
  return fileSize
};

module.exports = calculateBase64Size;
```


* 看一下package.json文件是否需要完善,此处都是些很基础的

```
"name":"calculate-base64-size",
"version":"1.0.0",
"description":"A method for calculating the size of base64 files",
"main":"index.js",
"author":"https://github.com/luckyguygx",
"license": "MIT"
```


* 添加LICENCE文件。 把文件中的year和name版权拥有者改一下。
```
The MIT License (MIT)
Copyright (c) **year**  **name**
Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```

* 添加 README.md 项目使用说明文件 和 .gitignore忽略文件说明

* 发布npm包
 1） 到 https://www.npmjs.com 注册一个账号
 2） 在需要发布的文件目录终端执行npm adduser 按照提示输入用户名，密码和邮箱
 3） 执行npm whoami 命令如果出现你的名字的话就说明登录成功了
 4） 执行npm publish --access=public成功的话就是发布成功了
 5） 在另外一个工程里install一下刚刚发布的包名，可以测试一下功能是否正常
