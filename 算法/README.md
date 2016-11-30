> 判断一个单词是否回文

``` javascript
function checkPalindrom(str) {
	return str == str.split("").reverse().join("");
}
```

> 去掉一组整形数组重复的值, 返回剩下的。

``` javascript
// 比如输入[1, 13, 24, 11, 11, 14, 1, 2]
// 输出[1, 13, 24, 11, 14, 2]

var unique = function(arr) {
	var hashTable = {};	
	var data = [];
	for(var i = 0, len = arr.length;i < len;i++) {
		if(!hashTable[arr[i]]) {
			hashTable[arr[i]] = true;
			data.push(arr[i]);
		}
	}
	return data;
};
```

> 请给Array本地对象增加一个原型方法，它用于删除数组条目中重复的条目(可能有多个)，返回值是一个包含被删除的重复条目的新数组。

``` javascript
Array.prototype.distinct = function() {
	var data = [];
	for(var i = 0;i < this.length;i++) {
		for(var j = i + 1;j < this.length;) {
			if(this[i] === this[j]) {
				data.push(this.splice(j, 1)[0]);
			} else {
				j++;
			}
		}
	}	
	return data;
};
// test
console.log([1, 2, 3, 4, 4, 4, 3, 3].distinct()); // 4, 4, 3, 3
```


> 统计一个字符串中出现最多的字母

``` javascript
// 比如输入：aaacccssszzzzzaaaaaijjjl0o
// 输出：a

function findMax(str) {
	if(str.length == 1) {
		return;
	}
	var charObj = {};
	for(var i = 0;i < str.length;i++) {
		if(!charObj[str.charAt(i)]) {
			charObj[str.charAt(i)] = 1;
		} else {
			charObj[str.charAt(i)] += 1;
		}
	}
	var maxChar = '';
	var maxValue = 1;
	
	for(var k in charObj) {
		if(charObj[k] >= maxValue) {
			maxChar = k;	
			maxValue = charObj[k];
		}	
	}
	return maxChar;
}
```

> 冒泡排序

``` javascript
// 输入：[5, 6, 3, 4, 8, 0, 1, 4, 7]
// 输出：[0, 1, 3, 4, 4, 5, 6, 7, 8]
外层1：
	内层1：3 6 5 8 0 1 4 7
	内层2：0 6 5 8 3 1 4 7
外层2：
	内层1：0 5 6 8 3 1 4 7 
	内层2：0 3 6 8 5 1 4 7 
	内层3：0 1 6 8 5 3 4 7 
// 每一次外层循环是为了找到当前最小的值

function bubbleSort(arr) {
	for(var i = 0, l = arr.length;i < l - 1;i++) {
		for(var j = i + 1;j < l;j++) {
			if(arr[i] > arr[j]) {
				var temp = arr[i];
				arr[i] = arr[j];
				arr[j] = temp;
			}
		}
	}	
	return arr;
}
```

> 快速排序

``` javascript
// 1. 在数组中，选一个元素作为基准
// 2. 所有小于基准的元素，都移到基准的左边；所有大于基准的元素，都移到基准的右边。 
// 3. 对基准左边和右边的两个子集，不断重复第一步和第二步，直到所有子集只剩下一个元素为止。
function quickSort(arr) {
	if(arr.length <= 1) {
		return arr;
	}	
	var pivotIndex = Math.floor(arr.length / 2); 
	var pivot = arr[pivotIndex];
	// 找到基准元素，并将其从数组中分离出来
	var pivot = arr.splice(pivotIndex, 1)[0];	
	var leftArr = [];
	var rightArr = [];
	for(var i = 0;i < arr.length;i++) {
		if(arr[i] > pivot) {
			rightArr.push(arr[i]);
		} else {
			leftArr.push(arr[i]);
		}	
	}
	return quickSort(leftArr).concat([pivot], quickSort(rightArr));
}	
```



> 希尔排序

> 插入排序

> 不借助任何临时变量，交换两个整数

``` javascript
// 输入：a = 2;b = 4;
// 输出: a = 4;b = 2;
function swap(a, b) {
	b = b - a;
	a = a + b;
	b = a - b;
}
```

> 随机生成指定长度的字符串

``` javascript
function randomString(n) {
	var str = "abcdefghigklmnopqrstuvwxyz9876543210";	
	var temp = '';
	var i = 0;
	var l = str.length;
	for(i = 0;i < n;i++) {
		temp += str.charAt(Math.floor(Math.random() * l));
	}
	return temp;
}
```
