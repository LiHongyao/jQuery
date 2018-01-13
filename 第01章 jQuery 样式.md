# 第 01 回：选择器

jQuery允许使用css选择器查找元素，其语法形式为：`$('Selector')`，它还提供了一些额外的选择器，见下方的 \`*jQuery*` 注释。

## 1、查找元素

- `*`：通用选择器 **->** 返回页面所有的html元素节点集合；


- `element`：标签选择器 **->** 返回所有指定标签元素节点集合；


- `#id`：id选择器 **->** 返回指定id元素节点；
- `.class`：返回指定class元素节点集合;
- `selector1, selector2, selectorN`：群组选择器 **->** 返回所有指定群组选择器元素节点集合；

## 2、基本选择器

- `ancestor descendant`：后代选择器 **->** 返回指定后代元素节点集合；
- `parent > child'`：子类选择器 **->** 返回指定子类元素节点集合；
- `prev + next`：同级元素选择器 **->** 返回指定同级元素节点，当前节点的下一节点；
- `prev ~ sibilings`：同级元素选择器 **->** 返回指定同级元素节点，当前节点后面所有的指定元素节点；

## 3、基本筛选器

- `:not(selector)`：除选择器之外的所有元素。 比如 `div:not('#summary')` 
- `:first`：选中元素中的第一个元素；*（ jQuery ）*
- `:last`：选中元素中的最后一个元素；*（ jQuery ）*
- `:even`：选中元素中索引编号为偶数的元素；*（ jQuery ）*
- `:odd`：选中元素中索引编号为奇数的元素；*（ jQuery ）*
- `:eq(index)`：选中元素中索引编号为参数中指定数字的元素；*（ jQuery ）*
- `:gt(index)`：选中元素中索引编号大于参数中指定数字的元素；*（ jQuery ）*
- `:lt(index)`：选中元素中索引编号小于参数中指定数字的元素；*（ jQuery ）*
- `header`：所有的 \<h1>到\<h6>元素；*（ jQuery ）*
- `:animated`：正在进行动画的元素；*（ jQuery ）*
- `：focus`：当前拥有焦点的元素；

## 4、内容筛选器

- `:contains('text')`：包含参数中指定文本的元素；
- `:empty`：没有子节点的所有元素；
- `:parent`：拥有子节点（文本或子元素）的元素；*（ jQuery ）*
- `:has(selector)`：至少包含一个匹配选择器的元素；比如：`div:has(p)` 匹配所有包含\<p>元素的\<div>元素；

## 5、可见性筛选器

- `:hidden`：所有隐藏的元素；*（ jQuery ）*

- `:visible`：所有在页面布局中占据空间的元素；*（ jQuery ）*

  > 1、不会选中的元素包括：*display: none; height/width: 0; 祖先元素被隐藏*；

  > 2、会选中的元素包括：*visibility: hidden; opacity: 0;* 因为他们都会在布局中占据空间； 

## 6、子节点筛选器

- `:nth-child(n)`：指定下标位置的子节点；
- `:first-child`：当前选中元素的第一个子节点；
- `:last-child`：当前选中元素的最后一个子节点；
- `:only-child`：当元素是父元素中位移的子节点时；

## 7、属性选择器

- `[attribute]`：拥有指定属性的元素（属性值不限）；
- `[attribute  = 'value']`：拥有指定属性，并且值为指定值的元素；
- `[attribute != 'value']`：拥有指定属性，并且值不为指定值的元素；*（ jQuery ）*
- `[attribute ^= 'value']`：属性值以特定值开头；
- `[attribute $= 'value']`：属性值以特定值结尾；
- `[attribute *= 'value']`：属性值含有特定值；

## 8、表单

- `:input`：匹配所有 input, textarea, select 和 button 元素；*（ jQuery ）*
- `:text`：匹配所有文本类型的input元素；*（ jQuery ）*
- `:password`：匹配所有密码类型的input元素；*（ jQuery ）*
- `:radio`：匹配所有单选按钮；*（ jQuery ）*
- `:checkbox`：匹配所有复选框；*（ jQuery ）*
- `:submit`：匹配所有提交按钮；*（ jQuery ）*
- `:image`：匹配所有图片按钮；*（ jQuery ）*
- `:reset`：匹配所有重置按钮；*（ jQuery ）*
- `:button`：匹配所有按钮；*（ jQuery ）*
- `:file`：匹配所有文件域；*（ jQuery ）*
- `:selected`：匹配下拉列表中所有被选中的列表项；
- `:enabled`：匹配所有可用元素；


