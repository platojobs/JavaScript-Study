>JavaScript的默认对象表示方式`{}`可以视为其他语言中的`Map`或`Dictionary`的数据结构，即一组键值对。
>但是JavaScript的对象有个小问题，就是键必须是字符串。但实际上`Number`或者其他数据类型作为键也是非常合理的。
为了解决这个问题，最新的`ES6`规范引入了新的数据类型Map。要测试你的浏览器是否支持`ES6`规范，请执行以下代码，如果浏览器报`ReferenceError`错误，那么你需要换一个支持`ES6`的浏览器.
Persistence is the key to learning.

[学习贵在坚持](https://github.com/cuishengxi)

If you don't want to waste your life, you should spend it learning.

[如果不想虚度一生，那就要学习一辈子](https://github.com/cuishengxi)

#### Map
[学习贵在坚持](https://github.com/cuishengxi)

是一组键值对的结构，具有极快的查找速度。
```javascript
var m = new Map([['Michael', 95], ['Bob', 75], ['Tracy', 85]]);
m.get('Michael'); // 95
```
初始化`Map`需要一个二维数组，或者直接初始化一个空`Map`。`Map`具有以下方法:
```javascript
var m = new Map(); // 空Map
m.set('Adam', 67); // 添加新的key-value
m.set('Bob', 59);
m.has('Adam'); // 是否存在key 'Adam': true
m.get('Adam'); // 67
m.delete('Adam'); // 删除key 'Adam'
m.get('Adam'); // undefined
```
由于一个key只能对应一个value，所以，多次对一个key放入value，后面的值会把前面的值冲掉：
```javascript
var m = new Map();
m.set('Adam', 67);
m.set('Adam', 88);
m.get('Adam'); // 88
```

#### Set

`Set`和`Map`类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在`Set`中，没有重复的key。

要创建一个`Set`，需要提供一个`Array`作为输入，或者直接创建一个空`Set`：
```javascript
var s1 = new Set(); // 空Set
var s2 = new Set([1, 2, 3]); // 含1, 2, 3
```
重复元素在`Set`中自动被过滤:
```javascript
var s = new Set([1, 2, 3, 3, '3']);
s; // Set {1, 2, 3, "3"}
```
通过`add(key)`方法可以添加元素到`Set`中，可以重复添加，但不会有效果：
```javascript
s.add(4);
s; // Set {1, 2, 3, 4}
s.add(4);
s; // 仍然是 Set {1, 2, 3, 4}
```
通过`delete(key)`方法可以删除元素：
```javascript
var s = new Set([1, 2, 3]);
s; // Set {1, 2, 3}
s.delete(3);
s; // Set {1, 2}
```
>`Map`和`Set`是ES6标准新增的数据类型，请根据浏览器的支持情况决定是否要使用。

#### iterable类型
遍历`Array`可以采用下标循环，遍历`Map`和`Set`就无法使用下标。为了统一集合类型，ES6标准引入了新的`iterable`类型，`Array`、`Map`和`Set`都属于`iterable`类型。

具有iterable类型的集合可以通过新的`for ... of`循环来遍历。
```javascript
var a = ['A', 'B', 'C'];  //数组
var s = new Set(['A', 'B', 'C']); //集合
var m = new Map([[1, 'x'], [2, 'y'], [3, 'z']]);
for (var x of a) { // 遍历Array
    console.log(x);
}
for (var x of s) { // 遍历Set
    console.log(x);
}
for (var x of m) { // 遍历Map
    console.log(x[0] + '=' + x[1]);
}
```

#### `for ... of`循环和`for ... in`循环有何区别？

`for ... in`循环由于历史遗留问题，它遍历的实际上是对象的属性名称。一个`Array`数组实际上也是一个对象，它的每个元素的索引被视为一个属性。

当我们手动给Array对象添加了额外的属性后，`for ... in`循环将带来意想不到的意外效果：
```javascript
var a = ['A', 'B', 'C'];
a.name = 'Hello';
for (var x in a) {
    console.log(x); // '0', '1', '2', 'name'
}
```
>`for ... in`循环将把`name`包括在内，但`Array`的`length`属性却不包括在内。
>`for ... of`循环则完全修复了这些问题，它只循环集合本身的元素

```javascript
var a = ['A', 'B', 'C'];
a.name = 'Hello';
for (var x of a) {
    console.log(x); // 'A', 'B', 'C'
}
```
这就是为什么要引入新的`for ... of`循环。

然而，更好的方式是直接使用`iterable`内置的`forEach`方法，它接收一个函数，每次迭代就自动回调该函数。以Array为例：
```javascript
var a = ['A', 'B', 'C'];
a.forEach(function (element, index, array) {
    // element: 指向当前元素的值
    // index: 指向当前索引
    // array: 指向Array对象本身
    console.log(element + ', index = ' + index);
    /*
    A, index = 0
    B, index = 1
    C, index = 2
    */
    
});
```
>注意，`forEach()`方法是`ES5.1`标准引入的，你需要测试浏览器是否支持。
`Set`与`Array`类似，但`Set`没有索引，因此回调函数的前两个参数都是元素本身
```javascript
var s = new Set(['A', 'B', 'C']);
s.forEach(function (element, sameElement, set) {
    console.log(element);
    /*
    A
    B
    C
    */
});
```
>`Map`的回调函数参数依次为`value`、`key`和`Map`本身
```javascript
var m = new Map([[1, 'x'], [2, 'y'], [3, 'z']]);
m.forEach(function (value, key, map) {
    console.log(value);
    /*
    x
    y
    z
    */
});
```
[学习贵在坚持](https://github.com/cuishengxi)
如果对某些参数不感兴趣，由于JavaScript的函数调用不要求参数必须一致，因此可以忽略它们。例如，只需要获得Array的element
```javascript
var a = ['A', 'B', 'C'];
a.forEach(function (element) {
    console.log(element);
    /*
    A
    B
    C
    */
});
```
Persistence is the key to learning.

[学习贵在坚持](https://github.com/cuishengxi)

If you don't want to waste your life, you should spend it learning.

[如果不想虚度一生，那就要学习一辈子](https://github.com/cuishengxi)
