## Grouping operator

######Q: What is the output?

```js

	function myFunc(myVar) { 
		console.log(arguments);
		return myVar;
	} (1, 2, 3);
	￼	
```

######A: 

```		
	3

```

######Explanation

1. 看上去是一个IIFE，其实不是。 `myFunc` 是一个 *函数声明* 不是`函数表达式`。
2. 返回的值其实不来自于 `console.log` , `myFunc` 函数其实根本就没有被触发。上面的代码会被解析等价于下面的代码：
	```js
		
		function myFunc(myVar) { 
			console.log(arguments);
			return myVar;
		}; // 注意这个分号

		(1, 2, 3);		
	```

######Link

1.	[MDN on grouping operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Grouping)
2.	[Ben Alman on IIFE](http://benalman.com/news/2010/11/immediately-invoked-function-expression/)
