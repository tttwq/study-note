## 水平垂直居中

### 水平居中

#### 行内元素

1. 父元素是块元素：

   > ``` css
   > .father{
   >     text-align: center;
   > }
   > ```

2. 父元素不是块元素：

   > ```css
   > .father{
   >     display: block;
   > 	text-align: center;
   > }
   > ```

#### 块元素

##### 通过盒模型

1. 元素宽度确定：

   > ```css
   > .son{
   > 	margin: 0 aoto;
   > }
   > ```

2. 元素宽度不确定：

   > 将元素设置为`inline-block`或`inline`；
   >
   > ```css
   > .father{
   > 	display: block;
   > 	text-align: center;
   > }
   > .son{
   >     display: inline-block/inline;
   > }
   > ```

##### 通过定位

设置父元素为相对定位，再设置子元素为绝对定位，子元素的`left: 50%`;

1. 元素宽度确定：

   > 设置子元素的`margin-left`：- 元素宽度的一半；
   >
   > ```css
   > .father{
   > 	position: relative;
   > }
   > .son{
   >     width: 100px;
   >     position: absolute;
   >     left: 50%;
   >     margin: -50px;
   > }
   > ```
   >
   > 

2. 元素宽度不确定：

   > 利用`transform`属性；
   >
   > ```css
   > .father{
   >     position: relative;
   > }
   > .son{
   >     position: absolute;
   >     left: 50%;
   >     transform: translateX(-50%);
   > }
   > ```

##### 通过flexbox布局

```css
.father{
    display: flex;
    justify-content: center;
}
```

### 垂直居中

#### 行内元素

##### 单行

设置行内元素的行高等于盒子的高；

```css
.father{
    height: 100px;
}
.son{
    line-height: 100px;
}
```

##### 多行

利用table-cell布局；

```css
.father{
    display: table-cell;
    vertical-align: center;
}
```

#### 块元素

##### 通过定位

设置父元素为相对定位，再设置子元素为绝对定位，子元素的`top: 50%`;

1. 元素高度确定：

   > 设置子元素的 `margin-top`: -元素高度的一半；
   >
   > ```css
   > .father{
   >     height: 100px;
   >     position: relative;
   > }
   > .son{
   >     position: absolute;
   >     top: 50%;
   >     margin-top: -50px;
   > }
   > ```

2. 元素高度不确定：

   > 利用`transform`属性；
   >
   > ```css
   > .father{
   >     position: relative;
   > }
   > .son{
   >     position: absolute;
   >     top: 50%;
   >     transform: translateY(-50%);
   > }
   > ```

##### 通过flexbox布局

```css
.father{
    display: flex;
    align-items: center;
}
```

### 水平垂直居中

#### 已知高度和宽度

设置父元素为相对定位，再设置子元素为绝对定位，通过`margin`；

1. 

   > ```css
   > .father{
   >     position :relative;
   > }
   > .son{
   >     width: 100px;
   >     height: 100px;
   >     position: absolute;
   >     top: 0;
   >     right: 0;
   >     bottom: 0;
   >     left: 0;
   >     margin: auto;
   > }
   > ```

2. 

   > ```css
   > .father{
   >     position: relative;
   > }
   > .son{
   >     position: absolute;
   >     top: 50%;
   >     left: 50%;
   >     margin-top: -50px;
   >     margin-left: -50px
   > }
   > ```
   >
   > 

#### 未知高度和宽度

##### 通过定位

通过`transform`属性；

```css
.father{
    position: relative;
}
.son{
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translateX(50%) translateY(50%);
}
```

##### 通过flexbox布局

```css
.father{
    position: flex;
    justify-content: center;
    align-items: center;
}
```

## 两列自适应布局

一列由内容撑开，另一列撑满剩余宽度；

### 传统布局

`float`+`overflow`

1. 一列设置`float`，其宽度由内容撑开（避免该列中的子元素为块元素，独占一行，影响布局）；
2. 另一列不被浮动元素覆盖，且撑满剩余宽度 —— 开启BFC；
3. 兼容IE6浏览器 —— `zoom: 1`

```html
<div class="box">
		<div class="left">
			<p>left</p>
		</div>
		<div class="right">
			<p>right</p>
			<p>right</p>
		</div>
	</div>
```

```css
.box{
			width: 500px;
			margin:50px auto;
			border: 1px solid #000;
		}
		.left{
			background-color: pink;
			float: left;
			margin-right: 10px;

		}
		.right{
			background-color: purple;
			overflow: hidden;
			zoom: 1;
		}
```

