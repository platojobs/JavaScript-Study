
#### 函数作为返回值
> 高阶函数除了可以接受函数作为参数外，还可以把函数作为结果值返回。
```javascript
function sum(arr) {
    return arr.reduce(function (x, y) {
        return x + y;
    });
}

sum([1, 2, 3, 4, 5]); // 15
```
但是，如果不需要立刻求和，而是在后面的代码中，根据需要再计算怎么办？可以不返回求和的结果，而是返回求和的函数！
```javascript
function lazy_sum(arr) {
    var sum = function () {
        return arr.reduce(function (x, y) {
            return x + y;
        });
    }
    return sum;
}
var f = lazy_sum([1, 2, 3, 4, 5]); // function sum() 当我们调用lazy_sum()时，返回的并不是求和结果，而是求和函数
f(); // 15 调用函数f时，才真正计算求和的结果
```
在这个例子中，我们在函数`lazy_sum`中又定义了函数`sum`，并且，内部函数`sum`可以引用外部函数`lazy_sum`的参数和局部变量，当`lazy_sum`返回函数sum时，相关参数和变量都保存在返回的函数中，这种称为`“闭包（Closure）”`的程序结构拥有极大的威力。
请再注意一点，当我们调用`lazy_sum()`时，**每次调用都会返回一个新的函数**，即使传入相同的参数:
```javascript
var f1 = lazy_sum([1, 2, 3, 4, 5]);
var f2 = lazy_sum([1, 2, 3, 4, 5]);
f1 === f2; // false  f1()和f2()的调用结果互不影响。
```
---------
#### 闭包

> 注意到返回的函数在其定义内部引用了局部变量arr，所以，当一个函数返回了一个函数后，其内部的局部变量还被新函数引用，所以，闭包用起来简单，实现起来可不容易。
另一个需要注意的问题是，返回的函数并没有立刻执行，而是直到调用了`f()`才执行。我们来看一个例子:
```javascript
function count() {
    var arr = [];
    for (var i=1; i<=3; i++) {
        arr.push(function () {
            return i * i;
        });
    }
    return arr;
}

var results = count();
var f1 = results[0];
var f2 = results[1];
var f3 = results[2];
/*在上面的例子中，每次循环，都创建了一个新的函数，然后，把创建的3个函数都添加到一个Array中返回了。
你可能认为调用f1()，f2()和f3()结果应该是1，4，9，但实际结果是：*/
f1(); // 16
f2(); // 16
f3(); // 16
/*全部都是16！原因就在于返回的函数引用了变量i，但它并非立刻执行。等到3个函数都返回时，它们所引用的变量i已经变成了4，因此最终结果为16.*/
```
>返回闭包时牢记的一点就是：**返回函数不要引用任何循环变量，或者后续会发生变化的变量。

    如果一定要引用循环变量怎么办？方法是再创建一个函数，用该函数的参数绑定循环变量当前的值，无论该循环变量后续如何更改，已绑定到函数参数的值不变： 
    
    
```javascript
    function count() {
    var arr = [];
    for (var i=1; i<=3; i++) {
        arr.push((function (n) {
            return function () {
                return n * n;
            }
        })(i));
    }
    return arr;
}
      var results = count();
      var f1 = results[0];
      var f2 = results[1];
      var f3 = results[2];

f1(); // 1
f2(); // 4
f3(); // 9
```
注意这里用了一个“创建一个匿名函数并立刻执行”的语法:
```javascript
(function (x) {
    return x * x;
})(3); // 9
```
理论上讲，创建一个匿名函数并立刻执行可以这么写：
```javascript
function (x) { return x * x } (3);
```
但是由于JavaScript语法解析的问题，会报SyntaxError错误，因此需要用括号把整个函数定义括起来：
```javascript
(function (x) { return x * x }) (3);
```
通常，一个立即执行的匿名函数可以把函数体拆开，一般这么写：
```javascript
(function (x) {
    return x * x;
})(3);
```

>在面向对象的程序设计语言里，比如Java和C++，要在对象内部封装一个私有变量，可以用private修饰一个成员变量。
在没有class机制，只有函数的语言里，借助闭包，同样可以封装一个私有变量。我们用JavaScript创建一个计数器：
```javascript
function create_counter(initial) {
    var x = initial || 0;
    return {
        inc: function () {
            x += 1;
            return x;
        }
    }
}
```
它的使用如下：
```javascript
var c1 = create_counter();
c1.inc(); // 1
c1.inc(); // 2
c1.inc(); // 3

var c2 = create_counter(10);
c2.inc(); // 11
c2.inc(); // 12
c2.inc(); // 13
```
>在返回的对象中，实现了一个闭包，该闭包携带了局部变量x，并且，从外部代码根本无法访问到变量x。换句话说，闭包就是携带状态的函数，并且它的状态可以完全对外隐藏起来。
--------------

