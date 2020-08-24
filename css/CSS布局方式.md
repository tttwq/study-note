## 传统布局

>  传统布局方式就是通过盒模型，使用 `display` 属性（文档流布局） + `position` 属性（定位布局） + `float属性`（浮动布局）

### 文档流

> 网页是一个多层的结构，通过CSS可以为每一层设置样式，用户只能看到最顶上一层；
>
> 最底下一层为文档流，是网页的基础；
>
> 元素主要有两个状态：在文档流中、脱离文档流；
>
> 我们所创建的元素默认在文档流；
>
> 元素在文档流中的特点：
>
> > 1. 块元素
> >
> >    > 块元素在文档流中独占一行；
> >    >
> >    > 自上向下垂直排列；
> >    >
> >    > 默认宽度是父元素的全部（充满父元素）；
> >    >
> >    > 默认高度被内容撑开；
> >
> > 2. 行内元素
> >
> >    > 行内元素不会独占一行；
> >    >
> >    > 自左向右水平排列，如果一行无法容纳，则会换行；
> >    >
> >    > 默认宽度和高度被内容撑开；

### 文档流布局（display）

#### 盒模型的布局

##### 水平布局

> 元素在其水平方向的布局由以下几个属性共同决定：
>
> > `margin-left`,    `border-left`,    `padding-left`,    `width`,    `padding-right`,    `border-right`,    `margin-right`
>
> 子元素存在于父元素的内容区；
>
> `margin-left`+ `border-left`+ `padding-left`+`width`+ `padding-right`+`border-right`+ `margin-right`  == 父元素内容区宽度；
>
> 以上等式若不满足，称为过度约束；
>
> `margin-left`、`width`、 `margin-right` 的值可以设置为auto；
>
> 过度约束时:
>
> > 若属性值没有auto，浏览器会自动调整`margin-right`，使等式成立；
> >
> > 若属性值为auto，则浏览器会自动调整auto值，使等式成立；
> >
> > > 若只有一个宽度和一个外边距设置为auto时，调整宽度；
> > >
> > > 若只有两个外边距设置为auto时，调整两个外边距（设置水平居中）；
> > >
> > > 若宽度和外边距都为auto时，调整宽度；
> >
> > ```markdown
> > <!DOCTYPE html>
> > <html>
> > <head>
> > 	<title></title>
> > 	<style type="text/css">
> > 		.box{
> > 			width: 800px;
> > 			height: 100px;
> > 			border: 1px solid black;
> > 		}
> > 		.inner1{
> > 			background-color: pink;
> > 			height: 100px;
> > 			width: 200px;
> > 		}
> > 		.inner2{
> > 			background-color: pink;
> > 			height: 100px;
> > 			width: 200px;
> > 			margin-left: auto;
> > 		}
> > 		.inner3{
> > 			background-color: pink;
> > 			height: 100px;
> > 			width: auto;
> > 			margin-left: auto;
> > 		}
> > 		.inner4{
> > 			background-color: pink;
> > 			height: 100px;
> > 			width: 200px;
> > 			margin-left: auto;
> > 			margin-right: auto;
> > 		}
> > 		.inner5{
> > 			background-color: pink;
> > 			height: 100px;
> > 			width: auto;
> > 			margin-left: auto;
> > 			margin-right: auto;
> > 		}
> > 	</style>
> > </head>
> > <body>
> > 	<div class="box">
> > 		<div class="inner1"></div>
> > 	</div>
> > 	<br />
> > 	<div class="box">
> > 		<div class="inner2"></div>
> > 	</div>
> > 	<br />
> > 	<div class="box">
> > 		<div class="inner3"></div>
> > 	</div>
> > 	<br />
> > 	<div class="box">
> > 		<div class="inner4"></div>
> > 	</div>
> > 	<br />
> > 	<div class="box">
> > 		<div class="inner5"></div>
> > 	</div>
> > </body>
> > </html>
> > ```
> >
> > <img src="D:/note/css/image/row.PNG" width="80%" height="80%">
>
> `width`的默认值为auto；

#####  垂直布局

> 默认情况父元素高度被内容撑开；
>
> 若设置了高度，当子元素高度>父元素时，子元素会从父元素溢出；
>
> 给父元素设置`overflow`属性处理溢出的元素；
>
> > visible：在父元素外部显示；
> >
> > hidden：溢出内容被裁减隐藏；
> >
> > scroll：在水平和垂直方向生成滚动条；
> >
> > auto：根据需要生成滚动条；

