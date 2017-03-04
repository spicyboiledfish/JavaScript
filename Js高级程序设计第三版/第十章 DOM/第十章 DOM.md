# DOM

![](1.png)

![](2.png)

## 操作节点

* someNode.appendChild(newNode), 向someNode末尾添加节点，如果添加的节点已经存在，那么就是移动移动元素。返回值是新增的节点。

* 插入到指定位置：insertBefore(要插入的节点，作为参照的节点)

``` 
returnNode = someNode.insertBefore(newNode, oldNode);
```

* replaceChild(要插入的节点，要替换的节点)：替换节点

``` 
returnNode = someNode.replaceChild(newNode, oldNode)
```

* 移除节点: removeChild(要移除的节点)

**所有类型的节点都有的方法:**

* cloneNode(true/false):表示深复制和浅复制,  复制后节点是游离的。

```
// 注意，这里是重点
// 1. IE9之前的版本不会为空白符创建节点。
<ul>
	<li>item 1</li>
	<li>item 2</li>
	<li>item 3</li>
</ul>
var deepList = myList.cloneNode(true);
console.log(deepList.childNodes.length); // 3(IE<9)或7(其他浏览器)

// 2. cloneNode()方法只复制特性，其他一切不复制。
// 但是IE存在一个BUG, 即它会复制事件处理程序。所以复制前要先移除事件处理程序
```
	
* normalize()方法处理文档树的文本节点，当某个节点调用该方法时，就会在该节点的后代节点中查找下面的情况。 如果后代的文本节点里无文本，就删除它;如果找到相邻的文本节点,就合并它们。

## Document类型

1. JavaScript通过Document类型表示文档。

2. HTMLDocument继承自Document。

3. 在浏览器中，document对象是HTMLDocument的一个实例。表示整个HTML页面。

4. 而且，document对象是window对象的一个属性，因此可以作为全局使用。

### 文档的子节点

**重点：**

```
var html =  document.documentElement;
var body = document.body;
```

说明：

```
<html>
	<head></head>
	<body></body>
</html>
```

* 对于上面的这种结构(没有doctype声明)，下面的测试都是正确的。如果有doctype声明的话，<code><!DOCTYPE html></code>也是文档的子节点。

```
// 第一个
var html = document.documentElement; // 取得对<html>的引用

// 第二个
// 不推荐这个，因为可能有注释节点，而注释节点每个浏览器对它的解析又不一样。
var html = document.childNodes[0];     ```

// 第三个, 不推荐
var html = document.firstChild;
```

* 作为HTMLDocument的实例，document对象还有一个body属性，直接指向<code>body</code>元素。

```
var body = document.body;
```

* document还有的一个属性<code>document.doctype</code>可以获取。但是不同浏览器对doctype的支持不一样。所以不推荐使用。


### 文档信息

作为HTMLDocument的一个实例，document对象还有标准的Document对象所没有的属性。这些属性提供了document对象所表现的网页的一些信息。

1. document.title

2. document.URL, 显示页面的一个完整URL地址(地址栏里的URL)。

3. document.domain, 显示页面的域名。

4. document.referrer，保存着链接到当前页面的那个页面的URL。

5. 三个属性中，只有document.domain可以设置。

	* 不能将这个属性设置为URL中不包含的域。    

	* 如果域名一开始是松散的，那么不能将它设置为紧绷的。也就是说, 开始如果是baidu.com，就不能设置为www.baidu.com

### 查找元素

* document.getElementById()，这是Document类型提供的方法。

* document.getElementsByTagName()，返回HTMLCollection对象，这是Document类型提供的方法。

```
var images = document.getElementsByTagName();

// 第一种方法访问images的元素
var img1 = images[0];

// 第二种方法访问images的元素
var img2 = images['title'];

// 第三种方法访问images的元素
var img3 = images.item(0);

