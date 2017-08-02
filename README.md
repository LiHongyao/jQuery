# 一、jQuery 简介

  jQuery是一套跨浏览器的[JavaScript库](http://baike.sogou.com/lemma/ShowInnerLink.htm?lemmaId=1023011&ss_c=ssc.citiao.link)，简化HTML与JavaScript之间的操作。它是[轻量级](http://baike.sogou.com/lemma/ShowInnerLink.htm?lemmaId=7988600&ss_c=ssc.citiao.link)的js库 ，兼容[CSS3](http://baike.sogou.com/lemma/ShowInnerLink.htm?lemmaId=40562&ss_c=ssc.citiao.link)，还兼容各种浏览器，jQuery2.0及后续版本不再支持[IE6](http://baike.sogou.com/lemma/ShowInnerLink.htm?lemmaId=4794817&ss_c=ssc.citiao.link)/7/8浏览器。由John Resig在2006年1月的BarCamp NYC上发布第一个版本。目前是由 Dave Methvin 领导的开发团队进行开发。jQuery使用户能更方便地处理HTML documents、events、实现动画效果，并且方便地为网站提供AJAX交互。jQuery还有一个比较大的优势是，它的文档说明很全，而且各种应用也说得很详细，同时还有许多成熟的插件可供选择。jQuery能够使用户的html页面保持代码和html内容分离，也就是说，不用再在html里面插入一堆js来调用命令了，只需定义id即可。

# 二、jQuery 相关特点

  jQuery包含以下特点：

- 动态特效
- ajax
- 通过插件来扩展
- 方便的工具 - 例如浏览器版本判断
- 渐进增强
- 链式调用
- 多浏览器支持，支持Internet Explorer6.0+、Opera9.0+、Firefox2+、Safari2.0+、Chrome1.0+（在2.0.0中取消了对Internet Explorer6,7,8的支持）

# 三、jQuery 优势

  jQuery的座右铭是 “写得少，干得多”，因为和传统的JavaScript相比，jQuery使得只需要使用更少的代码就可以完成同样的功能。jQuery具备以下优势：

- 简单的选择器/DOM操作
- 简化代码
- 跨浏览器兼容性

# 四、jQuery 版本选择

  在jQuery的开发过程中，创建了大量的代码来支持IE6、7、8，从而使得脚本更大也更加复杂。因此当研发2.0版本的jQuery时，研发团队决定这个版本放弃对早期浏览器的支持，以便创建更小、更快的脚本。

  不过，jQuery团队也考虑到，在网上仍然有很多用户使用这些早期的浏览器，因此开发者仍然需要去支持这些用户。出于这样的原因，他们保留了两个并行的jQuery版本：

  `jQuery 1.9+`：包含和2.0x同样的功能，不过依然支持IE6、7、8。

  `jQuery 2.0+`：放弃支持早期浏览器，使得脚本更小、更快。

  这两个版本的功能在短期之内应该不会产生重要的区别。jQuery文件名中应该包含其版本号（比如，jquery-3.2.1.min.js 或 jquery-3.2.1.js）。如果不这样做的话，用户的浏览器可能会缓存更新或更旧版本的文件，从而可能导致脚本运行不正常。

# 五、jQuery 引入方式

## 1、在线引用

### 1）、国外CDN

- Google Hosted Libraries

  src="[http://ajax.googleapis.com/ajax/libs/jquery/2.1.1/jquery.min.js](http://ajax.googleapis.com/ajax/libs/jquery/2.1.1/jquery.min.js)"


- Microsoft CDN

  src="[http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js](http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js)"

- jQuery官网

   src="[http://code.jquery.com/jquery-1.11.0.min.js](http://code.jquery.com/jquery-1.11.0.min.js)"

### 2）、国内CDN

- 百度

  src="[http://libs.baidu.com/jquery/2.0.0/jquery.min.js](http://libs.baidu.com/jquery/2.0.0/jquery.min.js)"

- 新浪

  src="[http://lib.sinaapp.com/js/jquery/1.6/jquery.min.js](http://lib.sinaapp.com/js/jquery/1.6/jquery.min.js)"

## 2、本地引用

  点击前往 [jQuery 下载](http://jquery.com/download/)，选择第一项 *Download the compressed, production jQuery 3.2.1*，保存到项目之后，直接引用这个文件即可。

> tips：最常用的jQuery基础方法是：`.ready()方法`
>
> ```javascript
> $(document).ready(function(){
> 	// insert javscript code here...
> });
> ```
>
> 或者其简写：
>
> ```javascript
> $(function(){
> 	// insert JavaScript code here...
> });
> ```
>
> 该方法的作用是文档就绪执行，当DOM加载完就可以执行（比 *window.onload* 更早）。在同一个页面里可以多次出现 `.ready()`。

# 六、jQuery/DOM 对象转换

  jQuery 对象是通过 jQuery 包装DOM 对象后产生的对象。jQuery 对象是 jQuery 独有的，其可以使用 jQuery 里的方法，但是不能使用 DOM 的方法；例如：` $("#img").attr("src","test.jpg"); ` 这里的 `$("#img")` 就是 jQuery 对象。

  DOM 对象就是Javascript 固有的一些对象操作。DOM 对象能使用Javascript 固有的方法，但是不能使用 jQuery 里的方法。例如：`document.getElementById("img").src = “test.jpg";`  这里的 `document.getElementById("img") ;`  就是DOM 对象。

  `$("#img").attr("src","test.jpg"); ` 和 `document.getElementById("img").src = "test.jpg";`  是等价的，是正确的，但是` $("#img").src = "test.jpg" ;` 或者 `document.getElementById("img").attr("src","test.jpg");`  都是错误的。

  再说一个例子，就是 `this` , 在写 jQuery 时经常这样写：` this.attr("src","test.jpg")；`可是就是出错，其实 `this` 是DOM对象，而 `.attr("src","test.jpg") ` 是 jQuery 方法，所以出错了。要解决这个问题就要将 DOM对象转换成 jQuery 对象，例如 `$(this).attr("src","test.jpg");`

## 1、DOM 对象转成 jQuery 对象

  对于已经是一个 DOM 对象，只需要用 `$()` 把DOM对象包装起来，就可以获得一个 jQuery 对象了，$(DOM 对象)。

```javascript
let domObj    = document.getElementById('img');
let jqueryObj = $(domObj);
```

  转换后，就可以任意使用 jQuery 的方法。

## 2、jQuery 对象转成 DOM 对象

  将 jQuery 对象转换为 DOM 对象的方式主要有两种：[index] 和 .get(index)；

- jQuery 对象是一个数据对象，可以通过 [index] 的方法，来得到相应的 DOM 对象：

```javascript
// jQuery 对象
let $div = $('#div'); 
// DOM 对象
let div  = $div[0];
```

- jQuery 本身提供，通过.get(index) 方法得到相应的 DOM 对象：

```javascript
// jQuery 对象
let $div = $('#div'); 
// DOM 对象
let div  = $div.get(0);
```

  通过以上方法，可以任意的相互转换 jQuery 对象和 DOM 对象，需要再强调的是： DOM 对象才能使用DOM 中的方法，jQuery 对象是不可以使用DOM中的方法。

# 七、jquery 方法扩展

```javascript
// 为 $.windowbox 添加新的方法
$.windowbox = {
	// 定义一个方法
	sayHello: function() {
		console.log(`Hello, world!`);
	}
}

// 调用 $.windowbox 里的 sayHello 方法
$.windowbox.sayHello()
// "Hello, world!"
```