##### 外边距的折叠

> **相邻垂直方向**外边距会发生折叠现象；
>
> > 兄弟元素:
> >
> > > 两者同号时，取绝对值较大的；
> > >
> > > 一正一负，取两者的和；
> >
> > 父子元素：
> >
> > > 子元素的上外边距会传递给父元素（影响布局）；
> >
> > 解决办法：
> >
> > ```css
> > .inner::before{
> > 			content: '';
> > 			display: table;
> > 		}
> > ```
> >
> > `display`设置为inline-block会出现空隙；

#### 行内元素的盒模型

> 不支持设置宽度`width`和高度`height`；
>
> 可以设置`padding`、`border`、 `margin`，垂直方向不影响页面布局；
>
> `display` 设置元素显示类型：
>
> > inline：设置为行内元素；
> >
> > block：设置为块元素；
> >
> > inline-block：设置为行内块元素；
> >
> > table：设置为表格；
> >
> > none：不显示；
>
> `display: none`和`visibility: hidden`：
>
> > `display: none`：元素不在页面中显示；
> >
> > `visibility: hidden`：元素不显示，但依然占据页面的位置；
>
> inline-block：两个inline-block之间存在空白间隙；
>
> > 原因：inline-block元素被当成行内元素排版，元素之间空白符（空格、回车等）都会被浏览器处理；
> >
> > 空隙大小与字体大小相关；
> >
> > 解决办法：
> >
> > 1. 上一个元素的闭合标签与下一个元素的开始标签写在一起；
> > 2. 在两个inline-block元素间加上注释
> > 3. 父元素设置`font-size`为0，子元素再单独设置字体大小；
> > 4. 设置`margin-right`为负值；
> > 5. 父元素设置`letter-spacing`或`word-spacing`为负值，子元素再调整为0；
> > 6. 给inline-block元素加float；

#### 盒子的大小

> `box-sizing` 设置盒子尺寸计算方式，可选值：
>
> > `content-box`：默认值，`width`和`height`用来设置内容区宽度和高度；
> >
> > `border-box`：`width`和`height`用来设置可见框（content、padding、border）宽度和高度；

### 浮动布局（float）

> 通过浮动可以使一个元素向其父元素的左侧或右侧移动；
>
> 使用`float`属性设置元素的浮动，可选值：
>
> > `none`：默认值，不浮动；
> >
> > `left`：向左浮动；
> >
> > `right`：向右浮动；
>
> 元素设置浮动后会从文档流脱离，但不脱离文本流；
>
> 元素脱离文档流后：
>
> > 块元素不在独占一行，默认宽度和高度被内容撑开；
> >
> > 行内元素可以设置宽度和高度，特点和块元素一样；
>
> 元素设置浮动后，水平布局的等式不需要强制成立；
>
> 浮动元素默认不会从父元素中移出；
>
> 浮动元素不会盖住其他浮动元素；
>
> 如果浮动元素的上方是没有浮动的块元素，则浮动元素无法上移；

#### 高度塌陷

> 在浮动布局中，父元素高度被子元素撑开，当子元素设置浮动后，子元素从文档流脱离，无法撑起父元素高度，其下元素上移，影响页面布局。
>
> 解决办法：
>
> 1. 开启BFC（块级格式化环境，CSS隐含属性-间接开启，`float`、`overflow`）
>
>    > 开启BFC的元素不会被浮动元素覆盖，子元素与父元素外边距不会折叠，可以包含浮动的子元素；
>    >
>    > 常用方式，在父元素设置：
>    >
>    > > ```css
>    > > overflow: hidden;
>    > > ```
>
> 2. 使用after伪类
>
>    > clear元素：
>    >
>    > >  清除浮动元素对当前元素所产生的影响，可选值：
>    > >
>    > > > `left`：清除左侧浮动元素对当前元素的影响；
>    > > >
>    > > > `right`：清除右侧浮动元素对当前元素的影响；
>    > > >
>    > > > `both`：清除两侧中最大的影响；
>    > >
>    > > 原理：浏览器自动为元素添加一个上外边距使其位置不收影响；
>    >
>    > ```css
>    > .outer::after{
>    > 			content: '';
>    > 			display: block;
>    > 			clear: both;
>    > 		}
>    > ```
>
> 3. clearfix
>
>    > ```css
>    > .clearfix::before,.clearfix::after{
>    > 			content: '';
>    > 			display: table;
>    > 			clear: both
>    > 		}
>    > ```
>    >
>    > 给父元素设置clearfix类，同时解决高度塌陷和外边距重叠的问题；

