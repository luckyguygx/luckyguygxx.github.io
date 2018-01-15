---
title: HTML5 为什么只需要写 <!DOCTYPE HTML>
date: 2016-03-10 20:30:16 
tags: [html]
---
> <!DOCTYPE>声明必须在文档的第一行，位于 <html> 标签之前，
<!DOCTYPE> 声明不是 HTML 标签。作用是告诉浏览器用哪种模式来渲染文档。<!DOCTYPE> 声明没有结束标签且对大小写不敏感

* 严格模式也称标准模式，指浏览器会按照W3C的标准解析执行代码。
* 混杂模式也称为怪异模式或者兼容模式，是一种向后兼容的解析方法，浏览器会按照自己的方式去解析执行代码。用此种模式会影响html的排版。
----
>在 HTML 4.01 中，<!DOCTYPE> 声明引用 DTD，因为 HTML 4.01 基于 SGML。DTD 规定了标记语言的规则，这样浏览器才能正确地呈现内容。
HTML5 不基于 SGML，所以不需要引用 DTD。

-----

###### HTML 4.01 与 HTML5 之间的差异：
 HTML 4.01 中有三种 <!DOCTYPE> 声明。在 HTML5 中只有一种：
html5：
`<!DOCTYPE html>`

html4:
HTML 4.01 Strict(该 DTD 包含所有 HTML 元素和属性，但不包括展示性的和弃用的元素（比如 font）。不允许框架集（Framesets）。)
`<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">`

HTML 4.01 Transitional(该 DTD 包含所有 HTML 元素和属性，包括展示性的和弃用的元素（比如 font）。不允许框架集（Framesets）。)
`<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" 
"http://www.w3.org/TR/html4/loose.dtd">`

HTML 4.01 Frameset(该 DTD 等同于 HTML 4.01 Transitional，但允许框架集内容。)
`<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" 
"http://www.w3.org/TR/html4/frameset.dtd">`

html每种元素允许出现在哪种文档类型中详细列表，点此查看：
[元素详细列表](http://www.w3school.com.cn/tags/html_ref_dtd.asp)