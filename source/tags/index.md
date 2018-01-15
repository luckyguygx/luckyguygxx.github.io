---
title: babel-polyfill
date: 2018-01-05 09:11:55
type: "tags"
tags: [babel]
---
> Babel 默认只转换js新的句法，不转换新的API，像是Iterator,Generator,Set,Maps，Proxy,Reflect,Symbol,Promise 等全局对象或者定义在全局对象上的方法比如Object.assign 都不会转码，所以为了使用完整的ES6 的API, 需要另外安装插件：babel-polyfill

___

Babel默认不转码的API清单：definitions.js:
https://github.com/babel/babel/blob/master/packages/babel-plugin-transform-runtime/src/definitions.js

___

```
npm i  --save-dev babel-polyfill
<!-- 然后在需要使用文件的顶部引入 -->
import “babel-polyfill”

<!-- 或者如果用webpac构建的话： -->
webpack.config.js中：
entry: ['babel-polyfill', `./${conf.path.src('index')}`]
```