- `:enabled`：匹配所有可用的表单元素；
- `:disabled`：匹配所有禁用的表单元素；
- `:checked`：匹配所有被选中的按钮或复选框；


> 提示：
>
> 1. jQuery选中一个或多个元素后，会返回一个jQuery对象（类似数组对象）。这个对象通常被称为 “匹配结果集” 或 “jQuery选取结果”。每一个元素都有一个索引编号，我们可通过索引取到结果集中的具体对象。由于jQuery的选取结果为一个集合，因此可能会含有多个元素。如果匹配结果集中含有多个元素，在使用一个方法获取信息时，那么jQuery只会从匹配结果集的第一个元素中获取此信息；在使用一个方法更新信息时，那么jQuery会更新匹配结果集中所有元素的信息，而不止第一个元素。jQuery对象会保存对元素的引用。把jQuery对象缓存在变量中，变量中就包含了对元素的引用。当变量包含一个jQuery对象时，通常都会在变量名的前面加一个`$`符号用来区分脚本中的其他变量，比如：`let $imgBox = $('#img-box');`。
> 2. `this` 是 JavaScript 中的关键字；`$(this)` 是 jQuery 对象；

# 第 02 回：文本

读取、修改元素的html结构或者元素的文本内容是常见的DOM操作，jQuery针对这样的处理提供了2个便捷的方法.html()与.text()

## 1、.html()

获取/设置集合中第一个匹配元素的HTML内容，常用的有如下两种使用方法：

- .html()：获取集合中第一个匹配元素的HTML内容
- .html( htmlString )：设置每一个匹配元素的HTML内容

> 提示：.html() 方法如DOM中的innerHTML()方法，所以在设置与获取上需要注意的一个最重要的问题，这个操作是针对整个HTML内容（不仅仅只是文本内容）

 ## 2、.text()

获取匹配元素集合中每个元素的文本内容结合，包括他们的后代，或设置匹配元素集合中每个元素的文本内容为指定的文本内容。具体有2种用法：

- .text()：获取匹配元素集合中每个元素的合并文本，包括他们的后代
- .text( textString )：设置匹配元素的文本

> 提示：.text()结果返回一个字符串，包含所有匹配元素的合并文本

**c、.html & .text similarities and differences**

- .html与.text的方法操作是一样，只是在具体针对处理对象不同
- .html处理的是元素内容，.text处理的是文本内容
- .html只能使用在HTML文档中，.text 在XML 和 HTML 文档中都能使用
- 如果处理的对象只有一个子文本节点，那么html处理的结果与text是一样的
- 火狐不支持innerText属性，用了类似的textContent属性，.text()方法综合了2个属性的支持，所以可以兼容所有浏览器

## 3、.val()

该方法主要用于处理表单元素的值，比如input、select和textarea。其使用方法有一下3种形式：

- .val()：获取匹配的元素集合中第一个元素的当前值
- .val( value )：设置匹配的元素集合中每个元素的值
- .val( function )：一个用来返回设置值的函数

> 提示：
>
> 1. 通过.val() 处理select元素，当没有选择项被选中时，它返回null
> 2. .val() 方法多用来设置表单字段的值
> 3. 如果select元素由multiple（多选）属性，并且至少一个选择项被选中，.val() 方法返回一个数组，这个数组包含每个选中选择项的值。

**.html()、.text()、.val() 的差异总结：**

- *.html()*，*.text()*，*.val()* 三种方法都是用来读取选定元素的内容；只不过*.html()*是用来读取元素的html内容（包括html标签），*.text()* 用来读取元素的纯文本内容，包括其后代元素，*.val()* 是用来读取表单元素的"value"值。其中 *.html()* 和 *.text()* 方法不能使用在表单元素上,而 *.val()* 只能使用在表单元素上；另外 *.html()* 方法使用在多个元素上时，只读取第一个元素；*.val()* 方法和 *.html()* 相同，如果其应用在多个元素上时，只能读取第一个表单元素的"value"值，但是 *.text()* 和他们不一样，如果 *.text()* 应用在多个元素上时，将会读取所有选中元素的文本内容。
- *.html(htmlString)*, *.text(textString)* 和 *.val(value)* 三种方法都是用来替换选中元素的内容，如果三个方法同时运用在多个元素上时，那么将会替换所有选中元素的内容。
- *.html()* , *.text()* , *.val()* 都可以使用回调函数的返回值来动态的改变多个元素的内容。

# 第 03 回：属性

## 1、元素属性

- .attr(key[, value])：获取/设置属性
- .attr(attributes)：给指定元素设置多个属性值，语法形式为：{属性名1:属性值1, 属性名2:属性值2, …...}
- .removeAttr(key)：移除属性

