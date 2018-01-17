# 第01回：隐藏、显示

## 1、.hide()

隐藏元素，其语法形式为：

```javascript
.hide([speed,[easing],[fn]])
```

> 参数解读：

- **speed**：三种预定速度之一的字符串("slow","normal", or "fast")或表示动画时长的毫秒数值(如：1000)
- **easing**：(Optional) 用来指定切换效果，默认是"swing"，可用参数"linear"
- **fn**：在动画完成时执行的函数，每个元素执行一次。

> 提示：元素隐藏之后会脱离文档流

## 2、.show()

显示元素，其语法形式为：

```javascript
.show([speed,[easing],[fn]])
```

> 注意：
>
> 1. *.show()(* 与 *.hide()* 方法是修改的display属性。
> 2. 如果使用 *“!important”* 在你的样式中，比如 *display: none !important*，如果你希望 *.show()* 方法正常工作，必须使用 *.css('display', 'block !important')* 重写样式。
> 3. 如果让show与hide成为一个动画，那么默认执行动画会改变元素的高度，高度，透明度。

## 3、.toggle()

show与hide是一对互斥的方法。需要对元素进行显示隐藏的互斥切换，通常情况是需要先判断元素的display状态，然后调用其对应的处理方法。比如显示的元素，那么就要调用hide，反之亦然。 对于这样的操作行为，jQuery提供了一个便捷方法 *.toggle()* 用于切换显示或隐藏匹配元素。

语法形式如下：

```javascript
.toggle([speed,[easing],[fn]])
```

# 第02回：上卷、下拉

## 1、.slideDown()

对于隐藏的元素，在将其显示出来的过程中，可以对其进行一些变化的动画效果。之前学过了show方法，show方法在显示的过程中也可以有动画，但是 *.show()* 方法将会匹配元素的宽度，高度，以及不透明度，同时进行动画操作。这里将要学习一个新的显示方法 *.slideDown()* 方法。

**.slideDown()：用滑动动画显示一个匹配元素**

.slideDown() 方法将给匹配元素的高度的动画，这会导致页面的下面部分滑下去，弥补了显示的方式。其语法形式为：

```javascript
.slideDown([speed,[easing],[fn]])
```

> 注意：
>
> 1. 下拉动画是从无到有，所以一开始元素是需要先隐藏起来的，可以设置 *display:none*。
> 2. 如果提供回调函数参数，callback 会在动画完成的时候调用。将不同的动画串联在一起按顺序排列执行是非常有用的。这个回调函数不设置任何参数，但是 this会设成将要执行动画的那个DOM元素，如果多个元素一起做动画效果，那么要非常注意，回调函数会在每一个元素执行完动画后都执行一次，而不是这组 动画整体才执行一次

## 2、.slideUp()

对于显示的元素，在将其隐藏的过程中，可以对其进行一些变化的动画效果。之前学过了hide方法，hide方法在显示的过程中也可以有动画，但 是.hide()方法将为匹配元素的宽度，高度，以及不透明度，同时进行动画操作。这里将要学习一个新的显示方法slideUp方法。

其语法形式为：

```javascript
.slideUp( [speed ] [, easing ] [, complete ] )
```

这个使用的含义就是：找到元素的高度，然后采用一个下滑动画让元素一直滑到隐藏，当高度为0的时候，也就是不可见的时，修改元素display 样式属性被设置为none。这样就能确保这个元素不会影响页面布局了。

## 3、.slideToggle()

slideDown与slideUp是一对相反的方法。需要对元素进行上下拉卷效果的切换，jQuery提供了一个便捷方法slideToggle用滑动动画显示或隐藏一个匹配元素。其语法形式为：

```
.slideToggle( [speed ] [, easing ] [, complete ] )
```

> 注意：
>
> 1. display属性值保存在jQuery的数据缓存中，所以display可以方便以后可以恢复到其初始值
> 2. 当一个隐藏动画后，高度值达到0的时候，display 样式属性被设置为none，以确保该元素不再影响页面布局

# 第03回：淡入、淡出

除了通过 *display* 设置元素的显示与隐藏，还有一种方法就是设置元素的不透明度（`opacity`），值范围为` 0~1` ，当不透明度为1时，元素显示，当不透明度为0时，元素隐藏。jQuery淡入淡出效果正是使用了这个原理。只不过，当不透明度为0时，元素虽然隐藏了，但是并没有脱离文档流，但是jQuery中，元素淡出会脱离文档流。

## 1、.fadeIn()

```javascript
.fadeIn( [speed ] [, easing ] [, complete ] )
```

## 2、.fadeOut()

```javascript
.fadeOut( [speed ] [, easing ] [, complete ] )
```

## 3、.fadeToggle()

```javascript
.fadeToggle( [speed ] [, easing ] [, complete ] )
```

## 4、.fadeTo()

```javascript
.fadefadeToToggle( speed , opacity , [, easing ] [, complete ] )
```

# 第04回：自定义动画

## 1、.animate()

jQuery 提供的动画有限，有时需要我们实现一些更为复杂的动画效果，这时我们就需要使用自定义动画了。当然，jQuery也为我们提供了自定义动画的接口，其语法形式如下：

```javascript
.animate( prop ,[ speed ], [ easing ], [ complete ] )
.animate( prop, options )
```

**参数解读**

- properties：一个或多个css属性的键值对所构成的Object对象，对 **数字属性值** 有效，驼峰命名，可使用快捷方式如‘show/toggle’。
- speed：持续时间，单位ms，提供 'fast' 和 'slow' 字符串，分别表示持续时间为200 和 600毫秒。
- easing：动画运动算法，jQuery库中默认调用 swing。如果需要其他的动画算法，请查找相关的插件
- complete：回调函数

```javascript
$(".box").click(function () {
   $(this).animate({
       left: "+=50px"
   },1000, function () {
     alert("动画执行完毕！");
   })
});
```

animate 在执行动画中，如果需要观察动画的一些执行情况，或者在动画进行中的某一时刻进行一些其他处理，我们可以通过animate提供的第二种设置语法，传递一个对象参数，可以拿到动画执行状态一些通知。

```javascript
.animate( prop, options )
```

**options参数：**

- duration：设置动画执行的时间
- easing ：规定要使用的 easing 函数，过渡使用哪种缓动函数
- step：规定每个动画的每一步完成之后要执行的函数
- progress：每一次动画调用的时候会执行这个回调，就是一个进度的概念
- complete：动画完成回调
- queue：布尔值。指示是否在效果队列中放置动画。如果为 false，则动画将立即开始

```javascript
$(".box").click(function () {
   $(this).animate({
       left: "+=50px"
   }, {
       duration: 1000,
       complete: function () {
           alert("动画执行完毕！");
       }
   })
});
```

> 同步动画：

动画同时执行，如下所示：

```javascript
$(".box").click(function () {
   $(this).animate({
       width: "50px",
       height: "50px",
       left: "800px",
       opacity: ".5",
   },1000, function () {
     alert("动画执行完毕！");
   })
});
```

> 队列动画

根据动画添加的先后顺序执行动画。

示例1：

```javascript
$(".box").click(function () {
    $(this).animate({width: "50px", height: "50px"}, function () {
        $(this).animate({left: "800px"}, function () {
            $(this).animate({opacity: ".5"}, function () {
                alert("动画执行完毕！");
            })
        })
    });
});
```

示例2：

```javascript
$(".box").click(function () {
    $(this)
        .animate({width  : "50px"}, 1000)
        .animate({height : "50px"}, 1000)
        .animate({opacity: ".5"}, 1000);
});
```

## 2、.queue()

animate 只对数字值的变化有效，如果想要将其他变化（比如颜色变化）加入到动画队列中，可使用 *.queue()* 方法，不过你需要指定 *next* 函数参数并调用，当其他变化执行之后手动执行后续动画队列。

```javascript

$(".box").click(function () {
    $(this)
        .animate({width  : "100px"}, 1000)
        .animate({height : "100px"}, 1000)
        .animate({opacity: ".5"}, 500)
        .queue(function (next) {
            // next -> 函数
            $(this).css({
                background: "blue"
            });
            next();
        })
        .slideUp(1000);
});
```

## 3、.dequeue()

*.queue()* 是 jQuery 1.4版本以后才出现的，而之前我们普遍使用的是 *.dequeue()* 方法。意思为执行下一个元素列队中的函数。 现在对上述代码进行修改，如下所示：

```javascript
$(".box").click(function () {
    $(this)
        .animate({width  : "100px"}, 1000)
        .animate({height : "100px"}, 1000)
        .animate({opacity: ".5"}, 500)
        .queue(function () {
            // next -> 函数
            $(this).css({
                background: "blue"
            });
            $(this).dequeue();
        })
        .slideUp(1000);
});
```

## 4、.clearQueue()

jQuery 还提供了一个清理列队的功能方法：*.clearQueue()*。

假如我想在执行完第二个动画就不再执行了。那么只要在第二个动画的回调函数那里添加一句 *$(this).clearQueue()* 就可以停止后面的列队动画了。

```javascript
$(".box").click(function () {
    $(this)
        .animate({width  : "100px"}, 1000)
        .animate({height : "100px"}, 1000)
        .animate({opacity: ".5"}, 500, function(){$(this).clearQueue();/* 清理队列*/})
        .queue(function () {
            // next -> 函数
            $(this).css({
                background: "blue"
            });
            $(this).dequeue();
        })
        .slideUp(1000);
});
```

 获取队列长度：

```javascript
function getQueueCount() {
    //获取当前列队的长度，fx 是默认列队的参数
    return $(".box").queue("fx").length;
}
```

## 5、.stop()

动画在执行过程中是允许被暂停的，当一个元素调用 *.stop()* 方法，当前正在运行的动画（如果有的话）立即停止。

语法形式：

```
.stop( [clearQueue ], [ jumpToEnd ] )
```

该方法的可选参数，简单来说可以有3种情况：

- **.stop()**： 停止当前动画，迅速执行后续动画效果。
- **.stop(true)**：停止当前动画，清除后续动画队列。
- **.stop(true,true)**：当前动画将停止，但该元素上的 CSS 属性会被立刻修改成动画的目标值

简单的说：参考下面代码、

```javascript
$("#box").animate({
    height: 300
}, 5000)
$("#box").animate({
    width: 300
}, 3000)
$("#box").animate({
    opacity: 0.6
}, 2000)
```

1. stop()：只会停止第一个动画，第二个第三个继续
2. stop(true)：停止第一个、第二个和第三个动画
3. stop(true ture)：停止动画，直接跳到第一个动画的最终状态 

## 6、.delay()

设置一个延时来推迟执行队列中之后的项目。

用于将队列中的函数延时执行。他既可以推迟动画队列的执行，也可以用于自定义队列。

语法形式：

```
.delay(duration, [queueName]);
```

> 参数解读：

**duration**：延时时间，单位：毫秒

**queueName**：队列名词，默认是Fx，动画队列。

> 代码示例：

```javascript
$('#foo').slideUp(300).delay(800).fadeIn(400);
```

## 7、.finish()

停止当前正在运行的动画，删除所有排队的动画，并完成匹配元素所有的动画。

当 *.finish()* 在一个元素上被调用，立即停止当前正在运行的动画和所有排队的动画（如果有的话），并且他们的CSS属性设置为它们的目标值（所有动画的目标值）。所有排队的动画将被删除。

如果第一个参数提供，该字符串表示的队列中的动画将被停止。

*.finish()* 方法和 *.stop(true, true)* 很相似，*.stop(true, true)* 将清除队列，并且目前的动画跳转到其最终值。但是，不同的是，*.finish()* 会导致所有排队的动画的CSS属性跳转到他们的最终值。

## 8、jQuery.fx.off

关闭页面上所有的动画。

把这个属性设置为 `true` 可以立即关闭所有动画(所有效果会立即执行完毕)。有些情况下可能需要这样，比如：

\* 你在配置比较低的电脑上使用jQuery。

\* 你的一些用户由于动画效果而遇到了 [可访问性问题](http://www.jdeegan.phlegethon.org/turn_off_animation.html)

当把这个属性设成 `false` 之后，可以重新开启所有动画。

## 9、jQuery.fx.interval

设置jQuery动画每隔多少毫秒绘制一帧图像 (默认为13 毫秒) 数字越小越流畅，但可能影响浏览器性能。















