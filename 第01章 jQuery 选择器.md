  jQuery允许使用css选择器查找元素，其语法形式为：`$('Selector')`，它还提供了一些额外的选择器，见下方的 \`*jQuery*` 注释。

# 一、查找元素

- `*`：通用选择器 **->** 返回页面所有的html元素节点集合；


- `element`：标签选择器 **->** 返回所有指定标签元素节点集合；


- `#id`：id选择器 **->** 返回指定id元素节点；
- `.class`：返回指定class元素节点集合;
- `selector1, selector2, selectorN`：群组选择器 **->** 返回所有指定群组选择器元素节点集合；

# 二、基本选择器

- `ancestor descendant`：后代选择器 **->** 返回指定后代元素节点集合；
- `parent > child'`：子类选择器 **->** 返回指定子类元素节点集合；
- `prev + next`：同级元素选择器 **->** 返回指定同级元素节点，当前节点的下一节点；
- `prev ~ sibilings`：同级元素选择器 **->** 返回指定同级元素节点，当前节点后面所有的指定元素节点；

# 三、基本筛选器

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

# 四、内容筛选器

- `:contains('text')`：包含参数中指定文本的元素；
- `:empty`：没有子节点的所有元素；
- `:parent`：拥有子节点（文本或子元素）的元素；*（ jQuery ）*
- `:has(selector)`：至少包含一个匹配选择器的元素；比如：`div:has(p)` 匹配所有包含\<p>元素的\<div>元素；

# 五、可见性筛选器

- `:hidden`：所有隐藏的元素；*（ jQuery ）*

- `:visible`：所有在页面不居中占据空间的元素；*（ jQuery ）*

  > 1、不会选中的元素包括：*display: none; height/width: 0; 祖先元素被隐藏*；

  > 2、会选中的元素包括：*visibility: hidden; opacity: 0;* 因为他们都会在布局中占据空间； 

# 六、子节点筛选器

- `:nth-child(n)`：指定下标位置的子节点；
- `:first-child`：当前选中元素的第一个子节点；
- `:last-child`：当前选中元素的最后一个子节点；
- `:only-child`：当元素是父元素中位移的子节点时；

# 三、属性选择器

- `[attribute]`：拥有指定属性的元素（属性值不限）；
- `[attribute  = 'value']`：拥有指定属性，并且值为指定值的元素；
- `[attribute != 'value']`：拥有指定属性，并且值不为指定值的元素；*（ jQuery ）*
- `[attribute ^= 'value']`：属性值以特定值开头；
- `[attribute $= 'value']`：属性值以特定值结尾；
- `[attribute *= 'value']`：属性值含有特定值；

# 四、表单

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


# 五、友情提示

  jQuery选中一个或多个元素后，会返回一个jQuery对象（类似数组对象）。这个对象通常被称为 “匹配结果集” 或 “jQuery选取结果”。每一个元素都有一个索引编号，我们可通过索引取到结果集中的具体对象。

  由于jQuery的选取结果为一个集合，因此可能会含有多个元素。如果匹配结果集中含有多个元素，在使用一个方法获取信息时，那么jQuery只会从匹配结果集的第一个元素中获取此信息；在使用一个方法更新信息时，那么jQuery会更新匹配结果集中所有元素的信息，而不止第一个元素。

  jQuery对象会保存对元素的引用。把jQuery对象缓存在变量中，变量中就包含了对元素的引用。当变量包含一个jQuery对象时，通常都会在变量名的前面加一个`$`符号用来区分脚本中的其他变量，比如：`let $imgBox = $('#img-box');`。




