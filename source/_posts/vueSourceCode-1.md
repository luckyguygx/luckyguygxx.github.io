---
title: Object.defineProperty
date: 2018-02-06 14:11:24
type: "tags"
tags: [Vue]
---

#### 给对象添加或修改属性的新方法：Object.defineProperty(obj, prop, descriptor)。该方法对于vue中双向数据绑定的实现起了非常非常非常重要的作用。此篇，来深剖下该方法的用法。

___

*基本的语法：
Object.defineProperty(obj, prop, descriptor) 
参数说明： 
obj：必需。目标对象 
prop：必需。需要定义或修改的属性的名字 
descriptor：必需。目标属性所拥有的特性 
返回值： 
目标对象即第一个参数：obj
___

前两个参数不用多说，下面我们来细究下第三个参数：descriptor。对象里目前存在的属性描述符有两种主要形式：**数据描述符**和**存取描述符**。数据描述符是一个具有值的属性，该值可能是可写的，也可能不是可写的。访问器描述符是由getter-setter函数对描述的属性。**描述符必须是这两种形式之一；不能同时是两者**。

___
###### 数据描述符：
  可设置的特性如下：
   value: 设置属性的值。
   writable: 值是否可以重写。true | false。
   enumerable: 目标属性是否可以被枚举。true | false。
   configurable: 目标属性是否可以被删除或是否可以再次修改特性 true | false。
   * writable：false代表只读。
   ```
     let obj = {};
     Object.defineProperty(obj,"a",{
     value:111,
     writable:false
     });
     console.log(obj.a); //111
     obj.a = 222;
     console.log(obj.a); //111
  ```
* enumberable: 对象的属性是否可以在for...in或者Object.keys()中被枚举。
  ```
   let obj1 = {};
   Object.defineProperty(obj1,"a",{
   value:111,
   enumerable:true
  });
   console.log(Object.keys(obj1));// ["a"]

   let obj2 = {};
   Object.defineProperty(obj2,"a",{
   value:111,
   enumerable:false
   });
   console.log(Object.keys(obj2));// []
  ```
* configurable:该特性表示对象的属性是否可以被删除，以及除writable特性外的其他特性是否可以被修改。

  ```
  var o = {};
  Object.defineProperty(o, "a", { get : function(){return 1;}, 
                                configurable : false } );

  // throws a TypeError
  Object.defineProperty(o, "a", {configurable : true}); 
  // throws a TypeError
  Object.defineProperty(o, "a", {enumerable : true}); 
// throws a TypeError (set was undefined previously)
Object.defineProperty(o, "a", {set : function(){}}); 
// throws a TypeError (even though the new get does exactly the same thing)
Object.defineProperty(o, "a", {get : function(){return 1;}});
// throws a TypeError
Object.defineProperty(o, "a", {value : 12});
//报错：Uncaught TypeError: Cannot redefine property: a

// 下面是true的情况：
var o = {};
Object.defineProperty(o, "a", { get : function(){return 1;}, 
                                configurable : true } );

Object.defineProperty(o, "a", {configurable : true}); 
Object.defineProperty(o, "a", {enumerable : true}); 
Object.defineProperty(o, "a", {set : function(){}}); 
Object.defineProperty(o, "a", {get : function(){return 1;}});
Object.defineProperty(o, "a", {value : 12});

console.log(o.a); // 12
delete o.a; // 删除
console.log(o.a); // undefined

```
**注意点：如果只写了value，这个属性的特性中configurable，enumerable，writable都被默认为false**

###### 存取器描述：

* 基本用法：
```
var obj = {};
Object.defineProperty(obj,"newKey",{ 
get:function (){} | undefined,
set:function (value){} | undefined,
configurable: true | false ,
enumerable: true | false 
});
```
**注意点：当使用了get或set方法，就不允许使用writable和value这两个属性了**
* 实例演示：

  ```
  let obj = {};
  let initValue = 'lala';
  Object.defineProperty(obj,"firstProp",{
  get:function (){ 
  //获取值时触发该函数
  return initValue;
  }, 
  set:function (value){ 
  //设置值时触发该函数
  initValue = value;
  } 
  });
  console.log(obj.firstProp); //hello
  obj.firstProp= 'dulala'; 
  console.log(obj.firstProp);//dulala
  ```
**注意点：get或set不是必须成对出现，任写其一就可以。如果不设置方法，则get和set的默认值为undefined 。**


