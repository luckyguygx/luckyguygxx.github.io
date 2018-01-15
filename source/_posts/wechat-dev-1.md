---
title: node+express开发微信公众号开发问题-access_token
date: 2017-01-11 16:16:04
type: "tags"
tags: [微信开发]
---

#### 问：怎么有两个access_token？是一样的吗？

答：是有两个access_token，完全不是一个作用，刚开始做微信公众号开发的时候在这个上面还蒙了几天。
* 第一个access_token是微信公众号接口调用的授权凭证，微信公众平台对此token每天的调用次数规定了上限（见下图），并且这个token是有有效期的，有效期目前为2个小时，需定时刷新，重复获取将导致上次获取的access_token失效。微信公众平台开发者文档中也有建议我们开发者使用中控服务器统一获取和刷新Access_token，其他业务逻辑服务器所使用的access_token均来自于该中控服务器，不应该各自去刷新，否则容易造成冲突。
以下是每个接口每天大概的调用次数明细：

 ![主要明细](/img/wechat-access.jpg)

此接口地址为：
```
https请求方式: GEThttps://api.weixin.qq.com/cgi-bin/token?grant_type=client_credential&appid=APPID&secret=APPSECRET
```
* 另外一个access_token是微信网页授权时用到的，用户在微信客户端中访问第三方网页，公众号可以通过微信网页授权机制，来获取用户基本信息，进而实现业务逻辑。这个access_token没有调用次数限制。关于这个token更详细的文章请参考该链接：https://mp.weixin.qq.com/wiki?t=resource/res_main&id=mp1421140842
此接口地址为：
```
https://api.weixin.qq.com/sns/oauth2/access_token?appid=APPID&secret=SECRET&code=CODE&grant_type=authorization_code
```

* 以下是微信开发文档中对这两个token的说明：

 ![微信开发文档中对这两个token的说明](/img/wechat-access1.jpg)





 