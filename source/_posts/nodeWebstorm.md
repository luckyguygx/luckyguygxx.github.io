---
title: webstorm 调试node工程的注意事项
date: 2017-11-06 14:53:37
type: "tags"
tags: [node 开发调试]
---

为了尝试一些新特性把本地node从6.x升级到了8.x结果悲催的发现无法debug调试node工程了。
报错内容为："bad option: - expose_debug_as=v8debug" 

如果在配置了一些configurations（--expose_debug_as=v8debug）之后仍未生效的话，可以尝试把webstorm也升级到2017.3版本。

一些node官网上相关的issue： 
https://github.com/nodejs/node/issues/13410 
https://intellij-support.jetbrains.com/hc/en-us/community/posts/115000397470-Debugging-node-version-8-1-2
