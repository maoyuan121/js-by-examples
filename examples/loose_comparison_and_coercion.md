## Loose comparison and coercion

######Q: What is the output?

```js
	
	(function () {
		falseString = "false";		// 1
		if(true) {				
			var falseString;		// 2
			if(falseString) {		// 3
				console.log(falseString == true);	// 4
				console.log(falseString == false);  // 5
			}
		}
	})();
	￼	￼	
```

######A: 

```	js

	false
	false

```

######Explanation

1. 上面这段程序涉及到4个概念。hoisting, 作用域，bool表达式的特性强制转换和宽松比较的类型强制转换。 #`2`处的变量声明被提升到了function的最上面，因此在 #`3` 处时`falseString`变量的值不是`undefined`而是`false`字符串。
2. 同时js的作用域时function级别的，而不是块级的。  #`3` 是一个bool表达式，这里会存在一个类型转换，非空的字符串会被转换成`true`。
3. 关键的时两个 `console.log`发生的类型转换, 这里的转换是使用`==`发生的宽松比较。当js对1个bool和一个string执行宽松比较的时候，js会把它们转换成数组然后再进行比较。可以重写一下上面的两个console.log，效果一样：

	```js
		
		console.log(Number(falseStr) == Number(true));  //console.log(NaN == 1);
		console.log(Number(falseStr) == Number(false)); //console.log(NaN == 0);
		
	```
4. 这样酒能理解为什么两个输出都是`false`了。

#####Link

1.	[Scoping and hoisting](http://www.adequatelygood.com/JavaScript-Scoping-and- Hoisting.html)
2.	[MDN on Functions](https://developer.mozilla.org/en- US/docs/Web/JavaScript/Reference/Functions)
3.	[ES5 Spec on Boolean expression in if condition](http://www.ecma-international.org/ecma-262/5.1/#sec-12.5)
4.	[ES5 spec on loose comparisons](http://www.ecma-international.org/ecma- 262/5.1/#sec-11.9.3)