**闭包还可以把多参数的函数变成单参数的函数。例如，要计算xy可以用`Math.pow(x, y)`函数，不过考虑到经常计算x2或x3，我们可以利用闭包创建新的函数`pow2`和`pow3`：
```javascript
function make_pow(n) {
    return function (x) {
        return Math.pow(x, n);
    }
}
// 创建两个新函数:
var pow2 = make_pow(2);
var pow3 = make_pow(3);

console.log(pow2(5)); // 25
console.log(pow3(7)); // 343
```
#### 趣味站
很久很久以前，有个叫阿隆佐·邱奇的帅哥，发现只需要用函数，就可以用计算机实现运算，而不需要`0`、`1`、`2`、`3`这些数字和`+`、`-`、`*`、`/`这些符号
```javascript
// 定义数字0:
var zero = function (f) {
    return function (x) {
        return x;
    }
};

// 定义数字1:
var one = function (f) {
    return function (x) {
        return f(x);
    }
};

// 定义加法:
function add(n, m) {
    return function (f) {
        return function (x) {
            return m(f)(n(f)(x));
        }
    }
}
// 计算数字2 = 1 + 1:
var two = add(one, one);

// 计算数字3 = 1 + 2:
var three = add(one, two);

// 计算数字5 = 2 + 3:
var five = add(two, three);
// 计算数字6 = 3 + 3
var six = add(three, three);

// 你说它是3就是3，你说它是5就是5，你怎么证明？

// 呵呵，看这里:

// 给3传一个函数,会打印3次:
(three(function () {
    console.log('print 3 times');
}))();

// 给5传一个函数,会打印5次:
(five(function () {
    console.log('print 5 times');
}))();

// 给6传一个函数,会打印6次:
(six(function () {
    console.log('print 6 times');
}))();
// 继续接着玩一会...
//运行结果：
/*
print 3 times
print 3 times
print 3 times
print 5 times
print 5 times
print 5 times
print 5 times
print 5 times
print 6 times
print 6 times
print 6 times
print 6 times
print 6 times
print 6 times
*/
```
---------
#### Arrow Function（箭头函数）
为什么叫Arrow Function？因为它的定义用的就是一个箭头:
```javascript
x => x * x
```
等价于：
```javscript
function (x) {
    return x * x;
}
```
>**箭头函数相当于匿名函数，并且简化了函数定义。箭头函数有两种格式，一种像上面的，只包含一个表达式，连`{ ... }`和`return`都省略掉了。还有一种可以包含多条语句，这时候就不能省略`{ ... }`和`return`：
```javascript
x => {
    if (x > 0) {
        return x * x;
    }
    else {
        return - x * x;
    }
}
```
如果参数不是一个，就需要用括号`()`括起来：
```javascript
// 两个参数:
(x, y) => x * x + y * y

// 无参数:
() => 3.14

// 可变参数:
(x, y, ...rest) => {
    var i, sum = x + y;
    for (i=0; i<rest.length; i++) {
        sum += rest[i];
    }
    return sum;
}
```
>如果要返回一个对象，就要注意，如果是单表达式，这么写的话会报错：
```javascript
// SyntaxError:
x => { foo: x }
```
>因为和函数体的`{ ... }`有语法冲突，所以要改为：
```javascript
// ok:
x => ({ foo: x })
```
---------
#### this `箭头函数内部的this`
箭头函数看上去是匿名函数的一种简写，但实际上，箭头函数和匿名函数有个明显的区别：箭头函数内部的`this`是词法作用域，由上下文确定。
回顾前面的例子，由于JavaScript函数对`this`绑定的错误处理，下面的例子无法得到预期结果
```javascript
var obj = {
    birth: 1990,
    getAge: function () {
        var b = this.birth; // 1990
        var fn = function () {
            return new Date().getFullYear() - this.birth; // this指向window或undefined
        };
        return fn();
    }
};

```
>现在，箭头函数完全修复了`this`的指向，`this`总是指向词法作用域，也就是外层调用者`obj`：
```javascript
var obj = {
    birth: 1990,
    getAge: function () {
        var b = this.birth; // 1990
        var fn = () => new Date().getFullYear() - this.birth; // this指向obj对象
        return fn();
    }
};
obj.getAge(); // 25
```
如果使用箭头函数，以前的那种`hack`写法:`var that = this;`就不再需要了。
由于`this`在箭头函数中已经按照词法作用域绑定了，所以，用`call()`或者`apply()`调用箭头函数时，无法对`this`进行绑定，即传入的第一个参数被忽略：
```javascript
var obj = {
    birth: 1990,
    getAge: function (year) {
        var b = this.birth; // 1990
        var fn = (y) => y - this.birth; // this.birth仍是1990
        return fn.call({birth:2000}, year);
    }
};
obj.getAge(2015); // 25

```
------

