---
title: CSS选择器的浏览器支持
date: 2016-11-08 16:02:59
tags:
- css,浏览器兼容
categories: css
---
原地址链接:[http://labs.qianduan.net/css-selector](http://labs.qianduan.net/css-selector)
css兼容表:[http://caniuse.mojijs.com/Home/Html)

# css1
![css1](/images/css1.png)

# css2.1
![css2.1](/images/css2.1.png)

# css3
![css3](/images/css3.png)

1. :hover 在IE6中只有a元素可用。
2. E:empty 貌似在webkit核心浏览器中有些小bug。
3. 如果这个bug依然存在，不太确定如何测试。
4. IE6不支持.class1{}.class2{}双类选择器。

## IE8注意事项：
* E[attr]选择器在值为空的时候或者写错的时候，将不会生效；
* IE8支持CSS2.1的所有属性，支持伪类，但是不支持伪元素。

## IE8中的IE7兼容模式
* E[attr] 和IE8一样，值为空或写错的时候，无效；
* E[attr~=val]这里唯一需要注意的是，属性的值，区分大小写；
* E[attr|=val]IE7有一些大小写敏感的问题，但是通常可以正常使用；
* :first-child IE7 会将一个注释或者文字节点当成first-child，而不是只有元素才是“子”元素。所以，如果在第一个子元素前有注释或文字，IE7会匹配之而不是去匹配第一个子元素。

## Safari/Chrome
* Safari3.2(事实上可以追溯到3.1)以上的版本已经完全的支持所有CSS选择器了。
* Safari3.0基本上对CSS 2的选择器支持很好，但不支持CSS3大部分新增的选择器，而且对属性选择器的支持不是很完整。
* iPhone中的Safari有3.0和3.2两个版本，对CSS的支持情况与PC/Mac版的支持情况一致。
* Android系统自带的浏览器基本上也是基于webkit核心的，其对于CSS选择器的支持情况待测。