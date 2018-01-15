---
title: 微信小程序自带toast
date: 2017-06-10 22:40:56 
type: tags
tags: [小程序]
---
微信小程序自带toast提示并不好用，对于项目中UI设计不同要显示后台不同接口返回的信息来说，不能满足其需求，所以还是跟着网上的一些方法建了一个比较简单的，记录如下：
首先要完成的几个步骤： 
* 根据UI 的设计图建一个模板，在pages里增加了toast页面； 
* 创建组件的目录components 增加显示或隐藏toast 的js，并在app.js 中全局引入，并在初始化该小程序的时候传入。
* 在app.wxss 当中引入或者直接在app.wxss中增加toast模板的样式；
![目录.png](http://upload-images.jianshu.io/upload_images/4315733-c12555fc2a25053a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![app.js.png](http://upload-images.jianshu.io/upload_images/4315733-9a422a75550f12e0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
/* app.wxss toast提示 */
.toast_content_box {
display: flex;
width: 100%;
height: 100%;
justify-content: center;
align-items: center;
position: fixed;
z-index: 999;
background:rgba(0,0,0,0.6);
}
.toast_content {
width: 50%;
padding: 30rpx;
background:rgba(0,0,0,0.6);
border-radius: 20rpx;
}
.toast_content_text {
height: 100%;
width: 100%;
color: #fff;
font-size: 28rpx;
text-align: center;
}
```
___
toastTest.wxml很好理解先构建出页面的结构：
```
<template name="toast">
<view class="toast_content_box" wx:if="{{ isHide }}">
<view class="toast_content">
<view class="toast_content_text">
{{content}}
</view>
</view>
</view>
</template>
```
___
pages里toast下的toast.js只是用来注册一个页面不做其他操作
```
Page({
data: {
}
})
```
___

组件里的toast.js 里逻辑是这样的：
```
let _compData = {
'_toast_.isHide': false,// 控制组件显示隐藏
'_toast_.content': ''// 显示的内容
}
let toastPannel = {
// toast显示的方法
show: function (data) {
let self = this;
this.setData({ '_toast_.isHide': true, '_toast_.content': data });
setTimeout(function () {
self.setData({ '_toast_.isHide': false })
}, 3000)
}
}
function ToastPannel() {
// 拿到当前页面对象
let pages = getCurrentPages();
let curPage = pages[pages.length - 1];
this.__page = curPage;
Object.assign(curPage, toastPannel);
// 附加到page上，方便访问
curPage.toastPannel = this;
// 把组件的数据合并到页面的data对象中
curPage.setData(_compData);
return this;
}
module.exports = {
ToastPannel
}
```
主要思想就是把toast组件的属性方法注入到当前页面的实例里，让当前页面可以调用。
____

* 下面就是解决怎么调用的问题了
    在需要使用toast的页面的模板中引入模板：
```
<import src="../../pages/toast/toastTest.wxml"/>
<template is="toast" data="{{ ..._toast_ }}"/>
```
对应的js里onLoad 的时候要实例化一个ToastPannel：
```
  let app = getApp();
  new app.ToastPannel();
```
最后在页面的逻辑方法里就可以使用啦
```
that.show('账号或密码错误');
```
显示如下：
![toast.png](http://upload-images.jianshu.io/upload_images/4315733-3f9f4f1ef24d8dc8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



总结：刚开始用小程序不久，尚未构建一个够规模的大工程，此组件是可以实现自定义显示toast但是缺点也很明显必须每个使用到的页面都得引入模板一次，后面如果有更好的方式再完善吧

