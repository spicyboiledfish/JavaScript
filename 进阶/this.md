# this

高程上有这么两句话：

一句是(p114)：

> 函数内部的另一个特殊对象是this, 其行为和Java与C#中的this大致相似。换句话说，this引用的是函数据以执行的环境对象---或者也可以说是this值(当在网页的全局作用域中调用函数时，this对象引用的就是window)。

这里说，this引用的是函数执行环境的对象。

还有一句话是(P182)：

> 我们知道，this对象是运行时基于函数的执行环境绑定的： 在全局函数中，this等于window, 而当函数被作为某个对象的方法调用时，this等于那个对象。不过，匿名函数的执行环境具有全局性，因此其this对象通常指向window。但是有时候由于编写闭包的方式不同，这一点有可能不太明显。看例子

```
var name = 'window';

var obj = {
	name: 'my',
	
	getNameFunc: function() {
		return function() {
			return this.name;
		};
	}
};
console.log(obj.getNameFunc()()); // 非严格模式下，"window"

/*
 * 等价于
 *
 * var f = function() {
 *     return this.name;
 * }
 * 
 * obj.getNameFunc() = f;
 * f() = window.f() 所以，值为window 
 *
 */
```

由于obj.getNameFunc()返回一个函数(这个函数是window的)，那么obj.getNameFunc()()就会立即执行它所返回的那个函数。

 
