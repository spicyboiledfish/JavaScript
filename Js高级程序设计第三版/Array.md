### 关于数组的常用API

> 检测数组

```
// 1. if(value instanceof Array) {}, 并不推荐,存在跨页面问题
// 2. Array.isArray(value) // IE9+、Firefox4+、Safiri5+、Opera10.5+、Chrome
// 3. if(Array.prototype.toString.call(arr) === '[object Array]')
```

> 转换方法

```
1. toString()
2. valueOf() 调用这个返回的还是数组
	alert(colors.valueOf()); // 由于alert要接受字符串参数，所有数组会在后台调用toString()方法
3. toLocaleString(); 如果数组调用这个方法，调用的是数组每一项的toLocalString()方法, 和其他方法一样，会创建一个字符串，数组项以逗号分隔
4. join(",") 数组项会以传入的参数分隔
```

> 栈方法

```
1. push(); // 向数组添加元素, 传入参数可以是多个，返回值是数值，传入几个就返回几。
2. pop(); // 取得数组最后一项, 返回被移除的项
```

> 队列方法

```
1. shift() // shift的意思是改变、去掉, 取得第一项，返回被取得的项
2. unshif() // 从数组前端插入项，返回项的个数
```

> 重排序方法

```
1. reverse() // 翻转数组的顺序
2. sort() // 升序排序，sort()会调用每个数组项的toString()转型方法
		  // 然后比较得到的字符串。即使传入的是数值，比较的仍旧是字符串
		  // 因此sort()方法接受一个比较函数,比较函数接受两个参数 
		  // 如果第一个参数在第二个参数前返回一个负数。

// 这个比较函数可以适用于大部分的数据类型
function compare(value1, value2) {
	if(value1 < value2) {
		return -1;
	} else if(value1 > value2) {
		return 1;
	} else {
		return 0;
	}
} 

```