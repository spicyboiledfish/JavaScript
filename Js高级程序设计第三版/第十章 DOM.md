# DOM

## Node类型	

DOM1级定义了一个Node接口, 该接口由所有节点类型实现.

### 节点关系

1. 每一个节点都有childNodes属性，这个属性是动态的。访问方法如下：

``` 
var firstChild = someNode.childNodes[0];
var secondChild = someNode.childNdoes.item(1);
```

2. previousSibling和nextSibling可以访问同胞节点

3. firstChild和lastChild属性

4. parentNode属性

5. hasChildNodes()方法 => true/false

6. 所有节点的最后一个属性是ownerDocument,该属性指向表示整个文档的文档节点

### 操作节点

1. appendChild(newNode)

2. 插入到指定位置：insertBefore(要插入的节点，作为参照的节点)

``` 
returnNode = someNode.insertBefore(newNode, oldNode);
```

3. replaceChild(要插入的节点，要替换的节点)：替换节点

``` 
returnNode = someNode.replaceChild()
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


## Document类型