// 第四种方法访问images的元素
var img4 = images.namedItem('title');
```

* document.getElementsByName(), 这是HTMLDocument类型提供的方法, 常用方法是获取单选按钮。

### 特殊集合

document对象还有一些特殊的集合，都是HTMLColletion类型的。

1. document.anchors, 包含文档中所有带name特性的<a>元素。

2. document.forms

3. document.images

4. document.links, 包含文档中所有带href属性的<a>元素。


### DOM一致性检测

// 目前不会涉及到

### 文档写入

1. document.write(), 常用与向文档中写入元素或者加载资源(script)。

2. document.writeln()

3. document.open()

4. document.close()


## Element类型

* 特征

	* nodeType的值为1

	* nodeName的值为元素的标签名

	* nodeValue的值为null
		
	* parentNode可能是Document或Element

* 访问标签名

```
var div = document.getElementById('myDiv');
console.log(div.tagName == div.nodeName); // true, "DIV"


// so ....
if(element.tagName.toLowerCase() == 'div') {

} 
```

### HTML元素

所有HTML元素都由HTMLElement类型表示，不是直接通过这个类型，也是通过它的子类型来表示。HTMLElement类型直接继承自Element并添加了一些属性。添加的这些属性分别对应于每个HTML元素都存在的下列标准特性。

* id

* title

* lang, 内容元素的语言代码，很少使用

* dir, 值为'ltr'或'rtl', 当值被重写的那一刻，立即影响页面中文本的左、右对齐方式。

* className

上面五个特性，可读可写，也就是说可以:

```
var div = document.getElementById('xx');
div.id = 'mm';
div.title = 'hh';
div.className = 'nn';
...
```


### 取得特性

每个元素都有一或多个特性，这些特性的用途是给出相应元素或其内容的附加信息。操作特性的DOM方法主要有3个，分别是getAttribute()、setAttribute()和removeAttribute()。这三个方法可以针对任何特性使用，包括那些以HTMLElement类型属性的形式定义的特性。

```
var div = document.getElementById('myDiv');
console.log(div.getAttribute('id'));
console.log(div.getAttribute('class'));
console.log(div.getAttribute('title'));
...
```

当然，getAttribute()也可以取得自定义特性(即标准HTML语言中没有的特性)的值。但是要注意两点：

* 特性的名称是不区分大小写的。

* HTML5规定，自定义特性应该加上data-前缀以便验证。

因为只有公认的(非自定义的)特性才会以属性的形式添加到DOM对象中，比如：

```
<div id="myDiv" data_mm="ll" align="center">

