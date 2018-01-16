# 第01回：事件添加

语法形式：

```javascript
$ele.event( [eventData ], handler(eventObject) )
```

```javascript
$(".button").click("Hello, jQuery!", function(e) {
  	// ...
  	// this --> .button
  	// e.data --> "Hello, jQuery!"
})
```

# 第02回：事件类型

## 1、鼠标事件

- .click() & .dblclick() ：单击 & 双击事件


- .mousedown()  & .mouseup() ：鼠标按下 & 鼠标抬起（提示：鼠标按下抬起会触发一个点击事件）

- .mousemove() ：鼠标移动事件（只要鼠标移动就会触发该事件，并且会触发多次）

- .mouseover()  & .mouseout() ：鼠标移入 & 鼠标移出

- .mouseenter & .mouseleave() ：鼠标移入 & 鼠标移出（不会冒泡）

- .hover() ：切换事件，类似于css中的hover，

  其语法形式为：*$(selector).hover(handlerIn, handlerOut)* ，在hover方法中传递两个回调函数即可。

## 2、表单事件

- .focusin()  & .focusout() ：失去焦点事件 & 获取焦点事件

- .blur()  & .focus() ：失去焦点 & 获取焦点（不会冒泡）

- .change() ：值改变事件（常用于input、textarea及select）

- .select() ：当 textarea 或文本类型的 input 元素中的文本被选择时，会发生 select 事件。

- .submit() ：表单提交事件（`type="submit/image" || 按Enter键`）

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
  >    return false; //阻止默认行为，提交表单
  > });
  > ```

## 3、键盘事件

- .keydown()  & .keyup() ：键盘按下 & 键盘抬起（当用户在一个元素上第一次按下/抬起键盘上的键的时候，就会触发）

  > 提示：
  >
  > 理论上它可以绑定到任何元素，但keydown/keyup事件只是发送到具有焦点的元素上，不同的浏览器中，可获得焦点的元素略有不同，但是表单元素总是能获取焦点，所以对于此事件类型表单元素是最合适的。

- .keypress() ：长按

## 4、one 事件

让绑定在指定元素上的事件只执行一次的方法。

基本语法如下：

```javascript
$("div").one("click", function(){
    // 这个事件只会触发一次
})
```

## 5、窗口事件

- .resize()：调整窗口大小
- .scroll()：窗口滚动

# 第03回：事件的绑定和解绑

## 1、on() 事件绑定

之前学的鼠标事件，表单事件与键盘事件都有个特点，就是直接给元素绑定一个处理函数，所有这类事件都是属于快捷处理。翻开源码其实可以看到，所有的快捷事件在底层的处理都是通过一个 *.on()* 方法来实现的。jQuery *.on()* 方法是官方推荐的绑定事件的一个方法。

**基本用法**：

```javascript
.on( events ,[ selector ] ,[ data ], fn )
```

最常见的给元素绑定一个点击事件，对比一下快捷方式与on方式的不同：

```javascript
$("#elem").click(function(){})  //快捷方式
$("#elem").on('click',function(){}) //on方式
```

**多个事件绑定同一个函数**

```javascript
$("#elem").on("mouseover mouseout", function(){ });
```

通过空格分离，传递不同的事件名，可以同时绑定多个事件。

**多个事件绑定不同函数**

```javascript
$("#elem").on({
    mouseover:function(){},  
    mouseout:function(){}
});
```

通过逗号分离，传递不同的事件名，可以同时绑定多个事件，每一个事件执行自己的回调方法。

**将数据传递到处理程序**

```javascript
function hello( event ) {
	console.log('Hello, ' + event.data.name);
}
$('#btn').on('click', {name: 'Henrry'}, hello);
// 点击输出：Hello, Henrry
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
        <a>目标节点</a> //点击在这个元素上
    </p>
</div>
```

给出如下代码：

```javascript
$('div').on('click', 'p', function(e) {
	e.target.textContent = 'Hello, world!';
});
```

> 事件绑定在最上层div元素上，当用户触发在a元素上，事件将往上冒泡，一直会冒泡在div元素上。如果提供了第二参数，那么事件在往上冒泡的过程中遇到了选择器匹配的元素，将会触发事件回调函数

## 3、off() 卸载事件

根据on绑定事件的一些特性，off方法也可以通过相应的传递组合的事件名，名字空间，选择器或处理函数来移除绑定在元素上指定的事件处理函数。当有多个过滤参数时，只有与这些参数完全匹配的事件处理函数才会被移除。

绑定两个事件

```javascript
$("elem").on("mousedown mouseup", fn)
```

删除一个事件

```javascript
$("elem").off("mousedown")
```

删除所有事件

```javascript
$("elem").off("mousedown mouseup")
```

快捷方式删除所有事件，这里不需要传递事件名了，节点上绑定的所有事件将全部销毁

```javascript
$("elem").off()
```

# 第04回：事件对象

## 1、事件对象的使用

事件中的Event对象容易被初学者忽略掉，可能大多时候初学者不知道怎么去用它，但有些时候它还是非常有用的。

一个标准的 *click* 事件：

```javascript
$(elem).on("click",function(event){
   event //事件对象
})
```

在不同浏览器之间事件对象的获取, 以及事件对象的属性都有差异。jQuery根据 W3C 标准规范了事件对象，所以在jQuery事件回调方法中获取到的事件对象是经过兼容后处理过的一个标准的跨浏览器对象

这里不在千篇一律的说方法的使用，通过实际的一个小案例，从而来了解事件对象的作用

```html
<ul>
    <li class="even1"></li>
    <li class="even2"></li>
    <li class="even2"></li>
    .........
