# 第01回：隐藏 & 显示

## 1、.hide()

  隐藏元素，其语法形式为：

```javascript
.hide( [duration ][, complete ] )
```

> 提示：元素应酬之后会脱离文档流

```html
<h1>Hello, world!</h1>
<button>隐藏元素</button>
```

```javascript
$('button').on('click', function() {
	$('h1').hide({
		// 持续时间
		duration: '1000',
		// 回调函数
		complete: function() {
			console.log('元素已隐藏！');
		}
	});
})
```

## 2、.show()

  方法的使用几乎与hide是一致的，hide是让元素显示到隐藏，show则是相反，让元素从隐藏到显示。

  看一段代码：使用上一致，结果相反

```javascript
$('button').on('click', function() {
	$('h1').hide('1000').show('1000');
})
```

> 让元素执行1秒的隐藏动画，然后执行1秒的显示动画。

  show与hide方法是非常常用的，但是一般很少会基于这2个属性执行动画，大多情况下还是直接操作元素的显示与隐藏为主

> 注意：
>
> - show与hide方法是修改的display属性，通过是visibility属性布局需要通过css方法单独设置
> - 如果使用!important在你的样式中，比如display: none !important，如果你希望.show()方法正常工作，必须使用.css('display', 'block !important')重写样式
> - 如果让show与hide成为一个动画，那么默认执行动画会改变元素的高度，高度，透明度

## 3、.toggle()

  show与hide是一对互斥的方法。需要对元素进行显示隐藏的互斥切换，通常情况是需要先判断元素的display状态，然后调用其对应的处理方法。比如显示的元素，那么就要调用hide，反之亦然。 对于这样的操作行为，jQuery提供了一个便捷方法toggle用于切换显示或隐藏匹配元素。

  语法形式如下：

```javascript
.toggle( [duration ][, complete ] )
```

# 第02回：上卷 & 下拉

## 1、.slideDown()

  对于隐藏的元素，在将其显示出来的过程中，可以对其进行一些变化的动画效果。之前学过了show方法，show方法在显示的过程中也可以有动画，但是.show()方法将会匹配元素的宽度，高度，以及不透明度，同时进行动画操作。这里将要学习一个新的显示方法slideDown方法。

  **.slideDown()：用滑动动画显示一个匹配元素**

  .slideDown()方法将给匹配元素的高度的动画，这会导致页面的下面部分滑下去，弥补了显示的方式。其语法形式为：

```javascript
.slideDown( [duration ] [, complete ] )
```

  持续时间（duration）是以毫秒为单位的，数值越大，动画越慢，不是越快。字符串 'fast' 和 'slow' 分别代表200和600毫秒的延时。如果提供任何其他字符串，或者这个duration参数被省略，那么默认使用400 毫秒的延时。

  具体使用：

```javascript
$("ele").slideDown(1000, function() {
    //等待动画执行1秒后,执行别的动作....
});
```

> 注意：
>
> - 下拉动画是从无到有，所以一开始元素是需要先隐藏起来的，可以设置display:none
> - 如果提供回调函数参数，callback会在动画完成的时候调用。将不同的动画串联在一起按顺序排列执行是非常有用的。这个回调函数不设置任何参数，但是 this会设成将要执行动画的那个DOM元素，如果多个元素一起做动画效果，那么要非常注意，回调函数会在每一个元素执行完动画后都执行一次，而不是这组 动画整体才执行一次

## 2、.slideUp()

  对于显示的元素，在将其隐藏的过程中，可以对其进行一些变化的动画效果。之前学过了hide方法，hide方法在显示的过程中也可以有动画，但 是.hide()方法将为匹配元素的宽度，高度，以及不透明度，同时进行动画操作。这里将要学习一个新的显示方法slideUp方法。

  最简单的使用：不带参数

```javascript
$("elem").slideUp();
```

  这个使用的含义就是：找到元素的高度，然后采用一个下滑动画让元素一直滑到隐藏，当高度为0的时候，也就是不可见的时，修改元素display 样式属性被设置为none。这样就能确保这个元素不会影响页面布局了。

  带参数：

```javascript
.slideUp( [duration ] [, easing ] [, complete ] )
```

  同样可以提供一个时间，然后可以使用一种过渡使用哪种缓动函数，jQuery默认就2种，可以通过下载插件支持。最后一个动画结束的回调方法。

```javascript
因为动画是异步的，所以要在动画之后执行某些操作就必须要写到回调函数里面，这里要特别注意
```

## 3、.slideToggle()

  slideDown与slideUp是一对相反的方法。需要对元素进行上下拉卷效果的切换，jQuery提供了一个便捷方法slideToggle用滑动动画显示或隐藏一个匹配元素。

