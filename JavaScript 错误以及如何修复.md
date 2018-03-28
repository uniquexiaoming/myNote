<h3>JavaScript 错误以及如何修复</h3>

<h4>Uncaught TypeError: undefined is not a function</h4>
<p>相关错误：number is not a function, object is not a function, string is not a function, Unhandled Error: ‘foo’ is not a function, Function Expected</p>
<pre>
	当尝试调用一个像方法的值时，这个值并不是一个方法。比如：
	var foo = undefined;
	foo();
	如果你尝试调用一个对象的方法时，你输错了名字，这个典型的错误很容易发生。
	var x = document.getElementByID('foo');
	由于对象的属性不存在，默认是 undefined ，以上代码将导致这个错误。
	尝试调用一个像方法的数字，“number is not a function” 错误出现。
</pre>
<p>如何修复错误：确保方法名正确。这个错误的行号将指出正确的位置。</p>

<h4>Uncaught ReferenceError: Invalid left-hand side in assignment</h4>
<p>相关错误：Uncaught exception: ReferenceError: Cannot assign to ‘functionCall()’, Uncaught exception: ReferenceError: Cannot assign to ‘this’</p>
<pre>
	尝试给不能赋值的东西赋值，引起这个错误。
	这个错误最常见的例子出现在 if 语句使用：
	if(doSomething() = 'somevalue')
	此例中，程序员意外地使用了单个等号，而不是双等号。
  “left-hand side in assignment” 提及了等号左手边的部分，因此你可以看到以上例子，左手边包含不能赋值的东西，导致这个错误。
</pre>
<p>如何修复错误：确保没有给函数结果赋值，或者给 this 关键字赋值。</p>

<h4>Uncaught TypeError: Converting circular structure to JSON</h4>
<p>相关错误：Uncaught exception: TypeError: JSON.stringify: Not an acyclic Object, TypeError: cyclic object value, Circular reference in value argument not supported</p>
<pre>
	把循环引用的对象，传给 JSON.stringify 总会引起错误。
	var a = { };
	var b = { a: a };
	a.b = b;
	JSON.stringify(a);
	由于以上的 a 和 b 循环引用彼此，结果对象无法转换成 JSON。
</pre>
<p>如何修复错误：移除任何想转换成 JSON 的对象中的循环引用。</p>

<h4>Unexpected token ;</h4>
<p>相关错误：Expected ), missing ) after argument list</p>
<pre>
	JavaScript 解释器预期的东西没有被包含。不匹配的圆括号或方括号通常引起这个错误。
	错误信息可能有所不同 - “Unexpected token ]” 或者 “Expected {” 等。
</pre>
<p>如何修复错误：有时错误出现的行号并不准确，因此很难修复。
01.[ ] { } ( ) 这几个符号不配对常常导致出错。检查所有的圆括号和方括号是否配对。行号指出的不仅是问题字符。
02.Unexpected / 跟正则表达式有关。此时行号通常是正确的。
03.Unexpected ; 对象或者数组字面量里面有个 ; 通常引起这个错误，或者函数调用的参数列表里有个分号。此时的行号通常也是正确的。</p>

<h4>Uncaught SyntaxError: Unexpected token ILLEGAL</h4>
<p>相关错误：Unterminated String Literal, Invalid Line Terminator</p>
<pre>
	一个字符串字面量少了结尾的引号。
</pre>
<p>如何修复错误：确保所有的字符串都有结束的引号。</p>

<h4>Uncaught TypeError: Cannot read property ‘foo’ of null, Uncaught TypeError: Cannot read property ‘foo’ of undefined</h4>
<p>相关错误：TypeError: someVal is null, Unable to get property ‘foo’ of undefined or null reference</p>
<pre>
	尝试读取 null 或者 undefined ，把它当成了对象。例如：
	var someVal = null;
	console.log(someVal.foo);
</pre>
<p>如何修复错误：通常由于拼写错误导致。检查错误指出的行号附近使用的变量名是否正确。</p>

<h4>Uncaught TypeError: Cannot set property ‘foo’ of null, Uncaught TypeError: Cannot set property ‘foo’ of undefined</h4>
<p>相关错误：TypeError: someVal is undefined, Unable to set property ‘foo’ of undefined or null reference</p>
<pre>
	尝试写入 null 或者 undefined ，把它当成了一个对象。例如：
	var someVal = null;
	someVal.foo = 1;
</pre>
<p>如何修复错误：也是由于拼写错误所致。检查错误指出的行号附近的变量名。</p>

<h4>Uncaught RangeError: Maximum call stack size exceeded</h4>
<p>相关错误：Related errors: Uncaught exception: RangeError: Maximum recursion depth exceeded, too much recursion, Stack overflow</p>
<pre>通常由程序逻辑 bug 引起，导致函数的无限递归调用。</pre>
<p>如何修复错误：检查递归函数中可能导致无限循环 的 bug 。</p>

<h4>Uncaught URIError: URI malformed</h4>
<p>相关错误：URIError: malformed URI sequence</p>
<pre>无效的 decodeURIComponent 调用所致。</pre>
<p>如何修复错误：按照错误指出的行号，检查 decodeURIComponent 调用，它是正确的。</p>

<h4>XMLHttpRequest cannot load http://some/url/. No ‘Access-Control-Allow-Origin’ header is present on the requested resource</h4>
<p>相关错误：Cross-Origin Request Blocked: The Same Origin Policy disallows reading the remote resource at</p>
<pre>
	http://some/url/
	错误肯定是使用 XMLHttpRequest 引起的。
</pre>
<p>如何修复：确保请求的 URL 是正确的，它遵循同源策略 。最好的方法是从代码中找到错误信息指出的 URL 。</p>

<h4>InvalidStateError: An attempt was made to use an object that is not, or is no longer, usable</h4>
<p>相关错误：InvalidStateError, DOMException code 11</p>
<pre>
	代码调用的方法在当前状态无法调用。通常由 XMLHttpRequest 引起，在方法准备完毕之前调用它会引起错误。
	var xhr = new XMLHttpRequest();
	xhr.setRequestHeader('Some-Header', 'val');
	这时就会出错，因为 setRequestHeader 方法只能在 xhr.open 方法之后调用。
</pre>
<p>如何修复：查看错误指出的行号，确保代码运行的时机正确，或者在它（例如 xhr.open）之前添加了不必要的调用</p>
