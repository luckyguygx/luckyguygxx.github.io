---
title: TypeScript类型推论注意事项
date: 2018-01-10 09:55:46
type: "tags"
tags: [TypeScript]
---
> 文中简称TypeScript为TS

#### 类型推论定义

在TS中，如果没有明确的指定类型，TS会依照类型推论的规则推断出一个类型，这就是类型推断。比如以下代码：
```
let luckyNumber = 'three';
luckyNumber = 7;

```
编译以上代码就会发现报错：error TS2322: Type '7' is not assignable to type 'string'.
因为luckyNumber被TS推断为了string类型，以上代码就等价于以下代码：
```
let luckyNumber:string = 'three';
luckyNumber = 7;

```
#### 注意点
 **如果在定义变量的时候没有直接赋值，那么不管之后是否赋值，都会被推断为any类型**
比如：
```
let luckyNumber;
luckyNumber = 3;
luckyNumber ='three'

```
编译完全不会报错，因为在定义的时候luckyNumber被推断为了any类型，编译完的js内容为：
```
var luckyNumber;
luckyNumber = 3;
luckyNumber = 'three';

```