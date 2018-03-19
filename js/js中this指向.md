## [js中this指向](http://www.ruanyifeng.com/blog/2010/04/using_this_keyword_in_javascript.html)

this只能在函数内部使用，一个总的原则：this的指向是调用函数的那个对象。

* 情况一：纯粹的函数调用

```
function test() {
    this.x = 1;
    console.log(this.x);
}

text(); // 1
```

为了证明this是全局对象，对代码做一些改变：
```
var x = 1;
function test() {
    alert(this.x);
}

text(); // 1
```

再改变一下：
```
var x = 1;

function test() {
    this.x = 0;
    console.log(this.x);
}

test(); // 0
console.log(x); // 0
```

* 情况二： 作为对象方法的调用

函数还可以作为某个对象的方法调用，这时this就指向这个上级对象

```
function test() {
    console.log(this.x);
}

var o = {};
o.x = 1;
o.m = test;
o.m(); // 1
```

* 情况三： 作为构造函数调用

通过构造函数生成一个新对象，this就指向这个新对象

```
function test() {
    this.x = 1;
}

var o = new test();
console.log(o.x); // 1
```

为了表明this不是全局对象，对代码做一些改变：

```
var x = 2;
function test() {
    this.x = 1;
    console.log(this.x);
}

var o = new test();
console.log(x); // 2
```
运行结果为2，表明全局变量x的值没有改变

* 情况四： apply调用

apply()是用来改变函数的调用对象，它的第一个参数表示改变后的调用这个函数的对象。

```
var x = 0;
function test() {
    console.log(this.x);
}

var o = {};
o.x = 1;
o.m = test;
o.m.apply(); // 0
```
apply()的参数为空，默认调用全局对象，因此结果为0，证明this指向全局对象。

如果把最后一行代码修改为
```
o.m.apply(o); // 1
```
此时，this代表的就是对象o



