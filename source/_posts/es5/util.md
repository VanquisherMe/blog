title: javascript-常用函数集合
date: 2016-05-07 18:44:12
toc: true
tags:
- javascript,常用函数集合
categories: ES5
---



# 返回对象的类名
```
function  classof(o) {
        console.log(Object.prototype.toString.call(o))
        return Object.prototype.toString.call(o).slice(8,-1);
    }


```

# 返回函数的名字
```
//返回函数的名字(可能是字符串),不是函数的话返回null
 Function.prototype.getName =function () {
        if("name" in this) return this.name;

        return this.name = this.toString().match( /function\s*([^(]*)\(/)[1];
    }


```

# 原型式继承
```
    // 返回一个继承自原型对象proto的属性的新对象
    // 这里可以用到ES5的Object.create()函数
    function inherit(proto) {
    //proto是一个对象，但不能是null
        if(proto == null) throw TypeError();
        if(Object.create) return Object.create(proto); //如果Object.create()存在,使用它
        var t = typeof proto; //否则进一步检查
        if(t!=='object' && t!=='function') throw TypeError();
        var F = function() {}; // 定义一个空构造函数
        F.prototype = proto; // 将其原型属性设置为proto
        return new F(); // 使用F()创建proto的继承对象
    }
```
