> 判断一个单词是否回文

``` javascript
function checkPalindrom(str) {
	return str == str.split("").reverse().join("");
}
```

> 去掉一组整形数组重复的值

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
		if()
	}
}
```