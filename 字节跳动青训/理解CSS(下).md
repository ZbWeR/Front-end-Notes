## 理解CSS(下) | 青训营笔记

这是我参与「第五届青训营 」伴学笔记创作活动的第 4 天

## 一、本堂课重点内容：

1. CSS Flex布局
2. CSS Grid布局

## 二、详细知识点介绍：

### 1.Flex 弹性布局

通过指定`display:flex`来为子元素设置弹性布局效果。

1. **flex-direction**属性指定了弹性子元素在父容器中的排列方向和顺序。

   | 属性值         | 描述                     |
   | -------------- | ------------------------ |
   | row            | 默认值，横向从左到右排列 |
   | row-reverse    | 横向从右到左排列         |
   | column         | 纵向从上到下排列         |
   | column-reverse | 纵向从下到上排列         |

2. **flex-wrap** 属性用于指定弹性盒子的子元素换行方式。

   | 属性值       | 描述                                                         |
   | ------------ | ------------------------------------------------------------ |
   | wrap         | 弹性容器为多行。该情况下弹性子项溢出的部分会被放置到新行，子项内部会发生断行。 |
   | nowrap       | 默认， 弹性容器为单行。该情况下弹性子项可能会溢出容器。      |
   | wrap-reverse | 反转 wrap 排列                                               |

3. **align-items** 属性是用来设置或检索弹性盒子元素在侧轴（纵轴）方向上的对齐方式。

   | 属性值     | 描述                                  |
   | ---------- | ------------------------------------- |
   | flex-start | 对齐侧轴的起始边界                    |
   | flex-end   | 对齐侧轴的结束边界                    |
   | center     | 在侧轴上居中放置,通常用来实现垂直居中 |
   | stretch    | 如果侧轴方向上的长度未定,则会自动拉伸 |

​	除此之外,还可以通过**align-self**设置单个元素的对齐方式.

4. **align-content** 属性可以用于控制**多行**的对齐方式，如果只有一行则不会起作用。

​	Tips: 与`align-items`的区别在于,假设子元素有两行，`items`是让子元素在对应的行内居中，比如子元素1位于第一行，就让子元素1在第一行居中，子元素7位于第二行，就让子元素7在第二行居中。而`content`是把所有子元素看成一个整体，让他们全部居中。

​	语法格式：`align-items: flex-start | flex-end | center | baseline | stretch;`

5. **justify-content**属性用于指定元素在主轴上的对齐方式。

   | 属性值        | 描述                                     |
   | ------------- | ---------------------------------------- |
   | center        | 水平居中                                 |
   | space-around  | 元素之间间隔相等，首尾空白为间隔距离一半 |
   | space-evenly  | 元素之间包括首尾间隔都相等               |
   | space-between | 首尾元素靠紧边界，元素之间距离相等。     |

6. **order**属性用于指定单个项目在事觉顺序中的显示位置.示例语法:`order:1;`

​	属性值越小,则排在越前面,默认属性值$0$,可以通过将属性值设为$-1$让某个元素排在最前面.

7. 有关弹性的属性:当容器有剩余空间时,会伸展;当容器空间不够时,会收缩.

| 属性        | 属性值                 | 描述                                         |
| ----------- | ---------------------- | -------------------------------------------- |
| flex-grow   | <number>               | 有剩余空间时的伸展能力,数字越大能力越强      |
| flex-shrink | <number>               | 容器空间不足时的收缩能力,数字越大能力越强    |
| flex-basis  | 关键字content或<width> | 无伸展无收缩时的基准长度,优先级大于width属性 |

复合属性**flex**,语法格式: `flex: flex-grow flex-shrink flex-basis`.

### 2.Grid 网格布局

通过指定`display:grid`来为子元素设置弹性布局效果。

1. **grid-template-rows/columns**属性用于设置网格轨道的数量以及尺寸大小.

例如:

+ `grid-template-columns: 100px 100px 100px;`设置了三个宽度为100px的列轨道.
+ `grid-template-columns: 1fr 1fr 1fr;`设置了三个宽度为1/3的列轨道.其中`fr`为可用空间的比例.
+ `grid-template-columns: repeat(3,1fr)`含义与上述语句相同,`repeat()`用于快速创建重复轨道.

2. **grid-auto-rows/columns**属性用于指定隐式创建轨道的大小.

我们利用**-template-**创建列(行)轨道之后,网格会根据内容**自动**创建另一方向上的轨道,此时我们可以通过**-auto-**去设置这些**自动**创建轨道的大小.例如:

```css
grid-template-columns: repeat(3, 100px);
grid-auto-rows: 100px;
```

该例中,我们创建了3个宽为 100px 的列轨道,并且设置行轨道高度为 100px.

其他技巧: `grid-auto-rows: minmax(100px, auto);`行轨道高度最小为100px,最大为内容高度,此处是**minmax**语句的作用.

3. **grid-area**属性通过网格线来确定元素的具体大小与位置.

例如：`grid-area: 1/1/3/2;`表示该元素的区域为**列轨道线1~3**,**行轨道线1~2**.即占有一二行第一列的两个网格.

取值解释: `a/b/c/d`,a表示列轨道线开头,c表示列轨道线结尾,b d为行轨道线开头和结尾.

## 三、实践练习例子：

**Grid布局示例**

```html
<style>
    .wrapper {
        display: grid;
        background-color: #fff4e6;
        border: 1px solid red;
        /* templat控制列轨道宽度,搭配auto控制行轨道高度 */
        grid-template-columns: repeat(3, 100px);
        /* grid-auto-rows: 100px 100px; */
        /* 最小高度为100px,最大高度适应内容 */
        grid-auto-rows: minmax(100px, auto);
    }

    .wrapper div {
        background-color: #ffd8a8;
        border: 1px solid #ffa94d;
        border-radius: 5%;
    }

    .wrapper div:nth-child(1) {
        background-color: pink;
        /* 列s/行s/列e/行e */
        grid-area: 1/1/3/2;
    }
</style>
<div class="wrapper">
    <div>One</div>
    <div>Two</div>
    <div>Three</div>
    <div>Four</div>
    <div>Five</div>
    <div>Six</div>
    <div>Seven</div>
    <div>Eight</div>
</div>
```

## 四、课后个人总结：

**难点**: Gird 布局中轨道的创建,个人理解是先采用**-template-**去设置一个方向上的轨道,再利用**-auto-**去设置另一个方向上的尺寸.

**易混点**: 

1. 区分`justify-`和`align-`到底哪一个是垂直哪一个是水平.
2. 区分`-content`和`-items`到底哪一个是所有内容为基准,哪一个是以一行上的内容为基准.

## 五、引用参考：

+ [【迄今为止最易懂】2分钟掌握 CSS Grid 布局_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV18p411A7JB/?spm_id_from=333.337.search-card.all.click)
