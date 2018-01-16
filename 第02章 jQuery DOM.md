# 第01回：节点创建

## 1、创建元素节点

可以有几种方式，后面会慢慢接触。常见的就是直接把这个节点的结构通过HTML标记字符串描述出来，通过$()函数处理，$("html结构")

```javascript
$('<div></div>')
```

## 2、创建文本节点

与创建元素节点类似，可以直接把文本内容一并描述

```javascript
$('<div>我是文本节点</div>')
```

## 3、创建属性节点

与创建元素节点同样的方式

```javascript
$("<div id='test' class='gg'>我是文本节点</div>")
```

# 第02回：节点插入

## 1、.append() 、.appendTo()

| 选择器         | 描述                          |
| ----------- | --------------------------- |
| append( )   | 向每个匹配的元素内部追加内容              |
| appendTo( ) | 把所有匹配的元素**追加到**另一个、指定的元素集合中 |

```javascript
$(A).append(B);  // 把B添加到A中(后面)
$(A).appendTo(B);// 把A添加到B中(后面)
```

## 2、.after()、.before()

| 选择器       | 描述         |
| --------- | ---------- |
| after( )  | 指定元素后面添加内容 |
| before( ) | 指定元素前面添加内容 |

```javascript
$(A).after(B); // 在A的后面添加B
$(A).before(B);// 在A的前面添加B
```

## 3、.prepend()、.prependTo()

| 选择器          | 描述              |
| ------------ | --------------- |
| prepend( )   | 指定元素内部前置一内容     |
| prependTo( ) | 指定元素前置到另一个元素的内部 |

```javascript
$(A).prepend(B);   // 把B添加到A中(前面)
$(A).prependTo(B); // 把A添加到B中(前面)
```

## 4、.insertAfter()、.insertBefore()

| 选择器            | 描述            |
| -------------- | ------------- |
| insertAfter()  | 将内容插入到指定元素的后面 |
| insertBefore() | 将内容插入到指定元素的前面 |

```javascript
$(A).insertAfter(B);  // 将A插入到B的后面
$(A).insertBefore(B); // 将A插入到B的前面
```

# 第03回：节点删除

## 1、.empty()

该方法主要是用于清空指定元素的所有子节点，如：

```html
<div class="hello"><p>耀哥</p></div>
```

如果我们通过empty方法移除里面div的所有元素，它只是清空内部的html代码，但是标记仍然留在DOM中。

```javascript
//通过empty处理
$('.hello').empty()

// 结果：<p>耀哥</p> 被移除
<div class="hello"></div>
```

## 2、.remove()

remove与empty一样，都是移除元素的方法，但是remove会将元素自身移除，同时也会移除元素内部的一切，包括绑定的事件及与该元素相关的jQuery数据。

例如一段节点，绑定点击事件：

```javascript
$('.btn').on('click', function() {
	alert('Hello, world!');
});
```

如果不通过remove方法删除这个节点其实也很简单，但是同时需要把事件给销毁掉，这里是为了防止"内存泄漏"，所以前端开发者一定要注意，绑了多少事件，不用的时候一定要记得销毁。

通过remove方法移除div及其内部所有元素，remove内部会自动操作事件销毁方法，所以使用使用起来非常简单。

```javascript
// 通过remove处理
$('.btn').remove()
// 结果：节点不存在了,同时事件也会被销毁
```

remove比empty好用的地方就是可以传递一个选择器表达式用来过滤将被移除的匹配元素集合，可以选择性的删除指定的节点。

## 3、.detach()

如果我们希望临时删除页面上的节点，但是又不希望节点上的数据与事件丢失，并且能在下一个时间段让这个删除的节点显示到页面，这时候就可以使用detach方法来处理。

detach从字面上就很容易理解。让一个web元素托管。即从当前页面中移除该元素，但保留这个元素的内存模型对象。

> jQuery 官方文档说明：

> ```javascript
> 这个方法不会把匹配的元素从jQuery对象中删除，因而可以在将来再使用这些匹配的元素。与remove()不同的是，所有绑定的事件、附加的数据等都会保留下来。
> $("div").detach()这一句会移除对象，仅仅是显示效果没有了。但是内存中还是存在的。当你append之后，又重新回到了文档流中。就又显示出来了。
> ```

当然这里要特别注意，detach方法是JQuery特有的，所以它只能处理通过JQuery的方法绑定的事件或者数据。

```html
<!DOCTYPE html>
<html lang="zh-cn">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<script src="https://cdn.bootcss.com/jquery/3.2.1/jquery.js"></script>
</head>
<body>

<h1>Hello, world!</h1>
<button>Click</button>
<script type="text/javascript">
	var flag = false;
	var p    = null;
	$('button').on('click', function() {
		flag  = !flag;
		if(flag) {
			p = $('h1').detach();
		}else {
			$('button').before(p);
			p = null;
		}
	});
</script>
</html>
```

