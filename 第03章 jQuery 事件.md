# 第01回：事件添加

语法形式：

```javascript
$el.eventType( [eventData ], handler(eventObject) )
```

```javascript
$(".btn").click("Henry", function(event) {
    // this -> 按钮对象
    console.log(`Hello, ${event.data}!`);
});
```

# 第02回：事件类型

事件类型和原生事件类型一致，这里只列出jQuery特有的一些事件：

## 1、`.hover()`

切换事件，类似于css中的hover，其语法形式为：

```js
$(selector).hover(handlerIn, handlerOut)
```

## 2、`.one()`

一次事件，顾名思义，事件方法只会触发一次。基本语法如下：

```javascript
$("div").one(eventType, handler(eventObject) )
```

> 特别注意：
>
> ```
> form元素是有默认提交表单的行为，如果通过submit处理的话，需要禁止浏览器的这个默认行为
> 传统的方式是调用事件对象  e.preventDefault() 来处理， jQuery中可以直接在函数中最后结尾return false即可
> ```
>
> jQuery处理如下：
>
> ```javascript
> $("#target").submit(function(data) { 
> 	return false; //阻止默认行为，提交表单
> });
> ```

# 第03回：事件的绑定和解绑

## 1、`on()` 事件绑定

之前学的鼠标事件，表单事件与键盘事件都有个特点，就是直接给元素绑定一个处理函数，所有这类事件都是属于快捷处理。翻开源码其实可以看到，所有的快捷事件在底层的处理都是通过一个 `.on()` 方法来实现的。jQuery  `.on()`  方法是官方推荐的绑定事件的一个方法。

**基本用法**：

```javascript
.on( events ,[ selector ] ,[ data ], fn )
```

最常见的给元素绑定一个点击事件，对比一下快捷方式与on方式的不同：

```javascript
$("#btn").click(function(){})  // 快捷方式
$("#btn").on('click',function(){}) // on方式
```

**多个事件绑定同一个函数**

```javascript
$("#btn").on("mouseover mouseout", function(){ });
```

通过空格分离，传递不同的事件名，可以同时绑定多个事件。

**多个事件绑定不同函数**

```javascript
$("#btn").on({
    mouseover: function(){},  
    mouseout: function(){}
});
```

通过逗号分离，传递不同的事件名，可以同时绑定多个事件，每一个事件执行自己的回调方法。

**将数据传递到处理程序**

```javascript
function fn(event) {
    console.log(`Hello, ${event.data.name}!`);
}
$(".btn").on("click", {name: "耀哥"}, fn);
```

可以通过第二参数（对象），当一个事件被触发时，要传递给事件处理函数的

## 2、on() 事件代理

JavaScript中，由于事件的冒泡机制，我们可以为事件设置代理，同样的，jQuery在on方法上也添加了事件代理这一机制，其语法形式如下：

```javascript
.on( events ,[ selector ] ,[ data ], handler(eventObject) )
```

在on的第二参数中提供了一个selector选择器，简单的来描述下：

参考下面3层结构

```html
<div>
    <p>
        <a>目标节点</a> 
    </p>
</div>
```

给出如下代码：

```javascript
$('div').on('click', 'p', function(e) {
	e.target.textContent = 'Hello, world!';
});
```

> 事件绑定在最上层div元素上，当用户触发在a元素上，事件将往上冒泡，一直会冒泡在div元素上。如果提供了第二参数，那么事件在往上冒泡的过程中遇到了选择器匹配的元素，将会触发事件回调函数。

## 3、`off()` 卸载事件

根据on绑定事件的一些特性，off 方法也可以通过相应的传递组合的事件名，名字空间，选择器或处理函数来移除绑定在元素上指定的事件处理函数。当有多个过滤参数时，只有与这些参数完全匹配的事件处理函数才会被移除。

绑定两个事件

```javascript
$("el").on("mousedown mouseup", fn)
```

删除一个事件

```javascript
$("el").off("mousedown")
```

删除所有事件

```javascript
$("el").off("mousedown mouseup")
```

快捷方式删除所有事件，这里不需要传递事件名了，节点上绑定的所有事件将全部销毁

```javascript
$("el").off()
```

# 第04回：事件对象

同原生

# 第05回：自定义事件

## 1、trigger事件

众所周知类似于mousedown、click、keydown 等等这类型的事件都是浏览器提供的，通俗叫原生事件，这类型的事件是需要有交互行为才能被触发。

在jQuery通过on方法绑定一个原生事件

```javascript
$('#elem').on('click', function() {
    alert("触发系统事件")
 });
```

alert需要执行的条件：必须有用户点击才可以。如果不同用户交互是否能在某一时刻自动触发该事件呢？ 正常来说是不可以的，但是jQuery解决了这个问题，提供了一个 **trigger** 方法来触发浏览器事件

所以我们可以这样：

```javascript
$('#elem').trigger('click');
```

在绑定on的事件元素上，通过trigger方法就可以调用到alert了，挺简单！

**再来看看.trigger是什么？**

> 简单来讲就是：根据绑定到匹配元素的给定的事件类型执行所有的处理程序和行为

trigger除了能够触发浏览器事件，同时还支持自定义事件，并且自定义事件还支持传递参数

```javascript
$('#elem').on('LiHy', function(event, arg1, arg2) {
    alert("触发自定义事件")
 });
$('#elem').trigger('LiHy', ['参数1', '参数2'])
```

**trigger触发浏览器事件与自定义事件区别？**

- 自定义事件对象，是jQuery模拟原生实现的
- 自定义事件可以传递参数

## 2、triggerHandler事件

trigger事件还有一个特性：**会在DOM树上冒泡**，所以如果要阻止冒泡就需要在事件处理程序中返回 *false* 或调用事件对象中的 `.stopPropagation()` 方法可以使事件停止冒泡

trigger事件是具有触发原生与自定义能力的，但是存在一个不可避免的问题**： 事件对象event无法完美的实现**，毕竟一个是浏览器给的，一个是自己模拟的。尽管 `.trigger()`  模拟事件对象，但是它并没有完美的复制自然发生的事件，若要触发通过 jQuery 绑定的事件处理函数，而不触发原生的事件，使用 `.triggerHandler()` 来代替。

`triggerHandler` 与 `trigger` 的用法是一样的，重点看不同之处：

- `triggerHandler`不会触发浏览器的默认行为，`.triggerHandler( "submit" )` 将不会调用表单上的 `.submit()`
- `.trigger()`  会影响所有与 jQuery 对象相匹配的元素，而 `.triggerHandler()`  仅影响第一个匹配到的元素
- 使用 `.triggerHandler()`  触发的事件，并不会在 DOM 树中向上冒泡。 如果它们不是由目标元素直接触发的，那么它就不会进行任何处理
- 与普通的方法返回 jQuery 对象(这样就能够使用链式用法)相反，`.triggerHandler()`  返回最后一个处理的事件的返回值。如果没有触发任何事件，会返回 `undefined`



