#### generator（生成器）

generator（生成器）是ES6标准引入的新的数据类型。一个generator看上去像一个函数，但可以返回多次。
ES6定义generator标准的哥们借鉴了Python的generator的概念和语法;
`generator`跟函数很像，定义如下:

```javascript
function* foo(x) {
    yield x + 1;
    yield x + 2;
    return x + 3;
}
```
-----

`generator`和函数不同的是，`generator`由`function*`定义（注意多出的`*`号），并且，除了`return`语句，还可以用`yield`返回多次。
大多数同学立刻就晕了，`generator`就是能够返回多次的“函数”？返回多次有啥用？me还是举个栗子吧。一个著名的斐波那契数列为例:
 `0 1 1 2 3 5 8 13 21 34 ...`
要编写一个产生斐波那契数列的函数，可以这么写：
```javascript
function fib(max) {
    var
        t,
        a = 0,
        b = 1,
        arr = [0, 1];
    while (arr.length < max) {
        [a, b] = [b, a + b];
        arr.push(b);
    }
    return arr;
}

// 测试:
fib(5); // [0, 1, 1, 2, 3]
fib(10); // [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]
```
函数只能返回一次，所以必须返回一个`Array`。但是，如果换成`generator`，就可以一次返回一个数，不断返回多次。用`generator`改写如下:
```javascript
function* fib(max) {
    var
        t,
        a = 0,
        b = 1,
        n = 0;
    while (n < max) {
        yield a;
        [a, b] = [b, a + b];
        n ++;
    }
    return;
}
```
直接调用试试：
```javascript
fib(5); // fib {[[GeneratorStatus]]: "suspended", [[GeneratorReceiver]]: Window}
```
直接调用一个`generator`和调用函数不一样，`fib(5)`仅仅是创建了一个`generator`对象，还没有去执行它。
调用`generator`对象有两个方法，一是不断地调用`generator`对象的`next()`方法
```javascript
var f = fib(5);
f.next(); // {value: 0, done: false}
f.next(); // {value: 1, done: false}
f.next(); // {value: 1, done: false}
f.next(); // {value: 2, done: false}
f.next(); // {value: 3, done: false}
f.next(); // {value: undefined, done: true}

```
>`next()`方法会执行`generator`的代码，然后，每次遇到`yield x`;就返回一个对象`{value: x, done: true/false}`，然后“暂停”。返回的value就是`yield`的返回值，`done`表示这个`generator`是否已经执行结束了。如果`done`为`true`，则value就是`return`的返回值。
当执行到`done`为`true`时，这个`generator`对象就已经全部执行完毕，不要再继续调用`next()`了。
第二个方法是直接用`for ... of`循环迭代`generator`对象，这种方式不需要我们自己判断`done`：
```javascript
function* fib(max) {
    var
        t,
        a = 0,
        b = 1,
        n = 0;
    while (n < max) {
        yield a;
        [a, b] = [b, a + b];
        n ++;
    }
    return;
}
for (var x of fib(10)) {
    console.log(x); // 依次输出0, 1, 1, 2, 3, ...
}
/*
输出结果：
0
1
1
2
3
5
8
13
21
34
*/

```
##### generator和普通函数相比，有什么用？
因为`generator`可以在执行过程中多次返回，所以它看上去就像一个可以记住执行状态的函数，利用这一点，写一个`generator`就可以实现需要用面向对象才能实现的功能。例如，用一个对象来保存状态，得这么写:
```javascript
var fib = {
    a: 0,
    b: 1,
    n: 0,
    max: 5,
    next: function () {
        var
            r = this.a,
            t = this.a + this.b;
        this.a = this.b;
        this.b = t;
        if (this.n < this.max) {
            this.n ++;
            return r;
        } else {
            return undefined;
        }
    }
};
```
>用对象的属性来保存状态，相当繁琐。

`generator`还有另一个巨大的好处，就是把异步回调代码变成“同步”代码。这个好处要等到后面学了**AJAX**以后才能体会到。
没有`generator`之前的黑暗时代，用**AJAX**时需要这么写代码:
```javascript
ajax('http://url-1', data1, function (err, result) {
    if (err) {
        return handle(err);
    }
    ajax('http://url-2', data2, function (err, result) {
        if (err) {
            return handle(err);
        }
        ajax('http://url-3', data3, function (err, result) {
            if (err) {
                return handle(err);
            }
            return success(result);
        });
    });
});
```
> 回调越多，代码越难看。

***有了generator的美好时代，用AJAX时可以这么写：
```javascript
try {
    r1 = yield ajax('http://url-1', data1);
    r2 = yield ajax('http://url-2', data2);
    r3 = yield ajax('http://url-3', data3);
    success(r3);
}
catch (err) {
    handle(err);
}
```
> 看上去是同步的代码，实际执行是异步的。
