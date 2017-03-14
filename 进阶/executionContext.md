[本文来自](http://davidshariff.com/blog/what-is-the-execution-context-in-javascript/#)

# 执行环境与执行环境栈

每个执行环境都与一个变量对象相对应。

每个函数都有自己的执行环境。

当代码在一个环境中执行时，会创建变量对象的一个作用域链。


## 详解


每次调用一个函数时，一个新的执行执行环境会被创建。但是，在JavaScript解释器中，对执行上下文的每次调用都有2个阶段。

**创建阶段**

> 创建阶段也就是：当函数被调用时，但在它执行所有代码之前。 

* 创建作用域链。

* 创建变量，函数和参数。

* 确定值"this"。

**激活/代码执行阶段**

* 分配值，引用函数和解释/执行代码。

可以在概念上将每个执行环境表示为具有3个属性的对象:

```
executionContextObj = {
	'scopeChain': {/* variableObject + all parent execution context's variableObject */},
	'variableObject': {/* function arguments / parameters, inner variable and function declarations */},
	'this': {}
}
```

**这里是解释器如何评估代码的伪描述**

1. 找到一些代码来调用函数。

2. 在执行function代码之前，创建execution context。

3. 进入创建阶段。

	* 初始化Scope chain

	* 创建variable object:
		
		* 创建arguments object, 检查参数的上下文，初始化名称和值来创建引用副本。

		* 扫描函数声明的上下文:

			* 对于找到的每个函数，在变量对象中创建一个属性，它具有一个引用指针，指向内存中的函数。

			* 如果函数名已经存在，则引用指针被覆盖。

		* 扫描变量声明的上下文:

			* 对于找到的每个变量声明，在变量对象中创建一个属性，即变量名，并将值初始化为undefined。

			* 如果变量名已经存在当前变量对象中，则不执行操作并继续扫描。

	* 确定"this"上下文内部的值。

4. 激活/执行代码阶段：

	* 在上下文中运行/解释函数代码，并在代码逐行执行时分配变量值。

### 一个例子

```
function foo(i) {
	var a = 'hello';
	var b = function privateB() {

	};

	function c() {

	}
}

foo(22);
```

在调用foo(22)时，创建执行环境阶段如下：

```
fooExecutionContext = {
	scopeChain: {/* */};
	variableObject: {
		arguments: {
			0: 22,
			length: 1
		},
		i: 22,
		c: pointer to function c()
		a: undefined
		c: undefined
	},
	this: {/* */}
};
```

激活代码阶段在函数完成执行时看起来像这样：

```
foExecutionContext = {
	scopeChain: {/* */},
	variableObject: {
		arguments: {
			0: 22,
			length: 1
		}
		i: 22,
		c: pointer to funciton c()
		a: 'hello'
		b: pointer to function privateB()
	},
	this: {/* */}
};
```

### 变量提升 

```
(function() {
	
	console.log(typeof foo); // function
	console.log(typeof bar); // undefined

	var foo = 'hello';
	var bar = function() {
		return 'world';
	};

	function foo() {
		return 'hello';
	}
})();
```

* 为什么我们要在声明foo之前访问foo?
	
	* 因为我们遵循'创建阶段', 我们知道变量在代码执行前就已经创建了。所以随着函数流开始执行，foo已经定义在了活动对象中。

* foo被声明了2次，为什么是foo显示function，而不是显示undefined或string?

	* 即使foo被声明了2次，我们知道，在创建执行环境阶段，函数是在变量前创建的，并且，如果属性名称已经存在于活动对象中，我们只是绕过它。

	* 因此，引用function foo()是在活动对象里首先创建的，当解析器得到var foo 时，我们已经看到数姓名foo存在，因此代码不执行任何操作并继续。

* 为什么bar是undefind?

	* bar实际上是一个具有函数赋值的变量，我们知道这些变量是创建的，创建执行环境阶段会用undeinfed来初始化它们。
	
