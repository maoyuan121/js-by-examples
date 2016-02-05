## About delete

######Q: 会输出什么?

```js

	var myVar = 1;
	var output = (function(){
		delete myVar;
		return myVar;
	})();
	
	console.log(output);		// 1
	
	function MyFunc(){}
	MyFunc.prototype.bar = 42;
	var myFunc = new MyFunc();

	delete myFunc.bar;	
	console.log(myFunc.bar);	// 2

	delete MyFunc.prototype.bar;
	console.log(myFunc.bar);	// 3
	￼	
```

######A: 

```		
	1
	42
	undefined

```

######解释

1. `delete` 操作符被用于删除一个对象的属性。因为 `myVar` 是一个变量不是一个对象, 因此 #`1` 没有生效。
2. 那为什么 #`2` 也没有生效呢？仔细看看 `myFunc.bar`，它是一个被继承的属性。因此 #`2` 也没有生效。
3. #`3` 输出 `undefined` 因为我们直接通过`MyFunc.prototype` 删除了属性。因此所有过`MyFunc`的实例都没有`bar`这个属性了。

######Link

1.	[MDN on delete](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete)
