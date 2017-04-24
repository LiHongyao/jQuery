  jQuery可以操作HTML页面元素，其重要的部分，就是对DOM的操作能力。在上一章中，我们已经了解了如何使用jQuery获取页面元素，本章我们主要学习在元素上通过jQuery实现一些操作。

# 一、jQuery  内容操作

## 1、获取/更改内容

### 1）、.html()

  返回或设置匹配元素内部的html，类似于DOM中的 *innerHTML*；

  当使用该方法从jQuery选取结果中获取信息时，它会返回第一个匹配元素内部的HTML，包括其所有的后代节点。

```html
<ul>
	<li><b>html</b></li>
	<li>css</li>
	<li>JavaScript</li>
    <li>jQuery</li>
</ul>
```

  例如，*$('ul').html()* 会返回如下内容：

```javascript
/*
<li><b>html</b></li>
<li>css</li>
<li>JavaScript</li>
*/
```

  而 *$('li').html()* 则返回如下内容：`<b>html</b>`

>注意：上面这个方法只会返回第一个 \<li> 元素中的内容。如果想要获取每个元素的值，可以使用 *.each()* 方法，后文会介绍。 

  当然你也可以使用 *.html()* 设置元素内容，可包含HTML，如下所示：

```html
<!-- HTML 部分 -->
<div></div>

<!-- JavaScript 部分 -->
<script type="text/javascript" src="jquery-3.2.1.min.js"></script>
<script type="text/javascript">

$('div').html('<b>Hello, world!<b>');

</script>
```

  上述代码执行之后，*div* 标签中将嵌套 *b* 标签；

### 2）、.text()

  设置或返回所选元素的文本内容，类似于DOM操作中的 *textContent*；

  当使用该方法从jQuery选取结果中获取文本时，它会返回jQuery选取结果中每个元素的内容，包括所有后代元素中的文本。

```html
<ul>
	<li><b>html </b></li>
	<li>css </li>
	<li>JavaScript </li>
    <li>jQuery </li>
</ul>
```

  例如，*$('ul').text()* 会返回如下内容：  

```javascript
/*
"
	html
	css
	JavaScript
"
*/
```

  而 *$('li').text()* 则会返回这些内容：`"html css JavaScript jQuery "`；

> 注意：上面这个方法会返回所有 \<li> 元素中的文字（包括单词后面的空格），但是列表项之间的空格则不会返回。如果需要获取 \<input> 或 \<textarea> 元素的内容，请使用 *.val()* 方法，详情见下文。

  同样的，你也可以通过 *.text()* 方法设置元素显示的文本：

```html
<!-- HTML 部分 -->
<div>Hello, world!</div>

<!-- JavaScript 部分 -->
<script type="text/javascript" src="jquery-3.2.1.min.js"></script>
<script type="text/javascript">

$('div').text('Hello, China!');

</script>
```

> 注意：使用 *.text()* 方法设置文本时，标签也会被转化成文本，该方法不能识别 html 标签。

### 3）、.replaceWith() 

  该方法会把匹配结果中的每个元素的内容替换为新的内容，同时返回被替换的元素。参考如下示例：

```html
<!-- HTML 部分 -->
<div>Hello, world!</div>

<!-- JavaScript 部分 -->
<script type="text/javascript" src="jquery-3.2.1.min.js"></script>
<script type="text/javascript">

$('div').replaceWith('<p>Hello, China!</p>');
// <div>Hello, world!</div>

</script>
```

  上述代码中，*\<div>Hello, world!\</div>*  被替换为 *\<p>Hello, china!\</p>*。

### 4）、.remove()

  该方法会移除匹配结果中的所有元素，包括元素自身，该方法无需设置参数。详情参考如下示例：

```html
<!-- HTML 部分 -->
<ul>
	<li>html </li>
	<li>css </li>
	<li>JavaScript </li>
	<li>jQuery </li>
</ul>

<!-- JavaScript 部分 -->
<script type="text/javascript" src="jquery-3.2.1.min.js"></script>
<script type="text/javascript">

$('ul').remove();

</script>
```

  上述代码中，连同 \<ul> 及其子元素都会被移除。

> 提示：*.html()* 、*.text()* 、*.replaceWith()* 方法可以使用字符串作为参数，这个字符串可以保存在一个变量中，也可以包含HTML标记。

  在使用上述方法更新元素内容时，可以使用字符串、变量或函数，如下将演示使用三个方法来更新页面中的内容：

