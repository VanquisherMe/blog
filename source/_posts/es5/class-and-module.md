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
> [实例类] instanceof [构造函数]

 instanceof 检验的是 【左操作数】 是否继承自 【左操作数】.prototype

```
    function A(from ,to) {
            this.from=from
            this.to =to
        }

        A.prototype.sum=function () {
            return this.from + this.to
        }

        function B(from ,to) {
            this.from=from+2
            this.to =to+2
        }

        //B的原型继承A的原型
        B.prototype =  A.prototype;


        var a=new A(1 ,3),
            b=new B(1 ,3)

        console.log(a.sum())    //4
        console.log(b.sum())   //8


        console.log(a instanceof A)  //true
        console.log(b instanceof A)  //true
        console.log(a instanceof B)  //true

        //原型继承
        function inherit(proto) {
            if(proto == null) throw TypeError();
            if(Object.create) return Object.create(proto);
            var t = typeof proto;
            if(t!=='object' && t!=='function') throw TypeError();
            var F = function() {};
            F.prototype = proto;
            return new F();
        }

        function C(from ,to) {
            this.from=from+3
            this.to =to+3
        }

        C.prototype = inherit(A.prototype)

        var c= new C(1,3)
        console.log(c.sum())
        console.log(c instanceof A)  //true
        console.log(c instanceof B)  //true
```

# isPrototypeOf() 方法

如果你想检测对象的原型链上是否存在某个*特定的原型对象(注意是对象)*,有没有不使用构造函数作为中介的方法呢?

拿1.的例子
```
    range.methods.isPrototypeOf(r) //true

```

# constructor 属性

> 通过检验实例类的构造函数名,来识别对象属于某个类的方法

注意:如果自定义的类原型上没有设置 constructor 属性,那么它们实例的 类就没有constructor 属性
```
function typeAndValue(x) {
        if(x == null) return ""; //

        switch (c.constructor){
            case Number: return "Number: "+x;
            case String: return "String: "+x;
            case Date: return "Date: "+x;
            case RegExp: return "RegExp: "+x;
            case Complex: return "Complex: "+x; //自定义
        }
    }
```




