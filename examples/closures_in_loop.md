## Closures in loop

######Q: 会输出什么?


```js

	var data = [0, 1, 2];
	var funcs = [];
	
	function init() {						// 0
		for (var i = 0; i < 3; i++) {
    				
	    	var x = data[i];				// 1
 	    	var innerFunc = function() { 	// 2
 	    		return x;
 	    	};
 
 			funcs.push(innerFunc);			// 3
 		}
	}
	
	function run() {						// 4
		for (var i = 0; i < 3; i++) {
		    console.log(data[i] + ", " +  funcs[i]());   // 5
  		}
	}
	
	init();
	run();
	
```

######A: 

```
		0, 2
		1, 2
		2, 2

```

######解释

1. 在理解输出前我们需要先理解闭包这个概念。闭包就是函数应用了独立自主的参数变量。换而言之，闭包函数记住了它被创建时候的环境。

2. 问题在于变量x, 所有 #`2`的inner函数都绑定了function外的同一个参数。这是因为这个x的作用域在 `init` 函数。看看下面修改后的代码，它会输出你想要的结果 (`0, 0`,`1, 1`,`2, 2` ...)。修改后的代码`temp`的作用域在 `innerFunc`里。

	```js
		
		var data = [0, 1, 2];
		var funcs = [];
	
		function init() {						// 0
			for (var i = 0; i < 3; i++) {
    				
	    		var x = data[i];				// 1
 	    		var innerFunc = function() { 	// 2
 	    			var temp = x;
 	    			return function() {
 	    				return temp;
 	    			}; 
 	    		}();
 
 				funcs.push(innerFunc);			// 3
 			}
		}
	
		function run() {						// 4
			for (var i = 0; i < 3; i++) {
			    console.log(data[i] + ", " +  funcs[i]());   // 5
  			}
		}
	
		init();
		run();
	
	```
	 
3. 最起码有3种方法来解决closure in loop的问题, Dave Herman的文章中有提到 (看下面的链接)。另外, ES6 has provision for block scoping of variable through `let` keyword declaration.

4. Do not fret if you still are not clear about how the closures work, it takes sometime to come to terms with closures. So, do read on.

######Links

1. [MDN on JS Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
2. [Dave Herman on Closure in loop](http://calculist.blogspot.com/2005/12/gotcha-gotcha.html)
3. [Stackoverflow question on closures](http://stackoverflow.com/questions/111102/how-do-javascript-closures-work)
4. [Stackoverflow question on closures in loop](http://stackoverflow.com/questions/750486/javascript-closure-inside-loops-simple-practical-example/19323214#19323214)
5. [JSFiddle for closures in loop](https://jsfiddle.net/davidojedalopez/jvhw9846/)
