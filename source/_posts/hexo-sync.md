---
title: hexo博客搬迁
date: 2017-01-15 10:12:47
type: "tags"
tags: [hexo]
---
刚开始用hexo搭建博客时，未考虑到换台电脑怎么处理的问题，无奈又重新搬迁了一次，（注意先保留之前的blog文件）搬迁流程如下：
1. 把原来的仓库重新命名并按格式创建新仓库，然后建两个分支 master 和 dev 。并在setting的branch里把dev设置为默认分支；（确保以下几步在dev分之下进行）
2. 把仓库git clone下来
3. 将之前备份的文件夹中的_config.yml，themes/，source/，scaffolds/，package.json，.gitignore复制至此文件夹下
4. 如果你也用的是next主题要注意下把next主题下的.git文件删除，否则主题文件提交不上去
5. 新仓库文件夹下执行npm install和npm install hexo-deployer-git。然后修改_config.yml中的deploy参数为master分支
6. 按正常提交逻辑提交dev分支 git add ./, git commit ..., git push origin dev:dev
7. 执行hexo g -d就可以发布静态网站到master分支上了


至此，搬迁就算完成了。源文件在dev分支上以后就不用怕换电脑了，耶耶耶！