## Extracted method and bind

######Q: 会输出什么?

```js

	var myObject = {
    	myCountryName: 'India',
    	getMyCountryName: function (){			   // 1
        	return this.myCountryName;
    	}
	};

	var countryInfo = myObject.getMyCountryName;  // 2

	console.log(countryInfo());	                  // 3
	console.log(myObject.getMyCountryName());	  // 4
	
```

######A: 

```	
	
	undefined
	India	

```

######解释

1. #`3`的`console.log`会输出`undefined` 因为执行他的上下文是global。 在这个例子中this指向的是`windows`对象，然而又不存在全局的`myCountryName`因此输出`undefined`。
2. 因为`windows`对象没有`myCountryName`属性，所以#`3`输出`undefined`。 #`4`的输出是我们想要的结果，因为此时`this`变量指向`myObject`。
3. 显性的调用bind绑定到对象可以解决提取方法的这个问题。

	```js
		
		var countryInfo = myObject.getMyCountryName.bind(myObject);
		
	``` 
