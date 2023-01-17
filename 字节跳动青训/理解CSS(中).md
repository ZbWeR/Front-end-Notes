## 理解CSS(中) | 青训营笔记

这是我参与「第五届青训营 」伴学笔记创作活动的第 3 天

## 一、本堂课重点内容：

1. CSS 选择器的特异度
2. CSS 继承
3. CSS 求值过程解析
4. CSS 布局方式及相关技术

## 二、详细知识点介绍：

### 1.选择器的特异度

对于同一个HTML元素,往往有多种方法可以将其选出，但不同方法之间的优先级不同,特异度的引入就是为了将其区分开来.

选择器的特异度分为4个等级，a b c d，从左到右，越左边的越优先, 如果一个选择器规则有多个相同类型选择器，则$+1$.

+ $a$等级:HTML内联样式.
+ $b$等级: id 选择器.
+ $c$等级: (伪)类选择器,属性选择器.
+ $d$等级: 标签选择器,伪元素选择器,通配符选择器.

特异度示例: 

|      选择器       | 特异度  |
| :---------------: | :-----: |
|        `p`        | 0,0,0,1 |
|     `.box p`      | 0,0,1,1 |
|   `.box #iamp`    | 0,1,1,0 |
| `.content .box p` | 0,0,2,1 |

比较特异度时,从高位到低位依次比较(特异度不会产生进位),特异度相同时,后定义的会覆盖掉先定义的.

### 2.继承

某些属性会自动继承其父元素的计算值，除非显式指定一个值. 

+ 文字属性默认会被继承,盒模型的属性通常默认不会被继承.此时可以为想要继承的属性赋值`inherit`,即可达到预期.

+ 如果某个属性没有成功继承或者人为给定值,它就会保持初始值.

  > 初始值: CSS中每个元素都有一个初始值,例如`background-color`初始值为`transparent`.可以使用`initial`关键字将某个属性重置为初始值

### 3.求值过程

<img src="https://assets.codepen.io/59477/value.svg" style="background-color:black">

文字概括: 从多个**声明值**中找出优先级最高的**层叠值**,若层叠值为空则使用继承或初始值,经过该处理后的是**指定值**(非空),仅看HTML和CSS将指定值转化为**计算值**(em->px),再根据实际布局的窗口大小等等将上一步未转换的值转化为**使用值**,最后将小数转为整数得到最终的**实际值**.

### 4.布局

布局是什么: 依据元素，容器，兄弟节点和内容等信息来确定内容的大小和位置的算法.

布局相关技术: 浮动，绝对定位,常规流(行级,块级,Flex,Grid,表格).

#### 盒子模型

![image-20230117113237775](C:\Users\zbwer\AppData\Roaming\Typora\typora-user-images\image-20230117113237775.png)

1. **height/weight**

用于指定content box的宽高;取值为长度,百分数(相对于有**指定**宽高的父级容器),auto(由浏览器其他属性决定)

2. **padding**

内边距,即内容与边框之间的距离,属性取值同上.此外还可通过`-left`,`-right`,`-top`,`-bottom`单独设置不同方向的内边距.

例如：`padding-left`就是仅设置左侧的内边距.

3. **border**

为盒子模型设置边框,具有三种属性四个方向(写法与padding相同).

| 属性           | 描述                                     |
| -------------- | ---------------------------------------- |
| `border-width` | 设置边框的粗细(px/em等)                  |
| `border-style` | 设置边框的类型(solid实线 dotted点线等等) |
| `border-color` | 设置边框的颜色(rgb/hsl)                  |

写法示例:`border-left:1px solid #ccc`表示 1px 粗且颜色为 #ccc 的实线边框.

技巧：利用边框绘制三角形.【此处待补充应用代码】

4. **margin** 【此处待填充技巧和折叠示例代码】

外边距,即不同盒子模型之间的距离,属性取值与`padding`相同.

技巧: 可以利用`margin:0 auto`实现水平居中.

