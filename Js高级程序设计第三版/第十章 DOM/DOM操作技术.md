## 动态脚本

利用< script>元素可以向页面中插入JavaScript代码，一种是用src特性包含外部文件。另一种方式就是利用这个元素本身来包含代码。这里要讨论的动态脚本，指的是在页面加载时不存在，但是将来某一时刻通过修改DOM动态添加的脚本。跟操作HTML元素一样，创建动态脚本也有两种方式： 插入外部文件和直接插入JS代码。

```
// 第一种
function loadScript(url) {
	var script = document.createElement('script');
	script.type = 'text/javascript';
	script.src = url;
	document.body.appendChild(script); // 客户端是不会下载外部文件的
}

// 第二种
function loadScriptString(code) {
	var script = document.createElement('script');
	script.type = "text/javascript";
	
	try {
		script.appendChild(document.createTextNode(code));
	} catch(ex) {
		script.text = code;
	}
	document.body.appendChild(script);
}

loadScriptString("function() {console.log('haha');}");
```

## 动态样式

加载外部样式文件是异步的，也就是加载样式和执行JavaScript代码的过程没有固定的次序。

```
// 第一种
function loadStyle(url) {
	var link = document.createElement('link');

	link.rel = "stylesheet";
	link.type = "text/css";
	link.href = url;
	var head = document.getElementsByTagName('head')[0];
	head.appendChild(link);
}

// 第二种
function laodStyleString(css) {
	var style = document.createElement('style');
	
	style.type = "text/css";
	try {
		style.appendChild(document.createTextNode(css));
	} catch(ex) {
		style.styleSheet.cssText = css;
	}
	var head = document.getElementsByTagName('head')[0];
	head.appendChild(style);
}
loadStyleString("background-color:red;}");
```

## 操作表格

由于如果用核心DOM方法操作表格，有一些复杂。

```
var table = document.createElement('table');
table.border = '1';
table.width = '100%';

var tbody = document.createElement('tbody');
table.appendChild(tbody);

// 创建第一行
tbody.insertRow(0);
tbody.rows[0].insertCell(0);
tbody.rows[0].cells[0].appendChild(document.createTextNode('cell 00'));

tbody.rows[0].insertCell(1);
tbody.rows[0].cells[1].appendChild(document.createTextNode('cell 01'));

// 创建第二行
tbody.insertRow(1);
tbody.rows[1].insertCell(0);
tbody.rows[1].cells[0].appendChild(document.createTextNode('cell 10'));

tbody.rows[1].insertCell(1);
tbody.rows[1].cells[1].appendChild(document.createTextNode('cell 11'));

document.body.appendChild(table);
```

## 使用NodeList

理解NodeList及其"近亲"NamedNodeMap 和 HTMLCollection, 是从整体上彻底理解DOM的关键所在。这三个集合都是"动态的"; 换句话说， 每当文档结构发生变化时，它们都会得到实时更新。

```
// 会导致无限循环, 因为length会实时更新
var divs = document.getElementsByTagName('div');
var i;
var div;

for(i = 0;i < divs.length;i++) {
	div = document.createElement('div');
	document.body.appendChild(div);
}

// 这样就可以了。
var len;
for(i = 0, len = divs.length;i++) {
	// ...
}
```