```html
<!-- HTML 部分 -->
<p>Hello, world!</p>
<div>Hello, world!</div>
<section>Hello, world!</section>


<!-- JavaScript 部分 -->
<script type="text/javascript" src="jquery-3.2.1.min.js"></script>
<script type="text/javascript">

// 1、使用字符串更新内容
$('p').text('Hello, china!');

// 2、使用变量更新内容
let text = '<b>Hello, china!</b>';
$('div').html(text);

// 3、使用函数更新内容
$('section').html(function() {
	return `<b>${$(this).text()}</b>`;
});

</script>
```

  上述示例中使用 ES6 新增的模板字符串 (\``)，*this* 指向选中的 \<section> 元素，*$(this)* 将该元素转换为一个新的jQuery对象，然后可以在其上使用 jQuery的方法。

## 2、元素操作

### 1）、.before()

  在匹配的元素之前插入内容；

### 2）、.after()

  在匹配的元素之后插入内容；

### 3）、.prepend()

  向匹配元素集合中的每个元素开头插入由参数指定的内容;

### 4）、.apend()

  向匹配元素集合中的每个元素结尾插入由参数指定的内容;

### 5）、.remove()

  从DOM树中移除匹配的元素及其所有的后代和文本节点；

### 6）、.deatach()

  与 *remove()* 方法相同，不过会在内存中保留副本，因此被删除的元素还可以重新被插回页面；

### 7）、.empty()

  移除匹配结果元素中的子节点和后代节点；

### 8）、.unwrap()

  移除匹配结果的父节点，并保留匹配元素；

### 9）、.clone()

  创建匹配结果及其后代和文本节点的副本；

### 10）、.add()

  向已有的选取结果中添加新的元素；

### 11）、.insertAfter()

  把匹配的元素插入到另一个指定的元素集合的后面。

### 12）、.insertBefore()

  把匹配的元素插入到另一个指定的元素集合的前面。

### 13）、综合案例

```html
<!-- HTML 部分 -->
<div>
	<p>Hello, China!</p>
</div>
<h1>jQuery Test</h1>
<section>
	<p>Hello, China!</p>
</section>


<!-- JavaScript 部分 -->
<script type="text/javascript" src="jquery-3.2.1.min.js"></script>
<script type="text/javascript">

// 获取div元素
var $div = $('div');
// 克隆div元素
var $cloneQuote = $div.clone();
// 移除div元素
$div.remove();
// 将克隆出来的div插入到h1的后面
$cloneQuote.insertAfter('h1');

// 清空section
$('section').empty();

// 在section中追加元素
var $b = $('<b>Hello, World!</b>')
$('section').append($b);

</script>
```

## 3、属性操作

  可以使用 *attr()* 和 *removeAttr()* 方法来操作任何元素的任何属性。如果使用 *attr()* 方法来更新一个不存在的属性，就会创建这个属性并赋予其指定的值。class 属性值可以包含多个 class 名称（之间用空格隔开）。*addClass()* 和 *removeClass()* 方法的强大之处，就在于可以使用它们来添加或移除class属性值中单独的 class 名称，而不影响其他的 class 名称。

### 1）、.attr()

  设置或返回匹配元素的属性和值。

- 获取属性：*attr(attrName)*
- 设置属性：*attr(attrName, attrValue)*

### 2）、.removeAttr()

  该方法用来移除指定的属性（及其属性值）。只需要在小括号中指定需要从元素移除的属性的名称即可。

### 3）、.addClass()

  该方法用于向 class 属性已有的值中添加一个新值，它不会覆盖已有的属性值。

### 4）、.removeClass()

  该方法用于从 class 属性值中溢出一个属性值，并保留该属性中的其他 class 名称。

### 5）、.css()

  jQuery 提供 *css()* 方法来获取或设置元素样式，获取css属性时，需要在小括号中指定需要获取哪个属性。如果匹配结果中包含多个元素，该方法会返回第一个元素的值。

- 获取css属性

  ```javascript
  $('div').css('background-color');
  ```

- 设置css属性

  ```javascript
  $('div').css('background-color', 'red');
  ```

- 设置多个属性

  ```javascript
  $('div').css({
  	'width' : '200px',
  	'height': '200px',
  	'background-color': 'red'
  });
  ```

## 4、表单值

  jQuery 提供 *val()* 方法获取和设置表单值，主要用于 \<input>、\<select> 和 \<textarea> 元素。在使用该方法获取值时，获取的是匹配元素中第一个元素的值，在使用该方法设置值时，设置的是匹配元素中每个元素的值。

# 二、查找元素