### 定位布局（position）

#### 相对定位

> ```css
> position: relative;
> ```
>
> 开启相对定位后，如果不设置偏移量，元素不发生任何变化；
>
> 相对定位参照与元素在文档流中的位置进行定位；
>
> 相对定位会提升元素层级；
>
> 不会使元素脱离文档流，不改变元素性质；

#### 绝对定位

> ```css
> position: absolute;
> ```
>
> 开启绝对定位后，如果不设置偏移量，元素的位置不发生变化；
>
> 会使元素从文档流中脱离，会改变元素性质；
>
> 绝对定位会提升元素层级；
>
> 绝对定位参照最近的开启定位的祖先元素；
>
> `left`+`margin-left`+ `border-left`+ `padding-left`+`width`+ `padding-right`+`border-right`+ `margin-right`+`right` == 包含框内容区宽度；
>
> 过度约束时浏览器自动调整`right`或`auto`值；

#### 固定定位

> ```css
> position: fixed;
> ```
>
> 开启固定定位后，会使元素从文档流中脱离，会改变元素性质；
>
> 绝对定位会提升元素层级；
>
> 如果不设置偏移量，元素的位置不发生变化；
>
> 固定定位参照浏览器视窗进行定位；

#### 元素的层级

> 对于开启了定位的元素，可以通过`z-index`指定元素的层级；
>
> `z-index`接受一个整数作为参数，值越大层级越高；
>
> 若元素层级一样，优先显示结构上靠下的元素；

## table布局

>  实现简单的布局，将表格的`border`、`cellpadding`、`cellspacing`全部设置为`0`，表格的边框和间距就不占有页面空间，它只起到划分空间的作用；
>
>  如果布局复杂，可以在单元格中再嵌套表格，单元格中的元素或者嵌套的表格用`align`和`valign`设置对齐方式；
>
>  `display:table；`；
>   `display:table-cell`：相当于td元素；
>   `display:table-row`：相当于tr元素；
>   `table-layout`：用于显示表格单元格、行、列的算法规则；
>
>  可选值：
>
>  > `auto`：自动表格布局，列的宽度由单元格中最大内容宽度决定，算法较慢 （在确定最终布局之前要访问表格中所有内容）；
>  >
>  > `fixed`：固定表格布局，接收第一行就可以显示表格，与表格内容无关；
>
>  缺点：
>
>  > `<table>`要比其它`html`标记占更多的字节，代码的复杂度会大大提升；
>  >
>  > `<table>`是整体载入后才开始显示的，没有加载完毕前，`<table>`为一片空白，而`<div>`等标签可以逐行渲染，一边加载一边显示；
>  >
>  > `<table>`里显示图片时有可能需要你把单个、有逻辑性的图片切成多个图；
>  >
>  > `<table>`会影响其单元格内部的某些布局属性的生效；
>  >
>  > `<table>`的语义是数据表格，使用`<table>`来布局不利于`SEO`；
>  >
>  > 若布局较为复杂，则可能造成多层`<table>`嵌套，代码嵌套过多表现的过于复杂；

## 弹性布局（Flex）

> 
>
> 弹性布局中元素的大小是高度依赖父容器的大小，目标就是为了撑满父元素；
>
> 浏览器的布局方式：沿着主轴的方向依次排列，如果要换行，则沿着交叉轴的方向进行换行；
>
> ```css
> 
> display: flex;
> display:inline-flex;
> display:-webkit-flex;
> ```
>
> Webkit 内核的浏览器，必须加上`-webkit`前缀；
>
> 设为 Flex 布局以后，子元素的`float`、`clear`和`vertical-align`属性将失效；
>
> 采用 Flex 布局的元素，称为 Flex 容器（flex container），它的所有子元素自动成为容器成员，称为 Flex 项目（flex item）；

### Flex容器

