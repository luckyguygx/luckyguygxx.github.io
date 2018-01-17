---
title: hexo博客重整及域名绑定
date: 2017-01-15 10:12:47
type: "tags"
tags: [hexo]
---

刚开始用hexo搭建博客时，未考虑到换台电脑怎么处理的问题，无奈又重新整理了一次，（注意一定要先保留之前的文件不要删除）重整流程如下：

1. 把原来的仓库重新命名并按格式创建新仓库，然后建两个分支 master 和 dev 。并在setting的branch里把dev设置为默认分支；（确保以下几步在dev分之下进行）
2. 把仓库git clone下来
3. 将之前备份的文件夹中的_config.yml，themes/，source/，scaffolds/，package.json，.gitignore复制至此文件夹下
4. 如果你也用的是next主题要注意下把next主题下的.git文件删除，否则主题文件提交不上去
5. 新仓库文件夹下执行npm install和npm install hexo-deployer-git。然后修改_config.yml中的deploy参数为master分支
6. 按正常提交逻辑提交dev分支 git add ./, git commit ..., git push origin dev:dev
7. 执行hexo g -d就可以发布静态网站到master分支上了


至此，可以算是能用了。源文件在dev分支上以后就不用怕换电脑了，耶耶耶！

下面来说说域名的事儿，因为github的这个地址不太容易记，之前空着一个域名一直没有用上，所以就把申请的域名绑定到这个博客上了，如果你也有自己的域名可以按照以下步骤绑定上：

准备事项：
ping一下自己的仓库（yourname.github.io）的IP地址 


* 域名解析：我选择了用DNSPOD，注册登录成功后,进入管理控制台，选择域名解析tab，添加域名，然后给该域名添加三条记录：

 ![添加记录](/img/hexo1.jpg)

* 更改DNS地址：我用的是oray申请的域名所以要到oray里的域名管理里把ns地址改为DNSPOD给的两个地址：
 
![更改ns地址](/img/hexo2.jpg)

* 在source文件夹（放在这里的目的是为了不在生成静态文件的时候被忽略掉）里新建CNAME文件主要不带任何后缀，CNAME文件里面内容是你的域名比如yourname.com

发布下试试看吧，因为oray上更新DNS后，48小时内生效，所以我这些操作是两天内完成的，不过网上有人说其实十几分钟就可以生效了。

