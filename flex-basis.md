# flex基础篇
##一、flex布局是什么？
Flex是Flexible Box的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。
任何一个容器都可以指定为flex布局

```javascript
//块元素指定
.box{
    display: flex;
}

//行内元素容器指定
.box{
    display:inline-flex;
}

//Webkit内核的浏览器，必须加上-webkit前缀。
.box{
    display: -webkit-flex;
    display: flex;
}
```
**注意，设为Flex布局以后，子元素的float、clear和vertical-align属性将失效。**

##二、基本概念
使用flex布局的容器被称为flex容器，容器内部的子元素自动称为flex项目。

容器默认存在两根轴，水平的主轴和垂直的交叉轴。由flex-direction属性指定

![bg2015071004](media/14866156376820/bg2015071004.png)

项目默认沿主轴排列。单个项目占据的主轴空间叫做main size，占据的交叉轴空间叫做cross size。

##三、容器的属性
以下六个属性定义在容器上

```
- flex-direction
- flex-wrap
- flex-flow
- justify-content
- align-items
- align-content
```

###3.1 `flex-direction`属性
`flex-direction`属性决定主轴的方向（即项目的排列方向）。

```
.box{
    flex-direction: row | row-reverse | column | column-reverse;
}
```
![bg2015071005](media/14866156376820/bg2015071005.png)

###3.2 `flex-warp`属性
默认情况下项目排列在一条线上，`flex-warp`属性定义了当一行排不下时候如何换行。![bg2015071006](media/14866156376820/bg2015071006.png)


```
.box{
    flex-wrap: nowrap | wrap | wrap-reverse;
}
```
它可能取三个值。
(1)`nowarp` (默认):不换行
![bg2015071007](media/14866156376820/bg2015071007.png)

(2)`warp`换行，第一行在上面
![bg2015071008](media/14866156376820/bg2015071008.jpg)

(2)`warp-reverse`换行，第一行在下面
![bg2015071009](media/14866156376820/bg2015071009.jpg)

###3.3 `flex-flow`属性
该属性为`flex-direction`和`flex-warp`两种属性的简写形式，默认为 `row  nowarp`

```
.box {
    flex-flow: <flex-direction> || <flex-wrap>;
}
```
###3.4 `justify-content`属性
该属性决定项目在主轴上的对齐方式

```
.box {
    justify-content: flex-start | flex-end | center | space-between | space-around;
}
```

它可能取5个值，具体对齐方式与轴的方向有关。下面假设主轴为从左到右

```
flex-start（默认值）：左对齐

flex-end：右对齐

center： 居中

space-between：两端对齐，项目之间的间隔都相等。

space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。
```

![bg2015071010](media/14866156376820/bg2015071010.png)


###3.5 `align-items`属性
该属性主要决定项目在交叉轴上如何对齐

```
.box {
    align-items: flex-start | flex-end | center | baseline | stretch;
}
```
![bg2015071011](media/14866156376820/bg2015071011.png)

它可能取5个值。具体的对齐方式与交叉轴的方向有关，下面假设交叉轴从上到下。

```
flex-start：交叉轴的起点对齐。

flex-end：交叉轴的终点对齐。

center：交叉轴的中点对齐。

baseline: 项目的第一行文字的基线对齐。

stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。
```

###3.6 `align-content`属性
该属性决定了多根轴线的对齐方式，如果项目只有一根轴线，该属性不起作用.即决定多行在纵轴上的排列方式

```
.box {
    align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}
```
![bg2015071012](media/14866156376820/bg2015071012.png)

该属性可能有六个取值

```
flex-start：与交叉轴的起点对齐。

flex-end：与交叉轴的终点对齐。

center：与交叉轴的中点对齐。

space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。

space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。

stretch（默认值）：轴线占满整个交叉轴。
```
##四、项目的属性
共有以下6个属性定义在项目上

```
- order
- flex-grow
- flex-shrink
- flex-basis
- flex
- align-self
```
###4.1 `order`属性
order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。

```
.item {
    order: <integer>;
}
```
![](media/14866156376820/14866227715767.jpg)

###4.2 `flex-grow`属性
该属性定义项目的放大比例，默认为`0`，即如果存在剩余空间，也不放大。

```
.item {
    flex-grow: <number>; /* default 0 */
}
```
![](media/14866156376820/14866228548837.jpg)

如果所有项目的`flex-grow`属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的`flex-grow`属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。

###4.3 `flex-shrink`属性
该属性定义了项目的缩小比例，默认为1，即项目空间不足时候同比例缩小

```
.item {
    flex-shrink: <number>; /* default 1 */
}
```
![](media/14866156376820/14866235688282.jpg)

如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。

###4.4 `flex-basis`属性
`flex-basis`属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。

它可以设为跟`width`或`height`属性一样的值（比如350px），则项目将占据固定空间。

###4.5 `flex`属性
该属性是前面三个属性`flex-grow`、`flex-shrink`、`flex-basis`的简写,后两者可选

###4.6 `align-self`属性
`align-self`属性允许单个项目有与其他项目不一样的对齐方式，可覆盖`align-items`属性。默认值为auto，表示继承父元素的`align-items`属性，如果没有父元素，则等同于`stretch`。

```
.item {
    align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```
![](media/14866156376820/14866250440869.jpg)

该属性可能取6个值，除了auto，其他都与align-items属性完全一致。

