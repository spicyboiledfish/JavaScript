# Regular Expression

## 创建方法

``` javascript
// 1. 使用字面量: /patter/attributes 
// 这里最前面的/和最后面的/表示用来隔开的。
// \b是单词边界符
// g是修饰符，表示global，全局匹配。如果不加g，只会匹配到第一个is就停止了。

var reg = /\bis\b/g;
'he is a girl, isis he is?'.replace(reg, 'IS');
// 或者可以直接使用正则
'he is a girl, isis he is?'.replace(/\bis\b/g, 'IS');


// 2. 使用构造函数: new RegExp(pattern, attributes);
// 因为'\'在js中是特殊字符，所以要转义
var reg = new RegExp('\\bis\\b', 'g');
'he is a girl, isis he is?'.replace(reg, 'IS');

// 结果：he IS a girl, isis he IS?
```

## 修饰符

``` javascript
1. g: global, 全局比配，如果不加的话，只会匹配到第一个is就停止了。
2. i: ignore case, 忽略大小写
3. m: multiple lines, 多行搜索

// 如：
var mstr = "@123
@456  
@789 ";
mstr.replace(/^@./gm, 'A');
结果： 'A23A56A89'
// 备注：这里的测试可能在控制台通不过，要在js代码里测试才可以。
```

## 两种基本字符类型

1. 元义文本字符: a、b、123等等表示字面意思的字符。
2. 元字符: 有特殊含义的非字母字符。如：* + ? $等等

### 字符类 

``` javascript
1. 使用元字符[]来构建一个简单的类
2. 表达式[abc]把字符a或者字符b或字符c归为一类。one of abc有一个就可以匹配
如：
'a2b3c4d5e6'.replace(/[abc]/g, 'x');
结果：'x2x3x4x5x6'
```

### 字符类取反

``` javascript
1. 使用元字符^创建反向类/负向类
2. 反向类的意思是不属于某类的内容
3. 表达式[^abc]表示不是a或b或c的内容
如：
'a2b3c4d5e6'.replace(/[^abc]/g, 'x');
结果：'axbxcxxxxx'
```
### 范围类

``` javascript
1. 在[]组成的类内部是可以连写的。
2. 如果要匹配-怎么办

'abc222d23fr4s23sf'.replace(/[a-z]/g, 'A');
结果: "AAA222A23AA4A23AA"

'abc233ABC'.replace(/[a-zA-Z]/g, 'Z');
结果：'ZZZ233ZZZ'

'2016-11-11'.replace(/[0-9]/g, 'Z');
结果：'ZZZZ-ZZ-ZZ'

'2016-11-11'.replace(/[0-9-]/g, 'Z');
结果：'ZZZZZZZZZZ'

```

### 预定义类

``` javascript
1. .等价于[^\r\n]  (任意字符，除了回车换行)
2. \d等价于[0-9] 
3. \D等价于[^0-9]
4. \s等价于[\t\n\x0B\f\r] 空白符
5. \S等价于[^\t\n\x0B\f\r] 非空白符
6. \w等价于[a-zA-Z_0-9] 单词字符（字母、数字、下划线）
7. \W等价于[^a-zA-Z_0-9] 非单词字符
```

### 边界字符

``` javascript
1. ^ 以xxx开头(不在[]里)
2. $ 以xxx结尾(不再[]里)
3. \b单词边界
4. \B非单词边界

// 如: ^
'@123@456@789'.replace(/^@./g, 'A');
结果：A23@456@789
// 如：$
'@123@456@789@'.replace(/.@$/g, 'A');
结果：@123@456@78A
```

