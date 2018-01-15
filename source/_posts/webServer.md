---
title: Web Server For Chrome
date: 2017-01-05 13:44:50
type: "tags"
tags: [移动端开发调试]
---

###### Web Server for Chrome
 官方介绍：
 A Web Server for Chrome, serves web pages from a local folder over the network, using HTTP. Runs offline.Web Server for Chrome is an open source (MIT) HTTP server for Chrome.
 It runs anywhere that you have Chrome installed, so you can take it anywhere. It even works on ARM chromebooks.
 It now has the option to listen on the local network, so other computers can access your files. Additionally, it can try and get an internet address.
 Many people use this to do basic web development on a chromebook. It is also handy for sharing files over a local network between computers, or even on the internet.
 

> 安装地址：https://chrome.google.com/webstore/detail/web-server-for-chrome/ofhbbkphhbklhfoeikjpcbhemlocgigb?hl=en
___

![web server for chrome](/img/webserver.png)

* 勾选了Accessible on local network会生成一个以你当前局域网ip为基址的地址（不勾选的话默认只会生成127.0.0.1的地址）
* Automatically show index.html作用是在URL没指定哪个html文件时，默认指向index.html；
* Choose Folder选择你文件所在的文件夹，再点下开关打开服务器，点击Web Servers URL(s)就可以跳转到网页了 移动端输入生成的ip地址也就可以访问了 