> <img src="./image/flexContainer.png" width="80%" height="80%">
>
> 默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）;
>
> 主轴的开始位置叫做`main start`，结束位置叫做`main end`；
>
> 交叉轴的开始位置叫做`cross start`，结束位置叫做`cross end`;
>
> 项目默认沿主轴排列。单个项目占据的主轴空间叫做`main size`，占据的交叉轴空间叫做`cross size`。

### 容器属性

#### flex-direction

> 决定主轴的方向，可选值：
>
> > `row`（默认值）：主轴为水平方向，起点在左端；
> >
> > `row-reverse`：主轴为水平方向，起点在右端；
> >
> > `column`：主轴为垂直方向，起点在上沿；
> >
> > `column-reverse`：主轴为垂直方向，起点在下沿；

#### flex-wrap

> 定义当项目在一条轴线排不下时，如何换行，可选值：
>
> > `nowrap`（默认值）：不换行；
> >
> > `wrap`：换行，第一行在上方；
> >
> > `wrap-reverse`：换行，第一行在下方；

#### flex-flow

> `flex-direction`属性和`flex-wrap`属性的简写形式；
>
> ```css
> flex-flow: <flex-direction> <flex-wrap>;
> ```

#### justify-content

> 定义了项目在主轴上的对齐方式，可选值：
>
> >`flex-start`（默认值）：左对齐；
> >
> >`flex-end`：右对齐；
> >
> >`center`： 居中；
> >
> >`space-between`：两端对齐，项目之间的间隔都相等；
> >
> >`space-around`：每个项目两侧的间隔相等，项目之间的间隔比项目与边框的间隔大一倍；

#### align-items

> 定义项目在交叉轴上如何对齐，可选值：
>
> > `flex-start`：交叉轴的起点对齐；
> >
> > `flex-end`：交叉轴的终点对齐；
> >
> > `center`：交叉轴的中点对齐；
> >
> > `baseline`: 项目的第一行文字的基线对齐；
> >
> > `stretch`（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度；

#### align-content

> 定义了多根轴线的对齐方式，如果项目只有一根轴线，该属性不起作用；
>
> 可选值：
>
> > `flex-start`：与交叉轴的起点对齐；
> >
> > `flex-end`：与交叉轴的终点对齐；
> >
> > `center`：与交叉轴的中点对齐；
> >
> > `space-between`：与交叉轴两端对齐，轴线之间的间隔平均分布；
> >
> > `space-around`：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍；
> >
> > `stretch`（默认值）：轴线占满整个交叉轴；

### 项目属性

#### order

> 定义项目的排列顺序，数值越小，排列越靠前，默认为0；

#### flex-grow

> 定义项目的放大比例，默认为`0`，即如果存在剩余空间，也不放大；

#### flex-shrink

> 定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小；

#### flex-basis

> 定义了在分配多余空间之前，项目占据的主轴空间（main size）；
>
> 浏览器根据这个属性，计算主轴是否有多余空间；
>
> 它的默认值为`auto`，即项目的本来大小；
>
> 可以设为跟`width`或`height`属性一样的值；

#### flex

> `flex-grow`, `flex-shrink` 和 `flex-basis`的简写，默认值为`0 1 auto`；
>
> 有两个快捷值：`auto` (`1 1 auto`) 和 `none` (`0 0 auto`)；

#### align-self

> 允许单个项目有与其他项目不一样的对齐方式，可覆盖`align-items`属性；
>
> 可选值：
>
> > `auto`|`flex-start`|`flex-end`|`center`|`baseline`|`stretch`
>
> 默认值为`auto`，表示继承父元素的`align-items`属性，如果没有父元素，则等同于`stretch`；

## 网格布局（Grid）

> 将网页划分成一个个网格，可以任意组合不同的网格，做出各种各样的布局;
>
> ``` css
> display: grid;
> display: inline-grid;
> ```
>
> 设为网格布局以后，容器子元素（项目）的`float`、`display: inline-block`、`display: table-cell`、`vertical-align`和`column-*`等设置都将失效；

### 容器属性

#### grid-template-columns && grid-template-rows

> 定义每一列的列宽，每一行的行高；
>
> 可以用绝对单位，也可以用百分比；
>
> 可以使用方括号，指定每一根网格线的名字，允许同一根线有多个名字；
>
> 关键字：
>
> > `auto-fill`：当容器的大小不确定时，让每一行（或每一列）容纳尽可能多的单元格；
> >
> > `fr`：用于分配剩余空间，表示每一行（或每一列）的比例关系；
> >
> > `auto`：浏览器自己决定长度；
>
> 使用`repeat()`函数简化重复值；
>
> > `repeat()`函数接收两个参数：重复次数，要重复的值；
>
> `minmax()`产生一个长度范围，表示长度就在这个范围之中；
>
> > `minmax()`接收两个参数：最大值，最小值；