效果如下：

<img src="./image/2column-float.png">

### flexbox布局

1. 开启flex布局；
2. 设置第二列撑满整个宽度 ——`flex`属性；

```css
.box{
			width: 500px;
			margin:50px auto;
			border: 1px solid #000;
			display: flex;
		}
		.left{
			background-color: pink;
			margin-right: 10px;

		}
		.right{
			background-color: purple;
			flex: 1;
		}
```

效果如下：

<img src="./image/2column-flex.png">

### grid布局

1. 开启grid布局；
2. 分配网格（设置列和列宽） —— `grid-template-columns`；

```css
.box{
			width: 500px;
			margin:50px auto;
			border: 1px solid #000;
			display: grid;
			grid-template-columns: auto 1fr;
		}
		.left{
			background-color: pink;
			margin-right: 10px;

		}
		.right{
			background-color: purple;
		}
```

效果如下：

<img src="./image/2column-grid.png">

## 三栏布局

中间列自适应宽度，旁边两侧固定宽度；

### 浮动布局

左边栏`float:left`，右边栏`float:left`，中间栏开启BFC；

避免浮动栏掉到下一行，需要修改dom结构；

注意父元素高度塌陷；

```html
<div class="box">
		<div class="left">
			<p>left</p>
		</div>
		
		<div class="right">
			<p>right</p>
		</div>
		<div class="center">
			<p>center</p>
			<p>center</p>
		</div>
	</div>
```

```css
.box{
			width: 500px;
			margin:50px auto;
			border: 1px solid #000;
		}
		.box::after{
			content: '';
			display: table;
			clear: both;
		}
		.left{
			background-color: pink;
			float: left;
			width: 100px;
			margin-right: 10px;
		}
		.center{
			background-color: yellow;
			overflow: hidden;
		}
		.right{
			background-color: purple;
			float: right;
			width: 100px;
			margin-left: 10px;
		}
```

效果如下：

<img src="./image/3column-float.png">

### 绝对定位布局

每一列都开启绝对定位，给每一栏设置定位；

由于开启绝对定位，元素完全脱离文档流和文本流，父元素会出现高度塌陷的问题，在高度未知的情况下，若想撑起父元素，只能通过js实现；

```html
<div class="left">
		<p>left</p>
	</div>
	<div class="center">
		<p>center</p>
		<p>center</p>
	</div>
	<div class="right">
		<p>right</p>
	</div>
```

```css
.left{
			background-color: pink;
			width: 200px;
			position: absolute;
			left: 0;
		}
		.center{
			background-color: yellow;
			position: absolute;
			left: 210px;
			right: 210px;
		}
		.right{
			background-color: purple;
			width: 200px;
			position: absolute;
			right: 0;
		}
```

效果如下：

<img src="./image/3column-position.png">

### flexbox布局

父元素开启flex布局；

中间栏填满整个宽度 ——`flex`属性；

IE9以下不支持；

```css
	.box{
			width: 500px;
			margin: 50px auto;
			border: 1px solid #000;
			display: flex;
		}
		.left{
			background-color: pink;
			width: 100px;
			margin-right: 10px;
		}
		.center{
			background-color: yellow;
			flex: 1;
		}
		.right{
			background-color: purple;
			width: 100px;
			margin-left: 10px;
		}
```

效果如下：

<img src="./image/3column-flex.png">

### 表格布局

表格布局兼容性好，但不支持设置栏边距；

内容溢出时会自动撑开父元素；

```css
.box{
			width: 500px;
			margin: 50px auto;
			border: 1px solid #000;
			display: table;
		}
		.left{
			background-color: pink;
			width: 100px;
			display: table-cell;
		}
		.center{
			background-color: yellow;
			display: table-cell;
		}
		.right{
			background-color: purple;
			width: 100px;
			display: table-cell;
		}
```

效果如下：

<img src="./image/3column-table.png">

### grid布局

开启grid布局；

分配网格（设置列和列宽） —— `grid-template-columns`;

IE10+上支持，而且也仅支持部分属性；

```css
.box{
			width: 500px;
			margin: 50px auto;
			border: 1px solid #000;
			display: grid;
			grid-template-columns: 110px 1fr 110px;
		}
		.left{
			background-color: pink;
			margin-right: 10px;
		}
		.center{
			background-color: yellow;
		}
		.right{
			background-color: purple;
			margin-left: 10px;
		}
```

