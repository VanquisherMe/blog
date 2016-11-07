title: javascript-类和模块
date: 2016-05-07 18:44:12
toc: true
tags:
- javascript,类和模块
categories: ES5
---

# 工厂函数
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

    function range(from , to) {
        //使用 inherit
        var r = inherit(range.methods);
        r.from = from;
        r.to = to;
        //返回新对象
        return r
    }

    //原型对象定义方法,这些方法为每个范围对象所继承
    range.methods ={
        //如果x在范围内,择返回true,否则返回false
        // 这个方法可以比较数字范围,也可以比较字符串和日期的范围
        includes:function (x) {
            return this.from <= x && x <= this.to;
        },
        //对于范围内的每个整数调用一次f
        //这个方法只可以用作数字范围
        foreach: function (f) {
            for(var x= Math.ceil(this.from); x <= this.to; x++) f(x)
        },
        //返回表示这个范围的字符串
        toString:function () {
            return "(" + this.form + "......" + this.to + ")";
        }
    }

    function log(x) {
        console.log(x)
    }

    var r = range(1,3)            //创建一个范围对象
    r.includes(2)                 //=> true:2这个范围内
    r.foreach(log)                 //输出 1 2 3
    console.log(r)                // (1 ... 3)
```

# instanceof 运算符
```
.compact([0, 1, false, 2, ‘’, 3]);
=> [1, 2, 3]
```