外边距垂直方向的折叠: 上面的元素设置`margin-bottom`而下面的元素设置`margin-top`时,它们之间的距离为两者最大值而非加和.解决方法见后文BFC排版部分.

5. **border-box**

默认情况下,`height`设置的是content box的高度.我们可以通过`box-sizing:border-box`的方法,使得`height`设置的是整个盒子的高度.实际开发中经常会把所有盒模型都设为**border-box**.

6. **overflow**

当盒子中的内容超越本身盒子模型的宽高时,我们可以通过`overflow`属性去设置如何展示这些内容.

| 属性值  | 描述                        |
| ------- | --------------------------- |
| visible | 可见                        |
| hidden  | 超出部分隐藏                |
| scroll  | 显示滚动条                  |
| auto    | 未超出不处理,超出显示滚动条 |

#### 行级 vs.块级

| 块级                                             | 行级                                     |
| :----------------------------------------------- | ---------------------------------------- |
| 不和其他盒子并列摆放                             | 可以和其他盒子放在一行                   |
| 适用于盒模型的所有属性                           | 宽高属性对行级元素无效,只取决于内容多少. |
| body,article,div,main,<br>section,h1-6,p,ul,li等 | span,em,strong,img,a等                   |
| `display:block`                                  | `display:inline`                         |

关于`display`属性: block(块级),inline(行级),**inline-block**(行内块,既能放在一行,又对宽高属性有效,不会被拆成多行),none(排版时忽略).【待填充参考代码->inline-block】

#### 行级排版上下文(IFC)

只包含行级盒子的容器会创建一个IFC.其排版规则如下:

+ 盒子在一行内水平摆放，一行放不下时则换行显示.
+ `text-align`决定一行内盒子的水平对齐,`veritical-align`决定一个盒子在行内的竖直对齐.
+ 避开浮动元素*

#### 块级排版上下文(BFC)

许多容器会创建一个BFC,例如: 

+ 根元素.
+ 浮动、绝对定位、display为`inline-block / flow-root`.
+ Flex子项和Grid子项.
+ overflow的值不为visible的块盒.

其排版规则如下:

+ 盒子从上到下排序.
+ BFC盒子内,垂直方向上margin合并,而不会与外面的合并.
+ BFC不会与浮动元素重叠.

## 三、实践练习例子：

**继承**

```html
<p>This is a<em>test</em> of <strong>inherit</strong> </p>

<style>
    body {font-size: 20px; }
    p {color: blue; }
    em {color: red;}
</style>
```

strong 标签的`font-size`继承自 body,而 `color`继承自 p. 表示为 蓝色的20px字体.

**行级排版与inline-block**

```html
<div>
  This is a paragraph of text with long word Honorificabilitudinitatibus. Here is an image
  <img src="https://assets.codepen.io/59477/cat.png" alt="cat">
  And <em>Inline Block</em>
</div>

<style>
  div {
    width: 15em;
    //overflow-wrap: break-word;
    background: #411;
  }
  em {
    display: inline-block;
    width: 3em;
    background: #33c;
  }
</style>
```

div 标签中均为行级元素,故遵循行级排版上下文规则,可以看到文字、图片和`InlineBlock`在一行内水平摆放.而 em 标签设置为了行内块元素,此时再设置宽度,由于内容超出宽度故自动换行.

`overflow-wrap`表示如何进行溢出换行处理.

## 四、课后个人总结：

**难点**:选择器特异度相关,写选择器时要注意特异度的问题,可能会导致某个样式被覆盖而不生效.个人的理解是**选择器越精确特异度就越高**,所以在写选择器时我会写得尽可能精确.

**易混点**: 

1. 默认盒模型和`border-box`之间的差异,有时候可能会忘记进行`border-box`设置,然后出现布局上的小差错.
2. 行内元素的宽高属性是无效的,在自己尝试时我经常会忘记这一点.

## 五、引用参考：

1. 选择器特异度部分参考:[CSS选择器特殊性，先后顺序 - 简书 (jianshu.com)](https://www.jianshu.com/p/bbec23d318f4)

