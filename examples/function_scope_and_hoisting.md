## Function scope and hoisting

######Q: 会输出什么?

```js

	var name = "John";

	(function(){
	  	console.log("The name is : " + name);

	  	var name = "Jane";

	  	console.log("The name is : " +name);
	})();

```

######A:

```
		undefined
		Jane

```

######解释:

1. **Hoisting :** js引擎会在一个作用域里面查找这个作用域内声明的变量，并把这个变量的声明（注意仅仅是声明，不是赋值）提升到这个作用域的最上面。

	因此第一个console.log("The name is : " + name)语句是读的本地的非全局的name变量; 上面的代码，等于我们下面显性hoisting之后的代码
	```js

	var name = "John";

	(function(){
		var name;  // 注意这里的变化  只是声明  不是赋值
	  	console.log("The name is : " + name);

	  	name = "Jane";  // 注意这里

	  	console.log("The name is : " +name);
	})();

	```
	这样我们理解起来就不困难了。


2. **Function Scope :**  Every variable in JS is scoped at a function level, means variables which are declared inside a function is not accessible outside the function in which it is declared.

3. **Scope chaining :** When a variable is not found in a function scope, the execution environment traverses to an outer scope to find the same. Otherwise, the variable which is found in the current scope is used.

	So in the above code, the statement var name = "Jane" declares a variable "name" which is local to the function scope. So the outer variable which has the same variable name is ignored, and the variable in current scope is used. Hence the second statement **console.log("The name is : " + name);** logs a value **Jane**.
	
######Links:

1. [JavaScript variable scope and hoisting](http://javascriptissexy.com/javascript-variable-scope-and-hoisting-explained/)