#### row-gap && column-gap && gap

> 设置行间距，列间距；

#### grid-template-area

> 定义区域；
>
> ```css
> .container {
>   display: grid;
>   grid-template-columns: 100px 100px 100px;
>   grid-template-rows: 100px 100px 100px;
>   grid-template-areas: 'a a a'
>                        'b b b'
>                        'c c c';
> }
> ```
>
> 上面代码将9个单元格分成`a`、`b`、`c`三个区域；
>
> 如果某些区域不需要利用，则使用"点"（`.`）表示；
>
> 区域的命名会影响到网格线，每个区域的起始网格线，会自动命名为`区域名-start`，终止网格线自动命名为`区域名-end`；

#### grid-auto-flow

> 指定容器的子元素在网格中的放置顺序，可选值：
>
> >`row`：先行后列；
> >
> >`column`：先列后行；
> >
> >`row dense`：先行后列，并且尽可能紧密填满，尽量不出现空格；
> >
> >`column dense`

#### justify-items && align-items && place-items

> 设置单元格内容的水平位置、垂直位置；
>
> ` place-items`是`align-items`属性和`justify-items`属性的合并简写形式；
>
> 可选值：
>
> > start：对齐单元格的起始边缘；
> >
> > end：对齐单元格的结束边缘；
> >
> > center：单元格内部居中；
> >
> > stretch：拉伸，占满单元格的整个宽度（默认值）;

#### justify-content && align-content && place-content

> 整个内容区域在容器里面的水平位置，垂直位置；
>
> 可选值：
>
> >`start`：对齐容器的起始边框；
> >
> >`end`：对齐容器的结束边框；
> >
> >`center`：容器内部居中；
> >
> >`stretch`：项目大小没有指定时，拉伸占据整个网格容器；
> >
> >`space-around`：每个项目两侧的间隔相等，项目之间的间隔比项目与容器边框的间隔大一倍；
> >
> >`space-between`：项目与项目的间隔相等，项目与容器边框之间没有间隔；
> >
> >`space-evenly`：项目与项目的间隔相等，项目与容器边框之间也是同样长度的间隔；

#### grid-auto-columns && grid-auto-rows

> 当项目的指定位置在现有网格的外部，浏览器会自动生成多余的网格，以便放置项目；
>
> `grid-auto-columns`和`grid-auto-rows`用来设置浏览器自动创建的多余网格的列宽和行高；
>
> 写法与`grid-template-columns`和`grid-template-rows`完全相同；

#### grid-template && grid

> `grid-template`属性是`grid-template-columns`、`grid-template-rows`和`grid-template-areas`这三个属性的合并简写形式；
>
> `grid`属性是`grid-template-rows`、`grid-template-columns`、`grid-template-areas`、 `grid-auto-rows`、`grid-auto-columns`、`grid-auto-flow`这六个属性的合并简写形式；

### 项目属性

#### grid-column-start && grid-column-end && grid-row-start && grid-row-end

> 定义项目边框所在网格线；
>
> 若项目重叠，则使用`z-index`属性指定项目的重叠顺序；

#### grid-column && grid-row

> `grid-column`属性是`grid-column-start`和`grid-column-end`的合并简写形式；
>
> `grid-row`属性是`grid-row-start`属性和`grid-row-end`的合并简写形式；

#### grid-area

> 指定项目放在哪一个区域；
>
> 可用作`grid-row-start`、`grid-column-start`、`grid-row-end`、`grid-column-end`的合并简写形式；
>
> ```css
>  grid-area: <row-start> / <column-start> / <row-end> / <column-end>;
> ```
>
> 

#### justify-self && align-self && place-self 属性

> 设置单元格内容的水平位置，垂直位置；
>
> 可选值：
>
> > `start`：对齐单元格的起始边缘。
> >
> > `end`：对齐单元格的结束边缘。
> >
> > `center`：单元格内部居中。
> >
> > `stretch`：拉伸，占满单元格的整个宽度（默认值）。



