# BOM

## window对象

在浏览器中，window对象扮演着两个角色，它们分别是：
* 作为访问浏览器的接口
* 作为Global对象

### 全局作用域

```
var age = '18';
window.name = 'yzf';

delete age; // 返回false
delete window.name; // 返回true
```

### 窗口关系和框架

1. 每个框架都有一个window对象，它们都保存在frames集合中。

2. top对象-----浏览器窗口。

3. parent对象-----指向当前框架的直接上层框架。

4. self对象-----始终指向window对象。

### 窗口位置

1. IE, Safari, Opera, Chrome都提供了screenLeft和screenTop属性。

2. Firefox提供了screenX和screenY属性。

```
var leftPos = (typeof window.screenLeft == 'number' ? 
		window.screenLeft : window.screenX);

var topPos = (typeof window.screenTop == 'number' ? 
		window.screenTop : window.screenY);
```

### 窗口大小

1. IE9+, Safari, firefox提供了outerWidth, outerHeight属性，表示浏览器本身的尺寸。

2. Opera提供了outerWidth, outerHeight属性，表示页面视图容器(单个标签对应的浏览器窗口)的大小。 

3. Opera提供了innerWidth, innerHeight属性，表示页面视图区(减去边框宽度)的大小。

4. Chrome提供了上面的这四种属性，都表示视口的大小，而非浏览器的大小。

5. 虽然无法确定浏览器的窗口大小，但是可以确定浏览器的视口大小，如下：

```
document.documentElement.clientWidth;
document.body.clientWidth;
```

### 导航和打开窗口

1. window.open，它有四个参数。分别表示:
	* URI
	* 窗口目标，可以是框架的name，还可以是：<code>_self, _parent, _top, _blank</code>
	* 一个表示浏览器特性的字符串
	* 表示新页面 是否 取代 浏览器浏览历史记录中 当前加载页面的 布尔值。
2. window.open()返回一个指向新窗口的引用。

3. window.close();

4. 新打开的窗口有一个opener属性，指向打开它的原始窗口。

5. xx.opener = null;可以切断标签页的联系。

### 系统对话框

```
alert();
comfirm(); 返回ture或false
prompt(); 传入询问的字符串和默认的提示字符串。
```

## location对象

最有用的BOM对象之一。

location有几个属性：

* hash, "#content"
* host, "www.example.com:8080"
* hostname, "www.example.com"
* href, "http://www.example.com"
* pathname, "/test"
* port, "8080"
* search, "?x=3"

### 查询字符串参数

```
function getQueryStringArgs() {
	
	var qs = (location.search.length > 0 ? location.search.substring(1) : "");
	var args = {};

	var items = qs.length ? qs.split('&') : [];
	var item = null;
	var name = null;
	var value = null;

	for(var i = 0;i < items.length;i++) {
		item = items.split('=');
		name = decodeURIComponent(item[0]);
		vaule = decodeURIComponent(item[1]);

		if(name.length) {
			args[name] = value;
		}
	}

	return args;
}
```

### 位置操作

* location.assign('http://www.example.com');
* location.href('http://www.example.com');
* window.location('http://www.example.com');

上面的第2和第3个方法，在背后会调用assign方法。还有一个replace方法, 书上说传入URL后跳转了之后会禁用后退按钮，但是在chrome里测试，并没有禁用。

还有一个reload()方法，重新加载, 如果传入true，会从服务器里重新加载。


## navigator对象

用的少，可以用来检测插件。

## screen对象

用的少，记录了显示屏的信息。

## history对象

```
history.go(1);
history.forword();
history.back();
```
