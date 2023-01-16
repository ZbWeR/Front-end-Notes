## CSS高级技巧

### [sprite]精灵图

#### 1.背景知识

当用户访问一个网站时，需要向服务器发送请求，网页上的每张图像都要经过一次请求才能展现给用户。一个网页中往往会应用很多小的背景图像作为修饰，当网页中的图像过多时，服务器就会频繁地接受和发送请求，这将大大降低页面的加载速度。

**精灵技术**可以有效地减少服务器接受和发送请求的次数，提高页面的加载速度。

#### 2.技术原理

+ 精灵技术主要针对背景图片使用，就是把多个小背景图片整合到一张大图片中。
+ 利用`background-positi on`实现，移动的距离就是目标图片的x,y(向下为正)坐标。
+ 一般情况下都是向上向左移动，所以数值是负值。使用时需要精确测量小图片的位置。

#### 3.案例时间

参考【精灵图使用】与【拼出名字】

### [iconfont]字体图标

#### 基础知识

使用场景：主要用于显示网页中通用、常用的一些**小巧简单**的图标。 

虽然可以使用精灵图实现，但精灵图的缺点很明显：1.图片文件还是较大；2.图片本身放大缩小会失真；3.一旦图片制作完毕想要更换非常复杂。

于是字体图标应运而生，**iconfont**展示的是图片，本质属于字体，可以设置文本的样式。具体优点如下：

+ 轻量级：字体图标比图像要小，减少了服务器请求。
+ 灵活性：本质是文字，可以随意的改变颜色、阴影、透明效果等等。
+ 兼容性：几乎支持所有的浏览器。

**总结**：结构样式简单的用[iconfont],结构复杂的用[sprite].

#### 使用方法

[icomoon]

1. 将下载包里的`fonts`放入页面根目录下。
2. 复制`style.css`中的字体声明，加入页面css代码中。
3. 在`demo.html`中找到要使用的图标，复制其对应的小方块``。
4. 给要使用图标的类添加样式`font-family=声明的字体名称`。

[iconfont]

使用方法见下载后的`demo_index.html`,有详细的操作讲解。	

### 三角

```css
.div {
    width: 0;
    height: 0;
	/* 为了兼容性 */
    font-size: 0;
    line-height: 0;
    margin: 100px auto;
    /* 两行缺一不可,改变border的大小可以改变三角的形状 */
    border: 100px solid transparent;
    border-top: 100px solid pink;
}
```

### 用户界面

#### 1.鼠标样式[cursor]

设置鼠标悬浮在对象上的光标形状。语法:`cursor: 属性值`

| 属性值      | 描述 |
| ----------- | ---- |
| default     | 默认 |
| pointer     | 小手 |
| move        | 移动 |
| text        | 文本 |
| not-allowed | 禁止 |

```html
<ul>
    <li style="cursor: default;">我是默认样式</li>
    <li style="cursor: pointer;">我是小手样式</li>
    <li style="cursor: move;">我是移动样式</li>
    <li style="cursor: text;">我是文本样式</li>
    <li style="cursor: not-allowed;">我是禁止样式</li>
</ul>
```

#### 2.轮廓线[outline]

最常见也是最直接的写法:`outline: none;`,去除点击后的轮廓线效果。

#### 3.防止拖拽[resize]

禁止文本域[textarea]的拖拽:`resize:none;`

```html
<style>
textarea {
    outline: none;
    resize: none;
}</style>
```

### 垂直对齐

前情提要：

+ 有宽度的块级元素水平居中：`margin:0 auto;`
+ 让文字水平居中,父元素设置:`tetx-align:center`

**[vertival-align]**经常用于设置图片或者表单(行内块元素)和文字垂直对齐，只针对**行内或行内块元素**

| 属性值 | 描述         |
| ------ | ------------ |
| middle | 垂直居中对齐 |
| top    | 顶部对齐     |
| bottom | 底部对齐     |

### 溢出省略

#### 单行文字

```css
/* 强制单行显示 */
white-space: nowrap;
/* 溢出部分隐藏 */
overflow: hidden;
/* 超出部分用省略号替代 */
text-overflow: ellipsis;
```

#### 多行文字(了解)

有较大的兼容性问题，适用于webKit浏览器

```css
div {
     height: 80px;// 高度要设置得合理，或者不设置
    width: 150px;
    background-color: pink;
    /* 一下为模板内容 */
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 4;//设置在第4行出现省略号
    -webkit-box-orient: vertical;
}
```

更推荐让后端来做，可以设置显示多少个字符，操作更简单

### CSS初始化

不同浏览器对有些标签的默认值是不同的，为了消除不同浏览器对HTML文本呈现的差异，照顾浏览器的兼容，我们需要对CSS进行初始化，一下为京东的css初始化代码

```css
/* 把我们所有标签的内外边距清零 */
* {
    margin: 0;
    padding: 0
}

/* em 和 i 斜体的文字不倾斜 */
em,
i {
    font-style: normal
}

/* 去掉li 的小圆点 */
li {
    list-style: none
}

img {
    /* border 0 照顾低版本浏览器 如果 图片外面包含了链接会有边框的问题 */
    border: 0;
    /* 取消图片底侧有空白缝隙的问题 */
    vertical-align: middle
}

button {
    /* 当我们鼠标经过button 按钮的时候，鼠标变成小手 */
    cursor: pointer
}

a {
    color: #666;
    text-decoration: none
}

a:hover {
    color: #c81623
}

button,
input {
    /* "\5B8B\4F53" 就是宋体的意思 这样浏览器兼容性比较好 */
    font-family: Microsoft YaHei, Heiti SC, tahoma, arial, Hiragino Sans GB, "\5B8B\4F53", sans-serif
}

body {
    /* CSS3 抗锯齿形 让文字显示的更加清晰 */
    -webkit-font-smoothing: antialiased;
    background-color: #fff;
    font: 12px/1.5 Microsoft YaHei, Heiti SC, tahoma, arial, Hiragino Sans GB, "\5B8B\4F53", sans-serif;
    color: #666
}

.hide,
.none {
    display: none
}

/* 清除浮动 */
.clearfix:after {
    visibility: hidden;
    clear: both;
    display: block;
    content: ".";
    height: 0
}

.clearfix {
    *zoom: 1
}
```

