---
title: 微信开发中ios系统input无法输入的问题
date: 2018-04-10 14:22:20
type: "tags"
tags: [混合开发 css]
---
   最近在做微信开发在iphone手机上测试的时候发现input输入框每次聚焦只能输入一个字符，试了几个可能影响的样式后终于找到了。。。
   原因只是写了一个禁止用户选择的公共样式：
   -webkit-user-select: none;