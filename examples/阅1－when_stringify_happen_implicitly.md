## When Stringify happens implicitly

######Q: What is the output?

```js

	var root = {};
    var elementOne = {key:'1'};
    var elementTwo = {key:'2'};

	root[elementOne] = "Element One"; 
	root[elementTwo] = "Element Two";

	console.log(root[elementOne]);

```

######A: 


```		
	
	Element Two
	
```


######Explanation


1. 设置一个对象的属性的时候，js会在内部使用`toString`转化parameter/key, 因此当我们把一个对象做为key的时候，如果这些对象没有实现自己的`toString`，默认会使用`Object.toString`来转换。
2. 因此，这两个对象会转换成 "[object Object]"。所以`root[elementOne]`  和 `root[elementTwo]` 都等于 `root["[object Object]"]` 。所以`root[elementOne]` 和 `root[elementTwo]` 都引用同一个值。
3. We can verify that, if we override `toString` method in each of the `elementOne` and `elementTwo` objects, we will have a different behavior. Take a look at the following example.



	```js

		var root = {};
    	var elementOne = { 
    		key:'1',
    		toString: function() {
    			return '1';
    		}    	
    	};
    	
    	var elementTwo = {
    		key:'2',
    		toString: function() {
    			return '2';    		
    		}
    	};

		root[elementOne] = "Element One"; 
		root[elementTwo] = "Element Two";

		console.log(root[elementOne]);		// prints "Element One"

	```
