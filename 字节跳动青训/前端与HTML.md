## 前端与HTML | 青训营笔记

这是我参与「第五届青训营 」伴学笔记创作活动的第 1 天

### 一、本堂课重点内容：

1. 什么是前端？什么是HTML？
2. HTML的基本语法.
2. HTML中的常见标签.
2. HTML语义化的理解.

### 二、详细知识点介绍：

#### 1.前端与HTML

什么是前端？前端是使用前端技术栈解决多端人机交互功能的工程师.

什么是HTML? 即 HyperText Markup Language,超文本标记语言.

#### 2.HTML的基本语法

+ 标签和属性不区分大小写,但是推荐**原生标签用小写**,自定义组件的标签用大写.
+ 空标签可以不闭合,比如 input, img, meta 等等
+ 属性值推荐使用**双引号**包含,某些属性值可以省略,例如required(属性值默认为Ture)

#### 3.HTML常见标签

+ 标题标签: `<h1></h1>`到`<h6></h6>`字体大小逐渐变小.
+ 列表标签: 有序`<ol>`,无序`<ul>`,自定义`<dl><dt><dd>`
+ 链接标签: `<a>`超链接,属性值`href`代表跳转的地址,`target`设置当前页面打开还是新建页面打开.
+ 多媒体标签: `<img>,<audio>,<video>`,属性值`src`资源路径,`alt`替代性文本,加载失败或不被加载时显示,`controls`显示播放控件.
+ 文本类标签: 短引用:`<q>`具体内容,`<cite>`章节或标题.长引用:`<blockquote>`.单行代码`<code>`,多行代码`<pre><code></code></pre>`.斜体`<em>`,粗体`<strong>`
+ 页面划分标签: `header,nav`放导航相关的内容,`main,artical`放主体内容,`aside`放广告或相关推荐,`footer`放版权本案信息.
+ input标签: 种类繁多,详情见*实践练习例子部分*.

#### 4.HTML语义化

简短概括：**传达内容而非传达样式**

是什么？ 

+ HTML中的元素、属性及属性值都拥有某些含义. 
+ 开发者应该遵循语义来编写HTML,例如有序用`ol`无需用`ul`等等

为什么？

+ 利于开发者修改维护页面 
+ 利于搜索引擎SEO优化 
+ 利于提升网页的无障碍性

怎么做？

+ 了解每个标签和属性的含义 
+ 思考什么标签最适合 
+ 不使用可视化工具自动生成代码

### 三、实践练习例子：

此处仅收录input标签的例子,并且只给出了主体代码部分

```html
<input type="text" placeholder="请输入用户名">
<input type="range">
<input type="number" min="1" max="10">
<input type="date" min="2018-01-01">
<!-- 多选 -->
<p>
    <label for=""><input type="checkbox">⚽</label>
    <label for=""><input type="checkbox" checked>🏀</label>
</p>
<!-- 单选 -->
<p>
    <label for=""><input type="radio" name="fruits">🍎</label>
    <label for=""><input type="radio" name="fruits">🍏</label>
</p>
<!-- 下拉选项 -->
<p>
    <select name="" id="">
        <option value="">🍦</option>
        <option value="">🍵</option>
        <option value="">🍬</option>
    </select>
</p>
<!-- 文本提示选项 -->
<p>
    <input list="NameList">
    <datalist id="NameList">
        <option>zbwer</option>
        <option>Fs Anna</option>
        <option>duoluoluo</option>
    </datalist>
</p>
```

**常见类型总结**

| type的属性值 | 描述                         |
| ------------ | ---------------------------- |
| text         | 输入文本类型                 |
| number       | 仅允许输入数字类型           |
| range        | 通过拖动控件实现输入一个范围 |
| date         | 输入日期类型                 |
| checkbox     | 多选框                       |
| radio        | 单选框                       |
| password     | 密码类型,输入时不可见        |

**常见属性总结**

| 属性        | 描述                                  |
| ----------- | ------------------------------------- |
| placeholder | 输入内容为空时的提示词                |
| min / max   | 设置输入内容的最大最小值              |
| name        | 给每个radio赋值相同的name实现单选效果 |
| checked     | 默认选中                              |

### 四、课后个人总结：

本章难点应该是对各种HTML标签的记忆以及不同使用场景下如何选用恰当的标签.

易混点我觉得在于`id`和`name`属性的使用上,在使用单选框`radio`时我总会把`name`写成`id`.

### 五、引用参考：

无