效果如下：

<img src="./image/3column-grid.png">

### 圣杯布局

dom结构中先写中间栏，实现中间栏的优先加载；

步骤：

> 1. 三个部分都设置浮动，实现三栏处于同一行；
> 2. 中间栏宽度设为100%，实现宽度自适应；
> 3. 通过设置 `margin-left `为负值让侧边栏与中间栏同一行；
> 4. 父元素设置` padding`，在左右两边留出间隙；
> 5. 设置相对定位，让 侧边栏移动到两边；

中间的最小宽度如果小于左边栏的宽度，左侧栏会掉到下一行；

如果其中一列内容高度拉长，其他两列的背景并不会自动填充；

```html
<div class="box">
		<div class="center">center</div>
		<div class="left">left</div>
		<div class="right">right</div>
	</div>
```

```css
.box{
			width: 300px;
			margin: 50px auto;
			border: 1px solid #000;
			padding: 0 110px;
		}
		.box::after{
			content: '';
			display: table;
			clear: both;
		}
		.left{
			background-color: pink;
			height: 100px;
			width: 100px;
			float: left;
			margin-left: -100%;
			position: relative;
			left: -110px;

		}
		.center{
			background-color: yellow;
			height: 200px;
			float: left;
			width: 100%;
		}
		.right{
			background-color: purple;
			height: 100px;
			width: 100px;
			float: left;
			margin-left: -100px;
			position: relative;
			right: -110px
		}
```

效果如下：

<img src="./image/3column-sb.png">

### 双飞翼布局

圣杯布局的优化

步骤：

> 1. 三个部分都设置浮动，实现三栏处于同一行；
> 2. 中间栏宽度设为100%，实现宽度自适应；
> 3. 通过设置 `margin-left `为负值让侧边栏与中间栏同一行；
> 4. 中间层增加一个内层div，并设置`margin`；

会多加一层 dom 树节点，增加渲染树生成的计算量；

```html
<div class="box">
		<div class="center">
			<div class="inner">center</div>
		</div>
		<div class="left">left</div>
		<div class="right">right</div>
	</div>
```

```css
.left{
			background-color: pink;
			height: 100px;
			width: 100px;
			float: left;
			margin-left: -100%;
		}
		.center{
			float: left;
			width: 100%;
		}
		.inner{
			background-color: yellow;
			height: 100px;
			margin: 0 100px;
		}
		.right{
			background-color: purple;
			height: 100px;
			width: 100px;
			float: left;
			margin-left: -100px;
		}
```

效果如下：

![sfy](D:\note\css\image\3column-sfy.PNG)

## 等高布局

### 伪等高

1. 用边框模拟

   > 用左右两边的边框伪装左右两个兄弟元素的背景；
   >
   > 左右两个元素设置透明背景色，并定位至中间元素边框上；

   左右两侧内容高度不能大于中间元素内容高度，否则无法撑开容器高度；

2. 利用背景图片`background-image`和平铺方式`background-repeat`；

3. 利用正padding+负margin

   > 背景在 padding 区域显示，设置一个大数值的 padding-bottom填充背景颜色;
   >
   > 设置相同数值的负的 margin-bottom，保证盒模型大小不变;
   >
   > 在所有列外面加上一个容器，设置` overflow:hidden `切掉溢出背景；

   当背景图定位再底部时，会看不到背景图；

### 真等高

#### table

`table-cell`元素默认等高

```css
.box{
			display: table;
			width: 100%;
			table-layout: fixed;
		}
		.left,.right{
			display: table-cell;
		}
		.center{
			display: table-cell;
		}
```

#### absolute

> 设置子元素的`top`、`bottom`为0，使所有子元素与父元素高度相同；
>
> ```css
> .box{
> 			width: 100%;
> 			height: 100px;
> 			position: relative;
> 		}
> 		.left,.right{
>             position: absolute;
> 			top: 0;
> 			bottom: 0;
> 			width: 100px;
> 		}
> 		.center{
>             margin: 0 20px;
> 			position: absolute;
> 			top: 0;
> 			bottom: 0;
> 			left: 100px;
> 			right: 100px;
> 			width: 200px;
> 		}
> 		.left{
> 			left: 0;
> 		}
> 		.right{
> 			right: 0;
> 		}
> ```

#### flex

flex中`align-items`默认值为`stretch`，项目默认拉伸为父元素高度，实现等高；

#### grid

通过网格实现等高；