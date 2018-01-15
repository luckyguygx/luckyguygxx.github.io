---
title: Node-prune
date: 2017-12-26 15:19:34
type: "tags"
tags: [node]
---
   Node-prune is a small tool to prune unnecessary files from 'node_modules', such as the markdown, typescript source files, and so on. And when you install some plugins, some files such as example, doc, docs, test and the like also be installed. So, when you put your project on the server, you will find the bulk is too large, and the release time will grow. This tool can reduce release time efficiently。
   
#### 安装go平台和配置相关的环境变量
下载地址：https://golang.org/dl/
下载安装过程就忽略了，环境变量配置如下(windows环境下)：

- GOROOT：Go的安装目录
- GOPATH：用于存放Go语言Package的目录，注意（**这个目录不能在Go的安装目录中**)
- GOBIN：Go二进制文件存放目录，写成%GOROOT%\bin就好
- GOOS：操作系统
- GOARCH：指定系统环境，i386表示x86，amd64表示x64
     ![go](/img/nodeprune1.png)



#### 安装node-prune
```
$ go get github.com/tj/node-prune/cmd/node-prune
```


#### 使用方法
1. 在项目的文件夹里使用：

   ```
   $ node-prune
   ```
   找了一个小项目试了试，瞬间少了10M：
   ![result](/img/nodeprune2.jpg)

2. 在别的目录下使用：

   ```
   $ node-prune path/to/node_modules
   ```

3. 添加到package.json里的scripts里：

   ```
   "scripts": {
    "postinstall": "node-prune"
   }
   ```

#### 了解更多
  [node-prune github 地址](https://github.com/tj/node-prune)

     