</ul>
```

ul有N个子元素li(这里只写了3个)，如果我要响应每一个li的事件，那么常规的方法就是需要给所有的li都单独绑定一个事件监听，这样写法很符合逻辑，但是同时有显得繁琐。

因为li都有一个共同的父元素，而且所有的事件都是一致的，这里我们可以采用要一个技巧来处理，也是常说的"事件委托"。

事件没直接和li元素发生关系，而且绑定父元素了。由于浏览器有事件冒泡的这个特性，我们可以在触发li的时候把这个事件往上冒泡到ul上，因为ul上绑定事件响应所以就能够触发这个动作了。唯一的问题怎么才知道触发的li元素是哪个一个？

这里就引出了事件对象：

> ```
> 事件对象是用来记录一些事件发生时的相关信息的对象。事件对象只有事件发生时才会产生，并且只能是事件处理函数内部访问，在所有事件处理函数运行结束后，事件对象就被销毁
> ```

回到上面的问题，既然事件对象是跟当前触发元素息息相关的，所以我们就能从里面相关的信息，从事件对象中找到 event.target

target 属性可以是注册事件时的元素，或者它的子元素。通常用于比较 event.target 和 this 来确定事件是不是由于冒泡而触发的。经常用于事件冒泡时处理事件委托

简单来说：

> `event.target` 代表当前触发事件的元素，可以通过当前元素对象的一系列属性来判断是不是我们想要的元素。

## 2、事件对象的属性和方法

- event.type：

  获取事件的类型

- event.pageX & event.pageY：

  获取鼠标当前相对于页面的坐标

- event.preventDefault() ：

  阻止默认行为

  这个用的特别多，在执行这个方法后，如果点击一个链接（a标签），浏览器不会跳转到新的 URL 去了。我们可以用 *event.isDefaultPrevented()*  来确定这个方法是否(在那个事件对象上)被调用过了

- event.stopPropagation() ：

  阻止事件冒泡

  事件是可以冒泡的，为防止事件冒泡到DOM树上，也就是不触发的任何前辈元素上的事件处理函数

- event.which：

  获取在鼠标单击时，单击的是鼠标的哪个键

  event.which 将 event.keyCode 和 event.charCode 标准化了。event.which也将正常化的按钮按下(mousedown 和 mouseupevents)，左键报告1，中间键报告2，右键报告3

- event.currentTarget : 

  在事件冒泡过程中的当前DOM元素

  冒泡前的当前触发事件的DOM对象, 等同于this.

> 提示：

**1. this 和 event.target 的区别：**

> js 中事件是会冒泡的，所以  event.target  是可以变化的，但 this 不会变化，它永远是直接接受事件的目标DOM元素；

**2. this 和 event.target 都是 dom 对象**

> 如果要使用 jquey 中的方法可以将他们转换为jquery对象。比如 this 和 $(this) 的使用、event.target和$(event.target)的使用；

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

trigger事件还有一个特性：**会在DOM树上冒泡**，所以如果要阻止冒泡就需要在事件处理程序中返回 *false* 或调用事件对象中的 *.stopPropagation()* 方法可以使事件停止冒泡

trigger事件是具有触发原生与自定义能力的，但是存在一个不可避免的问题**： 事件对象event无法完美的实现**，毕竟一个是浏览器给的，一个是自己模拟的。尽管 *.trigger()*  模拟事件对象，但是它并没有完美的复制自然发生的事件，若要触发通过 jQuery 绑定的事件处理函数，而不触发原生的事件，使用 *.triggerHandler()* 来代替

triggerHandler与trigger的用法是一样的，重点看不同之处：

- triggerHandler不会触发浏览器的默认行为，*.triggerHandler( "submit" )* 将不会调用表单上的 *.submit()*
- *.trigger()*  会影响所有与 jQuery 对象相匹配的元素，而 *.triggerHandler()*  仅影响第一个匹配到的元素
- 使用 *.triggerHandler()*  触发的事件，并不会在 DOM 树中向上冒泡。 如果它们不是由目标元素直接触发的，那么它就不会进行任何处理
- 与普通的方法返回 jQuery 对象(这样就能够使用链式用法)相反，*.triggerHandler()*  返回最后一个处理的事件的返回值。如果没有触发任何事件，会返回 *undefined*



