**基本的操作：slideToggle();**

  这是最基本的操作，获取元素的高度，使这个元素的高度发生改变，从而让元素里的内容往下或往上滑。

**提供参数：.** **slideToggle( [duration ] ,[ complete ] )**

  同样的提供了时间、还有动画结束的回调。在参数对应的时间内，元素会完成动画，然后出发回调函数

  同时也提供了时间的快速定义，字符串 'fast' 和 'slow' 分别代表200和600毫秒的延时

> 注意：
>
> - display属性值保存在jQuery的数据缓存中，所以display可以方便以后可以恢复到其初始值
> - 当一个隐藏动画后，高度值达到0的时候，display 样式属性被设置为none，以确保该元素不再影响页面布局

# 第03回：淡入 & 淡出

  除了通过display设置元素的显示与隐藏，还有一种方法就是设置元素的不透明度，值范围为0~1，当不透明度为1时，元素显示，当不透明度为0时，元素隐藏。jQuery淡入淡出效果正是使用了这个原理。只不过，当不透明度为0时，元素虽然隐藏了，但是并没有脱离文档流，但是jQuery中，元素淡出会脱离文档流。

## 1、.fadeIn()

```javascript
.fadeIn( [duration ], [ complete ] )
```

## 2、.fadeOut()

```javascript
.fadeOut( [duration ], [ complete ] )
```

## 3、.fadeToggle

```javascript
.fadeToggle( [duration ] ,[ complete ] )
```

> 参数解读：
>
> duration：线性规律，‘fast’和‘slow’ ，相当于200ms 和 600ms，默认400ms。
>
> complete：回调函数，动画执行结束后执行

## 4、.fadeTo

```javascript
.fadeTo( duration, opacity ,callback)
```

  淡入或淡出到某一个值。当第二参数为0时，淡出，相当于fadeOut，当第二个参数为1时，淡入，相当于fadeIn。

- duration：持续时间
- opacity：不透明度的值
- callback：回调函数

# 第04回：自定义动画

## 1、.animate()

  jQuery 提供的动画有限，有时需要我们实现一些更为复杂的动画效果，这时我们就需要使用自定义动画了。当然，jQuery也为我们提供了自定义动画的接口，其语法形式如下：

```javascript
.animate( properties ,[ duration ], [ easing ], [ complete ] )
.animate( properties, options )
```

**参数解读**

- properties：一个或多个css属性的键值对所构成的Object对象，对数字属性值有效，驼峰命名，可使用快捷方式如‘show/toggle’。
- duration：持续时间，单位ms，提供'fast' 和 'slow'字符串，分别表示持续时间为200 和 600毫秒。
- easing：动画运动算法，jQuery库中默认调用 swing。如果需要其他的动画算法，请查找相关的插件
- complete：回调函数

```html
<div style="width: 100px; height: 35px; background-color: green;></div>
```

```javascript
$('div').on('mouseenter', function() {
	$(this).animate({
		marginLeft: '300px',
		width: '200px'
	}, 1000, function() {
		console.log('动画执行完成！');
	})
})
```

  上述代码表示当鼠标进入到目标元素的时候，执行1s动画效果，向右移动300px，并且增加宽度为200px。当动画执行完之后打印输出提示信息。

  animate在执行动画中，如果需要观察动画的一些执行情况，或者在动画进行中的某一时刻进行一些其他处理，我们可以通过animate提供的第二种设置语法，传递一个对象参数，可以拿到动画执行状态一些通知。

```javascript
.animate( properties, options )
```

**options参数：**

- duration：设置动画执行的时间
- easing ：规定要使用的 easing 函数，过渡使用哪种缓动函数
- step：规定每个动画的每一步完成之后要执行的函数
- progress：每一次动画调用的时候会执行这个回调，就是一个进度的概念
- complete：动画完成回调

> 关键点：如果多个元素执行动画，回调将在每个匹配的元素上执行一次，不是作为整个动画执行一次

## 2、.stop()

  动画在执行过程中是允许被暂停的，当一个元素调用.stop()方法，当前正在运行的动画（如果有的话）立即停止。

  语法形式：

```
.stop( [clearQueue ], [ jumpToEnd ] )
```

  stop还有几个可选的参数，简单来说可以这3种情况：

- .stop(); 停止当前动画，点击在暂停处继续开始
- .stop(true); 如果同一元素调用多个动画方法，尚未被执行的动画被放置在元素的效果队列中。这些动画不会开始，直到第一个完成。当调用.stop()的时候，队列中的下一个动画立即开始。如果clearQueue参数提供true值,那么在队列中的动画其余被删除并永远不会运行
- .stop(true,true); 当前动画将停止，但该元素上的 CSS 属性会被立刻修改成动画的目标值

  简单的说：参考下面代码、