# 第04回：节点复制与替换

## 1、.clone()

克隆节点是DOM的常见操作，jQuery提供一个clone方法，专门用于处理dom的克隆。

.clone()方法深度复制所有匹配的元素集合，包括所有匹配元素、匹配元素的下级元素、文字节点。

clone方法比较简单就是克隆节点，但是需要注意，如果节点有事件或者数据之类的其他处理，我们需要通过*clone(ture)* 传递一个布尔值 `ture`用来指定，这样不仅仅只是克隆单纯的节点结构，还要把附带的事件与数据给一并克隆了。

```javascript
// HTML部分
// <div></div>

// JavaScript部分
$("div").on('click', function() {//执行操作})

//clone处理一
$("div").clone()     // 只克隆了结构，事件丢失

//clone处理二
$("div").clone(true) // 结构、事件与数据都克隆
```

## 2、.replaceWith()、.replaceAll()

```javascript
$(A).replaceWith(B); // 把A替换为B
$(A).replaceAll(B);  // 把B替换为A
```

## 3、.wrap()

如果要将元素用其他元素包裹起来，也就是给它增加一个父元素，针对这样的处理，JQuery提供了一个 *wrap* 方法。

```html
<p>Hello, world!</p>
```

```javascript
$('p').wrap('<div></div>')

// 结果为：
/*
<div>
  <p>Hello, world!</p>  
</div>
*/
```

## 4、.unwrap()

该方法与wrap方法相反，unwrap方法将匹配元素集合的父级元素删除，保留自身（和兄弟元素，如果存在）在原来的位置。

## 5、.wrapAll()

wrap是针对单个dom元素处理，如果要将集合中的元素用其他元素包裹起来，也就是给他们增加一个父元素，针对这样的处理，JQuery提供了一个wrapAll方法，比如，页面上有两个p元素，如果要为两个p元素添加共有的一个父类div，则通过如下代码实现：

```javascript
$('p').wrapAll('<div></div>');
```

## 6、.wrapInner()

如果要将合集中的元素内部所有的子元素用其他元素包裹起来，并当作指定元素的子元素，针对这样的处理，JQuery提供了一个wrapInner方法。我们来看例子：

```html
<div>Hello, world!</div>
<div>Hello, world!</div>
```

```javascript
$('div').wrapInner('<p></p>');

// 结果为：
/*
<div>
	<p>Hello, world!</p>
</div>
<div>
	<p>Hello, world!</p>
</div>	
 */
```

## 第05回：节点遍历

## 1、.children()

jQuery是一个集合对象，如果想快速查找集合里面的第一级子元素，此时可以用 *children()* 方法。这里需要注意：*.children(selector)* 方法是返回匹配元素集合中每个元素的所有子元素（仅儿子辈，这里可以理解为就是父亲-儿子的关系）

```html
<div class="div">
    <ul class="son">
        <li class="grandson">1</li>
    </ul>
</div>
```

代码如果是 *$(".div").children()* ，那么意味着只能找到ul，因为div与ul是父子关系，li与div是祖辈关系，因此无法找到。

> 提示：jQuery是一个集合对象，所以通过children是匹配集合中每一个元素的第一级子元素。

该方法可以接受参数，用于筛选子元素，如  *"$('.parent').children(.active)"*，匹配子元素中类名为 `active` 的那一个。

## 2、.find()

find 与 children 类似，区别在于 children是父子关系查找，find是后代关系查找（包含父子关系）。

```html
<div class="div">
    <ul class="son">
        <li class="grandson">1</li>
    </ul>
</div>
```

代码如果是 *“$("div").find("li")”* ，此时，li与div是祖辈关系，通过find方法就可以快速的查找到了。

> 提示：
>
> 1. find是遍历当前元素集合中每个元素的后代。只要符合，不管是儿子辈，孙子辈都可以。
> 2. 与其他的树遍历方法不同，选择器表达式对于 *.find()* 是必需的参数。如果我们需要实现对所有后代元素的取回，可以传递通配选择器 `*`。
> 3. find只在后代中遍历，不包括自己。

## 3、.parent()

如果想快速查找合集里面的每一个元素的父元素（这里可以理解为就是父亲-儿子的关系），此时可以用 *parent()* 方法。因为是父元素，这个方法只会向上查找一级。

```html
<div class="div">
    <ul class="son">
        <li class="grandson">1</li>
    </ul>
</div>
```

查找ul的父元素 div,  *$(ul).parent()* ，就是这样简单的表达

## 4、.parents()

jQuery是一个合集对象，如果想快速查找合集里面的每一个元素的所有祖辈元素，此时可以用 *parents()* 方法。其实也类似 *find* 与 *children* 的区别，parent只会查找一级，parents则会往上一直查到查找到祖先节点。

