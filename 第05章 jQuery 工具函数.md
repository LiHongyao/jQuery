# 数组和对象操作

## 1. `$.each()`

通用遍历方法，可用于遍历对象和数组。

不同于遍历 jQuery 对象的 `$().each()` 方法，此方法可用于遍历任何对象。回调函数拥有两个参数：第一个为对象的成员或数组的索引，第二个为对应变量或内容。如果需要退出 each 循环可使回调函数返回 false，其它返回值将被忽略。

```js
// 1.遍历数组
$.each(['A', 'B', 'C'], function (index, val) { 
        console.log(`下标：${index}，值：${val}`);
});
/*
下标：0，值：A
下标：1，值：B
下标：2，值：C*/

// 2.遍历对象
$.each({name:'Henry', age: 28}, function (key, val) { 
    console.log(`键：${key}，值：${val}`);
});
/*
键：name，值：Henry
键：age， 值：28*/
```

## 2. `$.extend()`

用一个或多个其他对象来扩展一个对象，返回被扩展的对象。

```js
function tool(options) {
    // 默认配置
    let configs = {
        duration: 1000,
        interval: 15
    };
    // 修改默认配置
    $.extend(configs, options);
    console.log(configs); // {duration: 2000, interval: 15, color: "green"}
}
tool({
    duration: 2000,
    color: 'green'
});
```

## 3. `$.grep()`

过滤数组元素

```js
resArr = $.grep([1, 2, 3, 4], (num, index) => {
    return num % 2 == 0;
});
console.log(resArr); // [2, 4]
```



