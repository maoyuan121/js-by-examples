## When your return statement misbehaves

######Q: 输出什么?


```js
	
	function retrunMisbehaves() {
    	return					// 1
    	{						// 2
        	key: 1
    	};
	}
	console.log(typeof retrunMisbehaves());	// 3
```
######A: 

```
	undefined
```

######解释

1. 初一看以为 `console.log`会返回一个object。在这我们要理解自动插入分号的概念。
2. 当我们在一行忘记写分号的时候JS引擎会自动给我们插入分号。上面的代码等于下面的代码，这样输出undefined就不难理解了:
	
	```js
		
		function retrunMisbehaves() {
    		return;					// 1
    		{						// 2
        		key: 1
	    	};
		}
		console.log(typeof retrunMisbehaves());	// 3
	```
3. Note the difference in line of code at #`1`, the function has returned here itself. So, we know that the standalone `return` statment is equivalent to `return undefined` and hence the output.

######Suggested Practice

1. Automatic semicolon insertion (ASI) is not bad per say but relying on the JS engine is. If you follow the practice of leaving out semicolon explicitly and leave the insertion to the JS engine, you better be aware of the all the rules of ASI (and not just the corner case, like this one). So most of the members of the JS community prefer to add semicolons explicitly, through out in their code consistently. 
2. If you are placing the semicolons explicitly, it is still important to understand the ASI rules (at least the corner cases) as we can avoid unintentional side effects, such as the one shown in above example.

######Links
1. [Stackoverflow question on ASI](http://stackoverflow.com/questions/2846283/what-are-the-rules-for-javascripts-automatic-semicolon-insertion-asi)
2. [Cowboy advice on semicolons usage](http://benalman.com/news/2013/01/advice-javascript-semicolon-haters/)

