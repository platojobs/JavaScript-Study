# JavaScript-Study
JavaScript-Study

#### JavaScript 简介
 JavaScript 是世界上最流行的编程语言。
这门语言可用于 HTML 和 web，更可广泛用于服务器、PC、笔记本电脑、平板电脑和智能手机等设备。

JavaScript 是脚本语言
JavaScript 是一种轻量级的编程语言。
JavaScript 是可插入 HTML 页面的编程代码。
JavaScript 插入 HTML 页面后，可由所有的现代浏览器执行。

HTML 中的脚本必须位于 `<script>` 与 `</script> `标签之间。
脚本可被放置在 HTML 页面的 <body> 和 <head> 部分中。
```JavaScript
<script>
alert("My First JavaScript");
</script>
```
##### JavaScript的实现
`<script>`标签
如需在 HTML 页面中插入 JavaScript，请使用 `<script>` 标签。
`<script>` 和 `</script>` 会告诉 JavaScript 在何处开始和结束。

+ JavaScript 函数和事件
上面例子中的 JavaScript 语句，会在页面加载时执行。
通常，我们需要在某个事件发生时执行代码，比如当用户点击按钮时。
如果我们把 JavaScript 代码放入函数中，就可以在事件发生时调用该函数。
您将在稍后的章节学到更多有关 JavaScript 函数和事件的知识。
+ `<head>` 或` <body>` 中的 JavaScript
您可以在 HTML 文档中放入不限数量的脚本。
脚本可位于 HTML 的 `<body>` 或 `<head>` 部分中，或者同时存在于两个部分中。
通常的做法是把函数放入 `<head>` 部分中，或者放在页面底部。这样就可以把它们安置到同一处位置，不会干扰页面的内容。
+ `<head>` 中的 JavaScript 函数
在本例中，我们把一个 JavaScript 函数放置到 HTML 页面的 `<head>` 部分。

```javascript
<!DOCTYPE html>
<html>
<body>

<h1>My Web Page</h1>

<p id="demo">A Paragraph</p>

<button type="button" onclick="myFunction()">Try it</button>

<script>
function myFunction()
{
document.getElementById("demo").innerHTML="My First JavaScript Function";
}
</script>

</body>
</html>
```
>我们把 JavaScript 放到了页面代码的底部，这样就可以确保在 `<p>` 元素创建之后再执行脚本。

+ 外部的 JavaScript
也可以把脚本保存到外部文件中。外部文件通常包含被多个网页使用的代码。
外部 JavaScript 文件的文件扩展名是 `.js`。
如需使用外部文件，请在 `<script>` 标签的 `"src"` 属性中设置该 `.js` 文件：

```javascript
<!DOCTYPE html>
<html>
<body>
<script src="myScript.js"></script>
</body>
</html>

```
在 `<head> `或 `<body>` 中引用脚本文件都是可以的。实际运行效果与您在 `<script>` 标签中编写脚本完全一致。
> <u>提示：外部脚本不能包含`<script>`标签</u>
&copy;:崔盛希


+ - [X] 操作 HTML 元素
+ - [X] 如需从 JavaScript 访问某个 HTML 元素，您可以使用 `document.getElementById(id)` 方法。请使用 `"id"` 属性来标识 HTML 元素

```javascript
<!DOCTYPE html>
<html>
<body>

<h1>大伟简介：</h1>

<p id="demo">我是大伟</p>

<script>
document.getElementById("demo").innerHTML="我是刘德华，拍过《神雕侠侣》";
</script>

</body>
</html>
```
