# DOM

## 节点层次 

```
<html>
    <head>
        <meta charset="utf-8">
        <title>This is a Test Page</title>
    </head>
    <body>
        <p>Hello world</p>
    </body>
</html>
```

1. **文档节点**是每个文档的根节点。

2. 上面的例子中，文档节点只有一个子节点，即<code><html></code>元素。我们又称之为**文档元素**。文档元素是文档的最外层元素，文档的其他所有元素都包括在文档元素中。

3. 每个文档只有一个文档元素，在<code>HTML</code>页面中，文档元素始终是<code>html</code>元素。
    
4. 一个有12种节点类型，这些类型都继承自一个基类型。

### Node类型	

1. DOM1级定义了一个Node接口, 该接口由DOM中所有节点类型实现.

2. 这个Node接口在JavaScript中是作为Node类型实现的；除了IE外，其他所有浏览器都可以访问到这个类型。

3. JavaScript中所有的节点类型都继承自Node类型，因此所有节点类型都共享着相同的基本属性和方法。

#### 节点属性

每个节点都有<code>nodeValue, nodeName, nodeType</code>属性，用于表明节点的类型。

    ```
    if (someNode.nodeType === 1) {
        var name = someNode.nodeName;
        console.log(name);
        console.log(This is an element);
    }
    ```


#### 节点关系

1. 每一个节点都有childNodes属性，这个属性是动态的(如果页面内容更新了，那么childNodes也有可能更新), 它是一个HTMLCollection对象。访问方法如下：

    ``` 
    var firstChild = someNode.childNodes[0];
    var secondChild = someNode.childNdoes.item(1);
    ```

2. previousSibling和nextSibling可以访问同胞节点

3. firstChild和lastChild属性

4. parentNode属性

5. hasChildNodes()方法 => true/false

6. 所有节点的最后一个属性是ownerDocument,该属性指向表示整个文档的文档节点

#### 操作节点

1. someNode.appendChild(newNode), 向someNode末尾添加节点，如果添加的节点已经存在，那么就是移动移动元素。返回值是新增的节点。

2. 插入到指定位置：insertBefore(要插入的节点，作为参照的节点)

    ``` 
    returnNode = someNode.insertBefore(newNode, oldNode);
    ```

3. replaceChild(要插入的节点，要替换的节点)：替换节点

    ``` 
    returnNode = someNode.replaceChild(newNode, oldNode)
    ```

4. 移除节点: removeChild(要移除的节点)

5. 所有类型的节点都有的方法：cloneNode(true/false):表示深复制和浅复制,  复制后节点是游离的。

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
	
6. normalize()方法处理文档树的文本节点，如果文本节点里无文本，就删除它，如果找到相邻的文本节点,就合并它们。


### Document类型

1. JavaScript通过Document类型表示文档。

2. HTMLDocument继承自Document。

3. 在浏览器中，document对象是HTMLDocument的一个实例。表示整个HTML页面。

4. 而且，document对象是window对象的一个属性，因此可以作为全局使用。

#### 文档的子节点


1. 访问文档的子节点的快捷方法有：

    ```
    <html>
        <head></head>
        <body></body>
    </html>
    ```

    对于上面的这种结构(没有doctype声明)，下面的测试都是正确的。如果有doctype声明的话，<code><!DOCTYPE html></code>也是文档的子节点。

    ```
    // 第一个
    var html = document.document.documentElement; // 取得对<html>的引用

    // 第二个
    // 不推荐这个，因为可能有注释节点，而注释节点每个浏览器对它的解析又不一样。
    var html = document.childNodes[0];     ```

    // 第三个, 不推荐
    var html = document.firstChild;
    ```

2. 作为HTMLDocument的实例，document对象还有一个body属性，直接指向<code>body</code>元素。

    ```
    var body = document.body;
    ```

3. document还有的一个属性<code>document.doctype</code>可以获取。但是不同浏览器对doctype的支持不一样。所以不推荐使用。


#### 文档信息

作为HTMLDocument的一个实例，document对象还有标准的Document对象所没有的属性。这些属性提供了document对象所表现的网页的一些信息。

1. document.title

2. document.URL, 显示页面的一个完整URL地址(地址栏里的URL)。

3. document.domain, 显示页面的域名。

4. document.referrer，保存着链接到当前页面的那个页面的URL。

5. 三个属性中，只有document.domain可以设置。

    ```
    * 不能将这个属性设置为URL中不包含的域。    

    * 如果域名一开始是松散的，那么不能将它设置为紧绷的。也就是说, 开始如果是baidu.com，就不能设置为www.baidu.com
    ```

#### 查找元素

1. document.getElementById()，这是Document类型提供的方法。

2. document.getElementsByTagName()，返回HTMLCollection对象，这是Document类型提供的方法。

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

3. document.getElementsByName(), 这是HTMLDocument类型提供的方法, 常用方法是获取单选按钮。


#### 特殊集合

document对象还有一些特殊的集合，都是HTMLColletion类型的。

1. document.anchors, 包含文档中所有带name特性的<a>元素。

2. document.forms

3. document.images

4. document.links, 包含文档中所有带href属性的<a>元素。


#### DOM一致性检测

#### 文档写入

1. document.write(), 常用与向文档中写入元素或者加载资源(script)。

2. document.writeln()

3. document.open()

4. document.close()


### Element类型