var div = document.getElementById('myDiv');
console.log(div.id); // 'myDiv'
console.log(div.data_mm); // undefined
console.log(div.align); // 'center'
```

所以一般，开发人员不使用getAttribute(), 而是使用对象的属性。只有在取得自定义特性值的时候，才会使用getAttribute()方法 。


### 设置特性

setAttribute() 方法既可以操作HTML特性也可以操作自定义特性。

要记住关于它的几个特点。

* 通过这个方法设置的特性名会被统一转换为小写形式。比如"ID"最终会变为"id"

* 像下面这样为DOM元素添加一个自定义的属性，该属性并不会自动生成元素的特性。

```
div.myColor = "red";
console.log(div.getAttribute('myColor')); // null
```

removeAttribute()可以彻底删除元素的特性，调用这个方法不仅会清除特性的值而且也会从元素中完全删除特性。

### attributes属性

Element类型是使用attributes属性的唯一一个DOM节点类型。attributes属性中包含一个NamedNodeMap, 与NodeList类似，也是一个动态的集合。元素的每一个特性都由一个Attr节点表示，每个节点都保存在NamedNodeMap对象中。NamedNodeMap对象拥有以下方法。

* getNamedItem(name): 返回nodeName属性等于name的节点;

* removeNamedItem(name): 从列表中移除nodeName属性等于name的节点;

* setNameItem(node): 向列表中添加节点，以节点的nodeName属性为索引;

* item(pos): 返回位于数字pos位置处的节点;


```
<div id="test" data-xx="xx" data-yy="yy">
var test = document.getElementById('test');
var xx = test.attributes.getNamedItem('data-xx').nodeValue; // 'xx'
var xx2 = test.attributes['data-xx'].nodeValue;
var yy = test.attributes.getNamedItem('data-yy').nodeValue; // 'yy'
```

这个属性还可以用来遍历元素的特性。

```
function outputAttributes(element) { 
	var pairs = new Array();
	var attrName;
	var attrValue;
	var i;
	var len;

	for(i = 0, len = element.attributes.length;i < len;i++) {
		attrName = element.attributes[i].nodeName;
		attrValue = element.attributes[i].nodeValue;
		pairs[i].push(attrName + "=\"" attrValue + "\"");
	}
}
```


### 创建元素

document.createElement()可以用来创建新元素，它只接受一个参数，即要创建元素的表签名。这个标签名在HTML文档中不区分大小写，但是在XHTML或XML文档中，要区分。

创建出来后的元素，它是游离的，但是它的ownerDocument属性却是被设置了的。

```
var xx = document.createElement('div')；
xx.className = 'a';
document.body.appendChild(xx);
```

### 元素的子节点

主要要判断节点的类型，因为浏览器的解析可能会不一样。比如说：

```
<ul id="list">
	<li>1</li>	
	<li>2</li>	
	<li>3</li>	
</ul>

var list = document.getElementById('list');
console.log(list.childNodes.length); // 7(会有空白符号，主流浏览器) 或 3(IE)

// 所以最好
if(list.childNodes[i].nodeType == 1) {
	// do-other
}
```

## Text类型

特性：

* nodeType的值为3

* nodeName的值为"#text"

* nodeValue的值为节点所包含的文本 (node.nodeValue == node.data)

* parentNode是一个元素

* 不支持(没有)子节点

* 拥有length属性

方法：

* appendData(text) 将text添加到节点的末尾

* deleteData(offset, count)

* insertData(offset, text)

* splitData(offset) 从offset指定的位置将当前文本节点分成2个文本节点

* substringData(offset, count) 提取从offset指定的位置开始到offset+count为止处的字符串。

### 创建文本节点

```
var text = document.createTextNode('haha'); // 创建文本节点
text.appendData(', 我是一个人'); // 在'haha'后面添加'我是一个人'

var div = document.createElement('div');
div.className = 'c';

div.appendChild(text);
document.body.appendChild(div);
```

### 规范化文本节点

DOM文档中存在相邻的同胞文本节点很容易导致混乱，因此分不清哪个文本节点表示哪个字符串。因此就有了一个能够将相邻文本节点合并的方法。

```
element.normalize();
```

### 分割文本节点

它的作用是和normalize()相反的。比如：

```
var textNode = document.createTextNode('Hello world');
var newNode = textNode.splitText(5); 

console.log(textNode); // "Hello"
console.log(newNode); // " world"
```

## DocumentFragment类型

在所有节点类型中，只有DocumentFragment在文档中没有对应的标记。DOM规定文档碎片(document fragment)是一种轻量级的文档，可以包含和控制节点，但是不会像完整的文档那样占用额外的资源。

虽然不能将文档片段直接田间到文档中，但是可以将它作为一个"仓库"来使用。即可以在里面保存将来可能会添加到文档中的节点。要创建文档片段，可以使用document.createDocumentFragment()。

举例来说，如果我们想为ul添加3个列表项，如果逐个添加列表项，将会导致浏览器反复渲染(呈现)新信息。所以可以这样:

```
<ul id="list"></ul>

var list = document.getElementById('list');
var fragment = document.createDocumentFragment;
var li;
var i;

for(i = 0;i < 3;i++) {
	li = document.createElement('li');
	fragment.appendChild(li);
}

list.appendChild(fragment);
```







