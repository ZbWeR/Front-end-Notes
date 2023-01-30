## Jquery学习笔记

### 基本使用

#### $ 符号

`$`是`Jquery`的别称,同时也是Jquery中的顶级对象.

```js
$('div').hide() 等价于 Jquery('div').hide()
```

#### jquery对象

jquery对象是指采用 jquery 方式获得的对象,本质是使用`$`包装 DOM 对象,采用伪数组的方式存储.

jquery对象只能使用 jquery 方法,而 DOM 对象只能使用原生 js 方法.

对象转化:

	1. DOM转jq: `$(DOM对象名)`
	1. jq转DOM: `$('div')[index]`其中index是数组下标

例如:

```js
myDiv = document.querySelector('div');
// 采用 $(DOM对象) 的方式可以把dom对象转换成jquery对象
$(myDiv).hide();
// jquery对象相当于数组存储的DOM对象
// 所以可以采用数组的方式来调用,以达到把jquery对象转为DOM对象的目的.
$('div')[0].style.display = 'none';
$('div').get(0).style.backgroundColor = 'red';
```

### 选择器

`$('选择器')$` 括号内直接写CSS选择器即可，要记得加引号.

隐式迭代就是把匹配的所有元素内部进行遍历循环,给每一个元素执行相同的方法,而不用我们进行循环,简化操作.

#### 筛选选择器

| 语法          | 用法                | 描述                                         |
| ------------- | ------------------- | -------------------------------------------- |
| :first        | `$('li:first')`     | 获取第一个li元素                             |
| :last         | `$('li:last')`      | 获取最后一个li元素                           |
| :eq(index)    | `$('li:eq(index)')` | 获取索引号为index的li元素,index从0开始       |
| :odd 或 :even | `$('li:odd')`       | 获取索引号为奇数或者偶数的元素，注意是索引号 |

#### 筛选方法

| 用法                    | 描述                                 |
| ----------------------- | ------------------------------------ |
| `$('li').parent()`      | 返回最近一级的父元素                 |
| `$('li').children('a')` | 返回最近一级的子元素(直接后代)       |
| `$('li').find('a')`     | 返回所有符合条件的子元素(所有后代)   |
| `$('li').siblings()`    | 返回除自己外的其他兄弟元素           |
| `$('li').eq(index)`     | 选择索引号为index的元素,index从0开始 |

+ 两个`eq`筛选方式的区别:

  ```js
  判断当前元素是否具有某个类名 hasClass('className')
  $('ul li').eq(2).hasClass('item');
  $('li:eq(2)').hasClass('item');
  ```

  从功能上来看没有任何区别,从便捷性上来看筛选方法更加常用，因为其`index`可以使用变量来直接替代.

#### 排他思想

需求: 在多个按钮中点击其中一个时,被点击的按钮颜色发生改变，而其他按钮保持未点击状态.

解决方案：利用jQuery隐式迭代的特性和`siblings`方法.

```js
$('button').click(function () {
    $(this).css('background-color', 'pink');
    $(this).siblings().css('background-color', '');
})
```

#### 链式编程

节约代码量，让代码看起来更优雅.

```js
$(this).css('background-color', 'pink');
$(this).siblings().css('background-color', '');
// 链式编程： 等价于上述语句
$(this).css('background-color', 'pink').siblings().css('background-color', '');
// 我的css样式为xxx,我的兄弟css样式为xxx
```

使用链式编程一定要注意对象主体是谁.

### 样式操作

#### CSS方法

jQuery可以通过`CSS`方法来修改简单元素样式.

1. 参数只写属性名,则返回属性值.

   ```js
   $(".box").css("width"); // 返回 200px
   ```

2. 参数为==属性名,属性值==.两者之间用`,`逗号分割，且属性名和属性值都应加引号.

   ```js
   $(".box").css("width", "400px");
   $(".box").css("color", "pink");
   ```

3. 同时修改多个样式,采用大括号的对象形式. (不推荐)

   ```js
   let red = "green";
   $(".box").css({
       width: "400px",
       height: "400px",
       backgroundColor: red,
       marginTop: "200px",
       "font-size": "20px"
   });
   ```

+ 不同样式之间采用`,`逗号间隔,最后一个样式不需要加末尾符号.
+ 如果属性名不加引号,则需采用驼峰命名法来处理复合属性,例如`backgroundColor`.如果加了引号,则采用css的方式书写.
+ 属性值一般需要加引号,不加引号会被解析为js中的变量,上述代码中的 red 就是一个示例.
+ 属性值为数字时可以不加引号,但不推荐这种做法.

#### 与类相关的方法

1. 添加类名: `addClass("className")`

```js
$("div").addClass("current");
```

2. 删除类名: `removeClass("className")`

```js
$("div").removeClass("box");
```

3. 切换类名: `toggleClass("className")`:如果有`className`这个类就移出,没有这个类就添加,实现类似开关的切换效果.

```js
$("div").toggleClass("spin");
```

### 效果

#### 显示隐藏切换

1. 显示语法规范: `show([speed],[easing],[fn])`

+ 不写任何参数,则无动画直接显示.

| 参数             | 说明                                             |
| ---------------- | ------------------------------------------------ |
| speed            | 表示动画的持续毫秒数                             |
| easing(几乎不用) | 表示动画切换的效果,默认为慢快慢,可选参数"linear" |
| fn               | 回调函数,表示动画结束后调用的函数                |

2. 隐藏语法规范:`hide([speed],[easing],[fn])`

3. 切换语法规范:`toggle([speed],[easing],[fn])`

代码示例:

```js
$('div').toggle(1000, "linear", function () {
    console.log("toggle success");
});// 动画以线性方式执行1000毫秒,结束后打印提示字符串.
```