## 2、状态属性

通过 *attr()* 方法也能设置状态属性，但是却不能切换状态（true和false之间切换），也就是说它可以让一个多选框被选中，却不能让它取消选中，所以要去做类似的状态切换操作需要用到 *prop()* 这个方法。

- .prop(key[, value])：获取/设置状态属性
- .removeProp(key)：移除状态属性
- indeterminate：获取/设置 “checkbox” 半选中状态

## 3、.data()

HTML5 dataset 是新的HTML5标准，允许你在普通的元素标签里嵌入类似 *data-\** 的属性，来实现一些简单数据的存取。它的数量不受限制，并且也能由JavaScript动态修改，也支持CSS选择器进行样式设置。这使得data属性特别灵活，也非常强大。有了这样的属性我们能够更加有序直观的进行数据预设或存储。那么在不支持HTML5标准的浏览器中，我们如何实现数据存取?  jQuery就提供了一个*.data()* 的方法来处理这个问题。

使用jQuery初学者一般不是很关心data方式，这个方法是jquery内部预用的，可以用来做性能优化。当然这个也是非常重要的一个API了，常常用于我们存放临时的一些数据，因为它是直接跟DOM元素对象绑定在一起的

jQuery提供的存储接口

```javascript
// 1、静态接口
jQuery.data( element, key, value )   // 存数据
jQuery.data( element, key )  // 取数据   

// 2、实例接口
.data( key, value ) // 存数据
.data( key ) // 取数据
```

2个方法在使用上存取都是通一个接口，传递元素，键值数据。在jQuery的官方文档中，建议用.data()方法来代替。

我们把DOM可以看作一个对象，那么我们往对象上是可以存在基本类型，引用类型的数据的，但是这里会引发一个问题，可能会存在**循环引用的内存泄漏风险**。

通过jQuery提供的数据接口，就很好的处理了这个问题了，我们不需要关心它底层是如何实现，只需要按照对应的data方法使用就行了。

同样的也提供2个对应的删除接口，使用上与data方法其实是一致的，只不过是一个是增加一个是删除罢了。

```javascript
jQuery.removeData( element [, name ] )

.removeData( [name ] )
```

# 第 04 回：样式

## 1、.class Styles

- .hasClass()

  该方法用于判断元素是否包含某class。

- .addClass()

  该方法可以为元素添加类名，通过动态改变类名，可以让其修改元素呈现不同的效果.

  > 提示：如果添加多个类名，请使用空格隔开。.addClass()方法不会替换一个样式类名。它只是简单的添加一个样式类名到元素上

- .removeClass()

  该方法的作用是从匹配的元素中删除全部或者指定的class，使用方法如下：

  .removeClass()：删除所有class

  .removeClass([ className ])：每个匹配元素移除的一个或多个用空格隔开的样式名

- .toggleClass()

  该方法主要用于类名的互斥切换，比如有时我们需要在删除对应类名和添加赌赢类名之间切换的时候，我们可直接使用该方法，更加方便。一次执行，相当于addClass，再次执行相当于removeClass。

## 2、.css Styles

`.css()` 方法主要用于设置/获取DOM元素样式。

**a、获取**

- .css( propertyName )：获取匹配元素集合中的第一个元素的样式属性的计算值
- .css( propertyNamess )：传递一组数组，返回一个对象结果

**b、设置**

- .css(propertyName, value )：设置CSS
- .css( properties )：可以传一个对象（严格语法json），同时设置多个样式

# 第 05 回：尺寸与位置

- `.height()`：获取/设置匹配元素当前计算的高度值（px）
- `.innerHeight()`：获取第一个匹配元素内部区域高度（包括padding、不包括border）。
- `.outerHieght()`：获取第一个匹配元素外部高度（默认包括padding和border）。
- `.width()`：获取/设置第一个匹配元素当前计算的宽度值（px）。
- `.innerWidth()`：获取第一个匹配元素内部区域宽度（包括padding、不包括border）。
- `.outerWidth()`：获取第一个匹配元素外部宽度（默认包括padding和border）。
- `.scrollTop()`：设置/获取匹配元素相对滚动条顶部的偏移。
- `.scrollLeft()`：设置/获取匹配元素相对滚动条左侧的偏移。
- `offset()`：获取元素偏移，相对于文档而言，有四个选项（`.top, .left, .right, .bottom`）
- `position`：获取元素位置，相对于拥有定位属性的祖先级元素而言，有四个选项（`.top, .left, .right, .bottom`）














