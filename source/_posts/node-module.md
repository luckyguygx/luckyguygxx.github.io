---
title: Node中的模块
date: 2018-02-26 13:37:24
type: "tags"
tags: [node]
---
  提到Node的模块必须要提到CommonJs因为node就是对该规范的实现，当然，node在实现中也是在遵循该规范的同时进行了取舍。那首先来剖析下CommonJs中对模块的定义：
  CommonJs对模块的定义很简单，主要分为模块引用，模块定义，模块标识三部分。
  1. 模块引用：
     var math = require('math');  // 如果不加扩展名，Node会按照.js、 .json 、.node的次序补足扩展名依次尝试。
     **需要注意的一点是在尝试的过程中需要调用fs模块阻塞式的判断文件是否存在，因为node是单线程所以会引起性能问题，所以如果是.node或者.json文件，最好还是带上后缀名**

  2. 模块定义：
     exports对象用于导出当前模块的方法或者变量。 **在模块中还存在一个module对象，它代表模块本身，exports是module的属性**。
     在Node中，一个文件就是一个模块，将方法挂载在exports对象上作为属性就可以导出了：
     // test.js
     exports.add = function(){
     ...
     }
     在另一个文件中：
     // program.js
     var math = require('test');
     
  3. 模块标识：
     模块标识其实就是传递给require()方法的参数，**参数可以是符合小驼峰命名的字符串或者相对路径或者绝对路径**。
     ___

  **CommonJs 模块有一个特点从以下的源码中很容易发现那就是模块可以多次加载，但是只会在第一次加载时运行一次，然后运行结果就被放进缓存了，以后再require改模块，会直接读取缓存结果。如果改动了代码想要让模块再次运行的话，必须要清除该模块的缓存**
```
Module._load = function(request, parent, isMain) { 
 // 计算绝对路径 
 var filename = Module._resolveFilename(request, parent); 
 // 如果有缓存，取出缓存 
 var cachedModule = Module._cache[filename]; 
 if (cachedModule) { 
 return cachedModule.exports; 
 // 第二步：是否为内置模块 
 if (NativeModule.exists(filename)) { 
 return NativeModule.require(filename); 
 } 
 // 第三步：生成模块实例，存入缓存
 var module = new Module(filename, parent);
 Module._cache[filename] = module; 
 // 第四步：加载模块 
 try { 
 module.load(filename); 
 hadException = false; } 
 finally { if (hadException) { 
 delete Module._cache[filename];
 } 
 } 
 // 第五步：输出模块的exports属性
 return module.exports;
 };
```

清除缓存：
```
// 清某个模块的缓存 
delete require.cache[require.resolve('/*moduleName*/')] 
 // 清所有模块的缓存 
Object.keys(require.cache).forEach(function(key) { delete require.cache[key]; })
```
 
  在Node中，模块分为两类：一类是node提供的模块被称为核心模块（比如http，fs，path等），另一类是用户编写的模块称为文件模块。
  在Node中引入模块，需要经历三个步骤：
  1.  路径分析
  2.  文件定位
  3.  编译执行
  核心模块在node源码的编译过程中编译进了二进制执行代码，在node进程启动的时候已经被加载进内存中了，所以引用核心模块的时候不需要进行**文件定位和编译执行**，并且在路径分析上还进行优先判断，所以核心模块的加载速度是最快的。
  文件模块则是在运行时动态加载，需要完整的路径分析，文件定位，编译执行的过程，相比要比核心模块速度要慢些。