```javascript
$("#box").animate({
    height: 300
}, 5000)
$("#box").animate({
    width: 300
}, box)
$("#box").animate({
    opacity: 0.6
}, 2000)
```

1. stop()：只会停止第一个动画，第二个第三个继续
2. stop(true)：停止第一个、第二个和第三个动画
3. stop(true ture)：停止动画，直接跳到第一个动画的最终状态 

# 第05回：jQuery 核心

## 1、.each()

  each 方法主要用于遍历，不仅可以遍历元素，还可以遍历数组和对象。其语法形式如下：

```javascript
// 1、遍历元素
$(selector).each()
// 2、遍历数组
jQuery.each(array, callback )
// 3、遍历对象
jQuery.each(object, callback )
```

> 提示：jQuery.each()函数还会根据每次调用函数callback的返回值来决定后续动作。如果返回值为false，则停止循环(相当于普通循环中的break)；如果返回其他任何值，均表示继续执行下一个循环。

```javascript
$.each(['HTML', 'CSS', 'Javascript'], function(idx, value) {
	console.log('idx = ' + idx + ', value = ' + value);
});
/*
idx = 0, value = HTML
idx = 1, value = CSS
idx = 2, value = Javascript
*/
```

## 2、.inArray()

  判断一个元素是否存在于数组中可以用 inArray 方法，类似于JavaScript的 indexOf，返回元素索引值，如果查询的值存在于数组中，则返回对应的下标，不能存在，则返回`-1`。其语法形式如下：

```javascript
jQuery.inArray( value, array ,[ fromIndex ] )
```

  参数解读：

- value：查询的值
- array：目标数组
- fromIndex：指定查询位置

  示例：

```javascript
var names = ['张三', '李四', '赵二', '王五'];
var result = $.inArray('赵二', names);
console.log(result); // 2
```

## 3、.trim()

  页面中，通过input可以获取用户的输入值，例如常见的登录信息的提交处理。用户的输入不一定是标准的，输入一段密码：'  1123456  "，注意了： 密码的前后会留空，这可能是用户的无心的行为，但是密码确实又没错，针对这样的行为，开发者应该要判断输入值的前后是否有空白符、换行符、制表符这样明显的无意义的输入值。

  jQuery.trim()函数用于去除字符串两端的空白字符。

```javascript
$('input').on('blur', function() {
    // 获取用户输入的文本
	var str = $.trim($(this).val());
	console.log(str);
});
```

> 提示：
>
> - 移除字符串开始和结尾处的所有换行符，空格(包括连续的空格)和制表符（tab）
> - 如果这些空白字符在字符串中间时，它们将被保留，不会被移除

## 4、.get()

  jQuery是一个集合对象，如果需要单独操作合集中的的某一个元素，可以通过**.get()**方法获取到。

  以下有3个a元素结构：

```html
<a>1</a>
<a>2</a>
<a>3</a>
```

  通过jQuery获取所有的a元素合集$("a")，如果想进一步在合集中找到第二2个dom元素单独处理，可以通过get方法。语法形式：

```javascript
.get( [index ] )
```

> 注意：
>
> - get方法是获取的dom对象，也就是通过document.getElementById获取的对象
> - get方法是从0开始索引

  所以第二个a元素的查找： `$('a').get(1)`

## 5、.index()

  get方法是通过已知的索引在集合中找到对应的元素。如果反过来，已知元素如何在集合中找到对应的索引呢？

  .index()方法，从匹配的元素中搜索给定元素的索引值，从0开始计数。

  **语法：参数接受一个jQuery或者dom对象作为查找的条件**

```javascript
.index()
.index( selector )
.index( element )
```

- 如果不传递任何参数给 .index() 方法，则返回值就是jQuery对象中第一个元素相对于它同辈元素的位置
- 如果在一组元素上调用 .index() ，并且参数是一个DOM元素或jQuery对象， .index() 返回值就是传入的元素相对于原先集合的位置
- 如果参数是一个选择器， .index() 返回值就是原先元素相对于选择器匹配元素的位置。如果找不到匹配的元素，则 .index() 返回 -1

  简单来说：

```html
<ul>
    <a></a>
    <li id="test1">1</li>
    <li id="test2">2</li>
    <li id="test3">3</li>
</ul>
```

$("li").index() 没有传递参数，返回的结果是1，它的意思是返回同辈的排列循序，第一个li之前有a元素,同辈元素是a开始为0，所以li的开始索引是1

如果要快速找到第二个li在列表中的索引,可以通过如下2种方式处理

```javascript
$("li").index(document.getElementById("test2")) //结果：1
$("li").index($("#test2"))  //结果:1
```













