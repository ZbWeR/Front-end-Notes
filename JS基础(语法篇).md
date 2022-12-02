## JS基础(语法篇)

### 书写位置

#### 1.行内式

`<input type="button" value="唐伯虎" onclick="alert('点秋香')">`

+ 可以将单行或少量JS代码写在HTML标签的事件属性中(以on开头),例如：onclick.
+ 注意单双引号的使用，HTML中推荐使用双引号，JS中推荐使用**单引号**.
+ 可读性差，引号嵌套易混淆，不建议大量使用。

#### 2.嵌入式

类似于CSS,在head标签中插入`script`即可。（学习时最常用的方式）

```html
<script>
     alert('童话镇');
</script>
```

#### 3.外部引用

`<script src="my.js"></script>`

+ 外部引用时script标签的中间不可以写代码
+ 适用于JS代码量较大的情况，方便模块化编程。

### 输入输出

| 方法             | 说明                           |
| ---------------- | ------------------------------ |
| alert(msg)       | 浏览器弹出警示框               |
| console.log(msg) | 浏览器控制台打印输出信息       |
| prompt(info)     | 浏览器弹出输入框，用户可以输入 |

### 变量

```javascript
// 定义变量并赋值
var age = 18, name = 'zbwer';
// 输出变量
console.log('年龄为:' + age, name);
// + 拼接输出 或用 逗号隔开
```

定义变量的关键字`var`

### Array对象

#### 1.初始化与遍历

```js
var Arr = [32, 180, 47, 49];
for (let i = 0, n = Arr.length; i < n; i++)
    Arr[i] += 1;
```

#### 2.对象方法

+ `push`：在数组后面添加一个或多个元素，并返回新的长度。
+ `pop`:删除数组的最后一个元素，并返回元素的值.(原数组为空返回undefined)

```javascript
var Arr = [1, 3, 5, 9, 2];
console.log(Arr.push(321)); // 6
console.log(Arr);			// [1,3,5,9,2,321]
console.log(Arr.pop());		//321
Arr.push(23, 45);
console.log(Arr);			//[1,3,5,9,2,23,45]
```

+ `unshift`:向数组的头部添加一个或多个元素，返回新的长度。
+ `shift`:删除并返回数组的第一个元素。

```javascript
var Arr = [1, 3, 5, 9, 2];
console.log(Arr.unshift(0)); //6
console.log(Arr);			 //[0,1,3,5,9,2]
console.log(Arr.shift());	 //0
```

+ `reverse`:颠倒数组中元素的顺序。
+ `concat`:链接两个或多个数组。

```javascript
var Arr = [1, 3, 5, 9, 2], B = [2, 5, 6];
console.log(Arr.reverse());  // [2,9,5,3,1]
console.log(Arr.concat(B));  // [2,9,5,3,1,2,5,6]
```

+ `sort`:对数组元素进行排序(默认按照ASCII从小到大)

```javascript
var Arr = [10, 5, 1000, 25, 1];
console.log(Arr.sort());	// [1,10,1000,25,5]
Arr.sort((a, b) => {
    return a - b;	//升序
});
console.log(Arr);			// [1,5,10,25,1000]
```

+ `join()`:把所有元素放进一个字符串当中，并通过指定的分隔符分隔。(默认为逗号)

```js
var Arr = ['zbwer', 'is', 'handsome'];
var A_to_string = Arr.join('*');	
console.log(A_to_string);	//zbwer*is*handsome
console.log(Arr);			//不改变原数组
```

更多方法参考:[JavaScript Array 对象 | 菜鸟教程 (runoob.com)](https://www.runoob.com/jsref/jsref-obj-array.html)

### 数据类型

**值类型**:字符串(String),数字(Number),布尔(Boolean),空(null),未定义(Undefined）,Symbol。

**引用数据类型（对象类型）**：对象(Object),数组(Array),函数(Function),还有两个特殊的对象：正则（RegExp）和日期（Date）。
