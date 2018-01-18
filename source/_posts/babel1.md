---
title: babel、babel-polyfill与babel-runtime
date: 2017-01-18 11:07:28
type: "tags"
tags: [babel]
---
Babel是一个转码器，可以将es6，es7转为es5代码，在平常项目开发中经常用到。但除了平常用到的一些配置外，更深入一点儿的没有去研究，最近看到一篇关于babel的博文引起了我的兴趣，于是又学习了一番。现将关于babel的部分知识总结如下（只代表个人看法，资历不够理解的不对的地方，请指正，以后如有新的点也会继续补充）：


-  Babel 默认只转换js新的句法，不转换新的API，像是Iterator,Generator,Set,Maps，Proxy,Reflect,Symbol,Promise 等全局对象或者定义在全局对象上的方法比如Object.assign 都不会转码，所以为了使用完整的ES6 的API, 所以我们需要另外安装：babel-polyfill或者babel-runtime。两者的区别：
    - 前者会把全局对象统统覆盖一遍，不管你是否用得到,可以说比较霸道但是效果立竿见影。比较适用于大量使用了Promise，Object.assign, Array.from 等这类的全局对象或其所属方法的项目.缺点：包会比较大100k左右，如果是移动端应用，要衡量一下。
      -通过polyfill可以使用的新特性：
        ```
        ArrayBuffer    Array.from     Array.of   Array#copyWithin  Array#fill
        Array#find     Array#findIndex  Function#name   Map  Math.acosh  
        Math.hypot     Number.isNaN   Number.isInteger   Object.assign
        Object.getOwnPropertyDescriptors   Object.is   Object.entries Object.values
        Object.setPrototypeOf  Promise  Reflect  RegExp#flags  Set  String#codePointAt  String#endsWith  String.fromCodePoint  String#includes
        String.raw  String#repeat  String#startsWith  String#padStart  String#padEnd
        Symbol WeakMap  WeakSet
        ```
    - 后者可以按照需求引入，缺点：覆盖不全。一般在写库的时候使用。建议不要直接使用babel-runtime，因为transform-runtime依赖babel-runtime，大部分情况下都可以用transform-runtime来达成目的

- core-js是polyfill、runtime的核心包，因为polyfill和runtime其实都只是对core-js和   regenerator进行的封装。 可以直接引用core-js来达成目的。core-js组织结构非常清晰，高度的模块化。比如core-js/es6里包含了es6里所有的特性。而如果你只想实现promise可以单独引入core-js/promise。core-js的地址：https://github.com/zloirock/core-js#ecmascript-6
  - 使用方法：
   ```
   <!-- 直接添加到全局环境 -->
   require('core-js/fn/set');
   require('core-js/fn/array/from');
   ```

- Babel的命令行转码：babel-cli ：$ npm install --global babel-cli
  - 一些基本的用法：
  ```
  转码文件：
  比如：entry.js的转码结果写入out.js中，第二个命令是第一个的缩写：
  $babel entry.js --out-file out.js 
  $babel entry.js -o out.js

  转码整个目录：
  $ babel src --out-dir lib
  # 或者
  $ babel src -d lib
  加s可以生成source map文件：
  $ babel src -d lib -s
  ```

- Babel提供的一个在线编译器：
  - 地址：https://babeljs.io/repl/

- 使用babel-runtime的情况下，在babel的配置文件.babelrc中配置了"plugins": ["transform-runtime"]后，就不用再手动的引入对应的core-js/*了，因为转的时候会自动加上而且是根据需要只抽离你代码里需要的部分（已用promise做测试例子证明）。


                            未完待续。

