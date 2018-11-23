
### Higher-order function
~~如果不想虚度一生，那就要学习一辈子~~
> JavaScript的函数其实都指向某个变量。既然变量可以指向函数，函数的参数能接收变量，那么一个函数就可以接收另一个函数作为参数，这种函数就称之为(Higher-order function)高阶函数.
```javascript
function add(x, y, f) {
    return f(x) + f(y);
}
```
当我们调用`add(-5, 6, Math.abs)`时，参数`x`，`y`和`f`分别接收`-5`，`6`和函数`Math.abs`，根据函数定义，我们可以推导计算过程为

```javascript
x = -5;
y = 6;
f = Math.abs;
f(x) + f(y) ==> Math.abs(-5) + Math.abs(6) ==> 11;
return 11;

```
代码验证下：
```javascript
var x = add(-5, 6, Math.abs); // 11
console.log(x);
/*
11
*/
```
> **编写高阶函数，就是让函数的参数能够接收别的函数。

-----

#### map

举例说明，比如我们有一个函数`f(x)=x2`，要把这个函数作用在一个数组`[1, 2, 3, 4, 5, 6, 7, 8, 9]`上，就可以用`map`实现如下:
![tupian](https://cdn.liaoxuefeng.com/cdn/files/attachments/0013879622109990efbf9d781704b02994ba96765595f56000/0)
