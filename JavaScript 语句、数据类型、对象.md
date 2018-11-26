#### JavaScript 语句
[学习贵在坚持](https://github.com/cuishengxi)
JavaScript 语句向浏览器发出的命令。语句的作用是告诉浏览器该做什么。
下面的 JavaScript 语句向 `id="demo"` 的 HTML 元素输出文本 `"Hello World"`：

分号 `;`
`分号`用于分隔 JavaScript 语句。
>通常我们在每条可执行的语句结尾添加分号。
使用`分号`的另一用处`是在一行中编写多条语句`。
提示：您也可能看到不带有分号的案例。
在 JavaScript 中，`用分号来结束语句是可选的`。

##### JavaScript 代码
JavaScript 代码（或者只有 JavaScript）是 JavaScript 语句的序列。
浏览器会按照编写顺序来执行每条语句。
本例将操作两个 HTML 元素：
```JavaScript
document.getElementById("demo").innerHTML="Hello World";
document.getElementById("myDIV").innerHTML="How are you?";
```

##### JavaScript 代码块
JavaScript 语句通过代码块的形式进行组合。
块由左花括号开始，由右花括号结束。
***块的作用是使语句序列一起执行***。
JavaScript 函数是将语句组合在块中的典型例子。
下面的例子将运行可操作两个 HTML 元素的函数：
```JavaScript
function myFunction()
{
document.getElementById("demo").innerHTML="Hello World";
document.getElementById("myDIV").innerHTML="How are you?";
}
```
##### JavaScript 对大小写敏感。
JavaScript `对大小写是敏感的`。
>当编写 JavaScript 语句时，请留意是否关闭大小写切换键。
函数 getElementById 与 getElementbyID 是不同的。
同样，变量 myVariable 与 MyVariable 也是不同的。

##### 空格
***注：JavaScript 会忽略多余的空格。您可以向脚本添加空格，来提高其可读性。*** 下面的两行代码是等效的：
[学习贵在坚持](https://github.com/cuishengxi)
```javascript
var name="Hello";
var name = "Hello";
```
对代码行进行折行
您可以在文本字符串中使用反斜杠对代码行进行换行。下面的例子会正确地显示：
```javascript
document.write("Hello \
World!");   //正确的的折行

document.write \
("Hello World!");  //错误的折行
```

>提示：JavaScript 是脚本语言。浏览器会在读取代码时，逐行地执行脚本代码。而对于传统编程来说，会在执行前对所有代码进行编译。

#### 变量
 变量是存储信息的容器
 
 变量可以使用短名称（比如 x 和 y），也可以使用描述性更好的名称（比如 age, sum, totalvolume）。
+ 变量必须以字母开头
+ 变量也能以 $ 和 _ 符号开头（`不过我们不推荐这么做`）
+ 变量名称对大小写敏感（y 和 Y 是不同的变量）
>提示：JavaScript 语句和 JavaScript 变量都对大小写敏感。
一个好的编程习惯是，在代码开始处，统一对需要的变量进行声明。
>
 您可以在一条语句中声明很多变量。该语句以 var 开头，并使用逗号分隔变量即可：
 ```javascript
var name="Gates", age=56, job="CEO";
//也可以多行
var name="Gates",
age=56,
job="CEO";
```
+ Value = undefined
在计算机程序中，经常会声明无值的变量。未使用值来声明的变量，其值实际上是 undefined。
在执行过以下语句后，变量 carname 的值将是 undefined：
```javascript
var carname;
```
+ 重新声明 JavaScript 变量
如果重新声明 JavaScript 变量，该变量的值不会丢失：
在以下两条语句执行后，变量 carname 的值依然是 "Volvo"：
```javascript
var carname="Volvo";
var carname;
```
 
#### 数据类型
字符串、数字、布尔、数组、对象、Null、Undefined

当您向变量分配文本值时，应该用双引号或单引号包围这个值。
当您向变量赋的值是数值时，不要使用引号。如果您用引号包围数值，该值会被作为文本来处理。
#### 1.字符串
字符串是存储字符（比如 "Bill Gates"）的变量。
字符串可以是引号中的任意文本。您可以使用单引号或双引号：
```javascript
var answer="Nice to meet you!";
var answer="He is called 'Bill'";
var answer='He is called "Bill"';  //内有引号的字符串

```
JavaScript的字符串就是用''或""括起来的字符表示。

如果`'`本身也是一个字符，那就可以用`""`括起来，比如`"I'm OK"`包含的字符是`I`，`'`，`m`，空格，`O`，`K`这6个字符。

如果字符串内部既包含'又包含"怎么办？可以用转义字符`\`来标识:
```javascript
'I\'m\"OK\"!'
```
转义字符`\`可以转义很多字符，比如`\n`表示换行，`\t`表示制表符，字符`\`本身也要转义，所以`\\`表示的字符就是`\`。
由于多行字符串用`\n`写起来比较费事，所以最新的ES6标准新增了一种多行字符串的表示方法，用反引号  \` ... \`表示;
>模板字符串
>要把多个字符串连接起来，可以用`+`号连接：

```javascript
var name = '小明';
var age = 20;
var message = '你好, ' + name + ', 你今年' + age + '岁了!';
alert(message);
```
如果有很多变量需要连接，用`+`号就比较麻烦。ES6新增了一种模板字符串，表示方法和上面的多行字符串一样，但是它会自动替换字符串中的变量：
```javascript
var name = '小明';
var age = 20;
var message = `你好, ${name}, 你今年${age}岁了!`;
alert(message);
```
##### 操作字符串

要获取字符串某个指定位置的字符，使用类似Array的下标操作，索引号从0开始:

JavaScript为字符串提供了一些常用方法:
+ toUpperCase  把一个字符串全部变为大写
+ toLowerCase  把一个字符串全部变为小写
+ indexOf  会搜索指定字符串出现的位置
+ substring 例子：substring(1，3)返回指定索引区间的子串，包含左边索引，不包含右边索引
```javascript
var s = 'hello, world'
s.substring(0, 5); // 从索引0开始到5（不包括5），返回'hello'
s.substring(7); // 从索引7开始到结束，返回'world'
```
[学习贵在坚持](https://github.com/cuishengxi)
#### 2.数字  
数字可以带小数点，也可以不带；极大或极小的数字可以通过科学（指数）计数法来书写：`var z=123e-5`;     

#### 3.布尔 

布尔（逻辑）只能有两个值：true 或 false。布尔常用在条件测试中

#### 4.数组

JavaScript的Array可以包含任意数据类型，并通过索引来访问每个元素；
>请注意，直接给Array的length赋一个新的值会导致Array大小的变化
>可以通过索引把对应的元素修改为新的值，因此，对Array的索引进行赋值会直接修改这个Array
>如果通过索引赋值时，索引超过了范围，同样会引起Array大小的变化

    大多数其他编程语言不允许直接改变数组的大小，越界访问索引会报错。然而，JavaScript的Array却不会有任何错误。在编写代码时，不建议直接修改Array的大小，访问索引时要确保索引不会越界。
    
   + indexOf  与String类似，Array也可以通过indexOf()来搜索一个指定的元素的位置
   + slice slice()就是对应String的substring()版本，它截取Array的部分元素，然后返回一个新的Array;
   + push和pop
   push()向Array的末尾添加若干元素，pop()则把Array的最后一个元素删除掉
   + unshift和shift   如果要往Array的头部添加若干元素，使用unshift()方法，shift()方法则把Array的第一个元素删掉
   + sort  sort()可以对当前Array进行排序，它会直接修改当前Array的元素位置，直接调用时，按照默认顺序排序
   + reverse  reverse()把整个Array的元素给掉个个，也就是反转
   + splice splice()方法是修改Array的“万能方法”，它可以从指定的索引开始删除若干元素，然后再从该位置添加若干元素.
   ```javascript
var arr = ['Microsoft', 'Apple', 'Yahoo', 'AOL', 'Excite', 'Oracle'];
// 从索引2开始删除3个元素,然后再添加两个元素:
arr.splice(2, 3, 'Google', 'Facebook'); // 返回删除的元素 ['Yahoo', 'AOL', 'Excite']
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
// 只删除,不添加:
arr.splice(2, 2); // ['Google', 'Facebook']
arr; // ['Microsoft', 'Apple', 'Oracle']
// 只添加,不删除:
arr.splice(2, 0, 'Google', 'Facebook'); // 返回[],因为没有删除任何元素
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']

```
   + concat concat()方法把当前的Array和另一个Array连接起来，并返回一个新的Array
   ```javascript
var arr = ['A', 'B', 'C'];
var added = arr.concat([1, 2, 3]);
added; // ['A', 'B', 'C', 1, 2, 3]
arr; // ['A', 'B', 'C']
```

>请注意，concat()方法并没有修改当前Array，而是返回了一个新的Array。
>实际上，concat()方法可以接收任意个元素和Array，并且自动把Array拆开，然后全部添加到新的Array里：
 ```javascript
var arr = ['A', 'B', 'C'];
arr.concat(1, 2, [3, 4]); // ['A', 'B', 'C', 1, 2, 3, 4]
```
+ join join()方法是一个非常实用的方法，它把当前Array的每个元素都用指定的字符串连接起来，然后返回连接后的字符串;
```javascript
var arr = ['A', 'B', 'C', 1, 2, 3];
arr.join('-'); // 'A-B-C-1-2-3'
```
>如果Array的元素不是字符串，将自动转换为字符串后再连接

+ 多维数组 如果数组的某个元素又是一个Array，则可以形成多维数组

```javascript
var cars=new Array();
cars[0]="Audi";
cars[1]="BMW";
cars[2]="Volvo";

var cars=new Array("Audi","BMW","Volvo");//(condensed array)

var cars=["Audi","BMW","Volvo"];//(literal array)
```
#### 5.对象
对象由花括号分隔。在括号内部，对象的属性以名称和值对的形式 (name : value) 来定义。属性由逗号分隔：
```javascript

//person 对象有三个属性
var person={firstname:"Bill", lastname:"Gates", id:5566};
```
#### 6.Null

#### 7.Undefined

>JavaScript 拥有动态类型。这意味着相同的变量可用作不同的类型：
```javascript
var x                // x 为 undefined
var x = 6;           // x 为数字
var x = "Bill";      // x 为字符串
```

### 对象

JavaScript的对象是一种无序的集合数据类型，它由若干键值对组成。

JavaScript的对象用于描述现实世界中的某个对象

JavaScript用一个`{...}`表示一个对象，键值对以xxx: xxx形式申明，用
![ , ]()隔开。注意，最后一个键值对不需要在末尾加`,`，如果加了，有的浏览器（如低版本的IE）将报错。
访问属性是通过`.`操作符完成的，但这要求属性名必须是一个有效的变量名。如果*属性名包含特殊字符* ，就必须用`''`括起来：
```javascript
var tongxie = {
    name: '习近平',
    birth: 1969,
    school: 'No.1 Middle School',
    height: 1.73.5,
    weight: 65,
    score: null
};
tongxie.name;
tongxie.birth;

```
如下：
tongxie的属性名`middle-school`不是一个有效的变量，就需要用`''`括起来。访问这个属性也无法使用`.`操作符，必须用['xxx']来访问：

```javascript
var tongxie = {
    name: '周杰伦',
    'middle-school': 'No.11 Middle School'
};
tongxie['middle-school']; // 'No.11 Middle School'
tongxie['name']; // '周杰伦'
tongxie.name; // '周杰伦'
```
[学习贵在坚持](https://github.com/cuishengxi)
也可以用tongxie['name']来访问xiaohong的name属性，不过tongxie.name的写法更简洁。我们在编写JavaScript代码的时候，属性名尽量使用标准的变量名，这样就可以直接通过object.prop的形式访问一个属性了。
实际上JavaScript对象的所有属性都是字符串，不过属性对应的值可以是任意数据类型。
如果访问一个不存在的属性会返回什么呢？JavaScript规定，`访问不存在的属性不报错，而是返回undefined`：
>由于JavaScript的对象是动态类型，你可以自由地给一个对象添加或删除属性

+ in  是否拥有某一属性
+ hasOwnProperty() 要判断一个属性是否是对象自身拥有的，而不是继承得到的

```javascript
var tongxie = {
    name: '杨超越',
    birth: 1990,
    school: '101 女团',
    height: 1.70,
    weight: 57,
    score: null
};
'name' in tongxie; // true
'grade' in tongxie; // false
'toString' in tongxie; // true  因为toString定义在object对象中，而所有对象最终都会在原型链上指向object，所以tongxie也拥有toString属性
```

```javascript
var skryiren = {
    name: '吴亦凡',
    tag:'Itunes Music刷榜艺人'
};
skryiren.hasOwnProperty('name'); // true
skryiren.hasOwnProperty('toString'); // false
```
Persistence is the key to learning.

[学习贵在坚持](https://github.com/cuishengxi)

If you don't want to waste your life, you should spend it learning.

[如果不想虚度一生，那就要学习一辈子](https://github.com/cuishengxi)
