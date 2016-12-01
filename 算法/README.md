### 列表

1. 判断一个单词是否回文

2. 数组去重，返回剩下的

3. 数组去重，返回去掉的

4. 统计一个字符串中出现最多的字母

5. 不借助任何变量交换两个变量

6. 随机生成指定长度的字符串 



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