```html
<div class="div">
    <ul class="son">
        <li class="grandson">1</li>
    </ul>
</div>
```

在li节点上找到祖辈元素div， 这里可以用 *$("li").parents()* 方法

## 5、.closest()

以选定的元素为中心，往内查找可以通过find、children方法。如果往上查找，也就是查找当前元素的父辈祖辈元素，jQuery提供了*closest()* 方法，这个方法类似parents但是又有一些细微的区别，属于使用频率很高的方法。

*closest()* 方法接受一个匹配元素的选择器字符串。从元素本身开始，在DOM 树上逐级向上级元素匹配，并返回最先匹配的祖先元素。例如：在a元素中，往上查找所有的li元素，可以这样表达：*$("a").closet("li')*。

> 提示：jQuery是一个集合对象，所以通过closest是匹配集合中每一个元素的祖先元素。

粗看 *.parents()* 和 *.closest()* 是有点相似的，都是往上遍历祖辈元素，但是两者还是有区别的，否则就没有存在的意义了

- 起始位置不同：.closest 开始于当前元素 .parents开始于父元素
- 遍历的目标不同：.closest要找到指定的目标，.parents遍历到文档根元素，closest向上查找，直到找到一个匹配的就停止查找，parents 一直查找到根元素，并将匹配的元素加入集合
- 结果不同：.closest返回的是包含零个或一个元素的jquery对象，parents返回的是包含零个或一个或多个元素的jquery对象

## 6、.next()、.nextAll()

- .next()：该方法用于匹配当前元素的下一个元素。
- .nextAll()：查找当前元素之后所有的同辈元素。

## 7、.prev()、.prevAll()

- .prev()：该方法用于匹配当前元素的上一个元素。
- .prevAll()：查找当前元素之前所有的同辈元素

## 8、.siblings()

该方法用于匹配当前元素的所有兄弟元素。

## 9、.each()

jQuery是一个集合对象，通过 `$()` 方法找到指定的元素集合后可以进行一系列的操作。比如我们操作$("li").css('') 给所有的li设置style值，因为jQuery是一个集合对象，所以css方法内部就必须封装一个遍历的方法，被称为隐式迭代的过程。要一个一个给集合中每一个li设置颜色，这里方法就是each。

.each() 方法就是一个for循环的迭代器，它会迭代jQuery对象集合中的每一个DOM元素。每次回调函数执行时，会传递当前循环次数作为参数从0开始计数。所以大体上了解3个重点：

- each是一个for循环的包装迭代器
- each通过回调的方式处理，并且会有2个固定的实参，索引与元素
- each回调方法中的this指向当前迭代的dom元素

看一个简单的案例：

```html
<ul>
    <li>王者荣耀</li>
    <li>李鸿耀</li>
</ul>
```

开始迭代li，循环两次：

```javascript
$("li").each(function(index, element) {
     index 索引 0,1
     element是对应的li节点 li,li
     this 指向的是li
})
```

这样可以在循环体zhzhon中做一些逻辑操作了，如果需要提前退出，可以通过返回 false以便在回调函数内中止循环。

# 第 06 回：筛选

## 1、.eq(index|-index)

获取当前链式操作中第N个jQuery对象，返回jQuery对象，当参数大于等于0时为正向选取，比如0代表第一个，1代表第二个。当参数为负数时为反向选取，比如-1为倒数第一个，具体可以看以下示例。

## 2、.first()、.last()

- .first()：获取第一个元素
- .last()：获取最后一个元素

##3、.filter(expr|obj|ele|fn)

筛选出与指定表达式匹配的元素集合。

这个方法用于缩小匹配的范围。用逗号分隔多个表达式

## 4、.is(expr|obj|ele|fn)

根据选择器、DOM元素或 jQuery 对象来检测匹配元素集合，如果其中至少有一个元素符合这个给定的表达式就返回true。

如果没有元素符合，或者表达式无效，都返回'false'。 '''注意：'''在jQuery 1.3中才对所有表达式提供了支持。在先前版本中，如果提供了复杂的表达式，比如层级选择器（比如 + , ~ 和 > ），始终会返回true

## 5、.not(expr|ele|fn)

从匹配元素的集合中删除与指定表达式匹配的元素

## 6、.map(callback)

将一组元素转换成其他数组（不论是否是元素数组）

你可以用这个函数来建立一个列表，不论是值、属性还是CSS样式，或者其他特别形式。这都可以用'$.map()'来方便的建立。

## 7、.has(expr|ele)

保留包含特定后代的元素，去掉那些不含有指定后代的元素。

.has()方法将会从给定的jQuery对象中重新创建一组匹配的对象。提供的选择器会一一测试原先那些对象的后代，含有匹配后代的对象将得以保留。
