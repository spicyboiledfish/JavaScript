> 本文转自http://www.cnblogs.com/Wayou/p/es6_new_features.html

## 箭头操作符

箭头左边的是输入的参数

箭头右边的是进行的操作以及返回的值

``` 
var array = [1, 2, 3];
array.forEach(v=>console.log(v));
```		

## 类的支持 

只能说更向真正的面向对象语言了

``` 
// 类的定义
class Animal {
	// ES6中新型构造器 
	constructor(name) {
		this.name = name;
	}
	// 实例方法
	sayName() {
		console.log("My name is " + this.name);
	}
}

// 类的继承
class Programmer extends Animal {
	constructor(name) {
		super(name);
	}	
	program() {
		console.log("I am coding...");
	}
}

// 测试类
var animal = new Animal("yzf");
var coder = new Programmer("hwy");
animal.sayName();
coder.sayName();
coder.program();

```

## 增强的字面量对象

具体表现在：

1. 可以在对象字面量里面定义原型

2. 定义方法不用function关键字

3. 直接调用父类方法

``` 
// 通过字面量创建对象
var human = {
	breath() {
		console.log("breath...");
	}
};

var worker = {
	__proto__: human, // 设置此对象的原型是human，相当于是继承
	company: 'baidu',
	work() {
		console.log("work...");
	}
};

human.breath();
worker.breath();
```

## 字符串模板

ES6中允许使用反引号<code>`</code>来创建字符串，这种方法创建的字符串里面可以包含由美元符号加花括号包裹的变量${varible}.

```
// 产生一个随机数
var num = Math.random();
// 将这个数输出到console里
console.log(`your num is: + ${num}`);
```

## 解构

自动解析数组或者对象里的值。比如一个函数要返回多个值，常规的方法是返回一个对象,将每个值做为这个对象的属性返回。但在ES6中可以返回一个数组，然后数组中的值会自动被解析到对应接受值的变量中。

```
function getVal() {
	return [1, 2];
}
var [x, y] = getVal();
var [name, ,age] = ['11', '22', '33'];
console.log("x:" + x + ".y:" + y); // x:1,y:2
console.log("name:" + name + ".age:" + age); // name:11.age:33
```
## 参数默认值，不定参数，拓展参数

### 参数默认值

``` 
// 以前
function sayHello(name) {
	name = name || "yzf";
	console.log("hello:" + name);
}
// ES6
function sayHello2(name='yzf') {
	console.log(`hello:${name}`);
}
sayHello(); // yzf
sayHello("hwy"); // hwy 
sayHello2(); // yzf
sayHello2("hwy"); // hwy

```

### 不定参数

```
// ES5可以使用arguments
...

// 将所有参数相加
function add(...x) {
	return x.reduce((m, n)=>m + n);
}

// 传递任意个数的参数
console.log(add(1, 2, 3)); // 输出6
console.log(add(1, 2, 3, 4, 5, 6)); // 输出21
```

### 拓展参数

拓展参数则是另一种形式的语法糖，它允许传递数组或类数组直接作为函数的参数而不是用apply

```
var people = ['yzf', 'hwy', 'yyh'];

// sayHello函数本来接受3个单独的参数
function sayHello(people1, people2, people3) {
	console.log(`Hello ${people1}, ${people2}, ${people3}`);
}

// 但是我们将一个数组以拓展参数的形式传递，它能很好的映射到每个单独的参数
sayHello(...people); // Hello 'yzf', 'hwy', 'yyh'
sayHello.apply(null, people); // Hello 'yzf', 'hwy', 'yyh'
```

## let与const关键字

let具有块作用域，const用来定义常量，即无法被更改的值

```
for(let i = 0;i < 5;i++) {
	console.log(i); 
}
console.log(i); // 输出"undefined", 严格模式下会报错
```

## for of值遍历

```
```