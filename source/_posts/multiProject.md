---
title: nginx配置一个域名下多个前端工程之前端实现方法
date: 2018-04-25 14:19:39
type: "tags"
tags: [webpack vue]
---
   ##### 对于普通的静态网站来说实现一个域名下多个前端工程没啥问题，但如果是使用了像webpack模块打包工具类似的工程的话还是需要对工程稍加配置的，最近试验了几种方案，虽然还有些细节没有搞清楚，但还是先总结一下吧。
  
   -----
   如下图所示，nginxconfig里配置里两个匹配项/app 和/wechat 分别指向app前端工程和wechat前端工程，然后访问的时候路径应该是：


  * http://xxx.xxx.xxx/app/该目录放置app工程的页面
  * http://xxx.xxx.xxx/wechat/该目录放置wechat工程的页面

  nginx.conf:

  ```
  location /wechat/{
		     proxy_pass http://xx.xx.xx.xx:xxx/wechat/;
		}
  location /app/{
		     proxy_pass http://xx.xx.xx.xx:xxx/app/;
		}
  ```

  ![result](/img/nginxconfig.jpg)

  ----

 ##### 工程描述：由于项目开发的比较早，各种原因又一直没有重构，使用的还是webpack1.X的版本，构建工具是vue-cli。 

 ##### 关键因素： 是否设置了publicPath（根据环境区分assetsPublicPath路径） 和 路由模式

  ----
 ##### 为了更好的理解先列一下几点基础知识：
  1. vue的路由模式：
      * hash —— 即地址栏 URL 中的 # 符号
比如这个 URL：http://www.xxx.com/#/login，hash 的值为 #/login。它的特点在于：hash 虽然出现在 URL 中，但不会被包括在 HTTP 请求中，对后端完全没有影响，因此改变 hash 不会重新加载页面。且push路由的时候只可修改 # 后面的部分，因此只能设置与当前 URL 同文档的 URL。
      * history —— 利用了 HTML5 History Interface 中新增的 pushState() 和 replaceState() 方法。push路由的时候路径全改

 2. publicPath:
    1. 官网文档的解释：该配置能帮助你为项目中的所有资源指定一个基础路径。它被称为公共路径(publicPath)

 
 
  ##### 实现方式：
  
   配置publicPath （配置assetsPublicPath路径为'/${需要加的层级}/'）比如'/app/' ，路由模式为hash （**注意点：页面内如果有直接写的location.href跳转的需要手动加一层关系**）

 




