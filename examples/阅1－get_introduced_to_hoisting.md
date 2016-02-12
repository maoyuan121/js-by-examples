## Get introduced to hoisting 

######Q: What is the output?


```js
	
	function func() {
    	return varOrFunc;		// 1
    	varOrFunc = 1;			// 2
    	
    	function varOrFunc() {	// 3
    		console.log("Inside varOrFunc")
    	}
    	var varOrFunc = '2';	// 4
	}
	console.log(typeof func());
	
```
######A: 

```
	function
```

######Explanation

1. 似乎会在#`1`这个语句立刻return, 忽略下面的代码。但事实却不是这样的。
2. 要理解这个输出结果，需要先理解*hoisting*这个概念 (hoisting包括变量和function两种)。函数声明和变量声明会被提升到作用域的最上面。在这个例子中，作用域是 `func` 级别的。通过下面的代码来演示hoisting的行为。

	```js
		
		function func() {
			// hoisted
			function varOrFunc() {	// 3
    			console.log("Inside varOrFunc")
    		}
    		var varOrFunc;			// 2.1
    		return varOrFunc;		// 1
	    	varOrFunc = 1;			// 2.2
	    	varOrFunc = '2';		// 4
		}
		console.log(typeof func());
	
	```
3. 上面的代码要注意的是，变量名 `varOrFunc` 同时被用于了 `function` 和 `var` 声明 - 在这种情况下，function的声明会覆盖变量声明（fucntion的声明比变量声明的优先级高），因此 #`2.1` 不生效。`console.log`输出的是function。
4. 注意了只有变量声明和函数声明会被hoist。函数表达式不会被hoisted。

######Links
1. [JS Scoping and Hoisting](http://www.adequatelygood.com/JavaScript-Scoping-and-Hoisting.html)
