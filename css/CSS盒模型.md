### CSS盒模型

> CSS将页面内的所有元素都设置为一个矩形的盒子，对页面的布局即将指定的盒子摆放到指定的位置；
>
> 盒子模型：
>
> <img src=".\image\boxModel.PNG" width="80%" height="80%">

#### 内容区（content）

> 内容区大小有`width`和`height`两个属性来设置；
>
> `width`：设置内容区的宽度；
>
> `height`：设置内容区高度；
>
> 内容区大小影响盒子大小

#### 边框（border）

> 盒子的边界；
>
> 要设置边框，至少设置三个样式：
>
> > 1. 边框的宽度   `border-width`；
> >
> >    > 可以用来设置4个方向的宽度，上、右、下、左；
> >    >
> >    > 可以单独指定某一方向边框宽度：`border-xxx-width`；
> >
> > 2. 边框的颜色   `border-color`；
> >
> >    > 如果不指定，默认使用`color`的值；
> >
> > 3. 边框的样式   `border-style`；
> >
> >    > 常用 `border-style`值：
> >    >
> >    > > solid：实线；
> >    > >
> >    > > dotted：点状虚线；
> >    > >
> >    > > dashed：线状虚线；
> >    > >
> >    > > double：双线；
> >    >
> >    > 默认值为none，表示没有边框
>
> 边框的大小会影响整个盒子的大小；
>
> 可以单独设置某一方向的边框：`border-top`、`border-right`、`border-bottom`、`border-left`
>
> `box-shadow`：水平偏移 垂直偏移 模糊半径 阴影颜色；
>
> `border-radius`：设置边框圆角，值为半径大小；
>
> `outline`与`border`:
>
> > `outline`与`border`用法一样，但是不影响布局；

#### 内边距（padding）

> 内容区和边框之间的距离；
>
> 四个方向的内边距： `padding-top`  、 `padding-right` 、`padding-bottom`、`padding-left`;
>
> 内边距的设置会影响整个盒子的大小；
>
> 内边距的颜色是内容区`background-color`的延伸；

#### 外边距（margin） 

> 外边距不影响盒子可见框大小，但是影响盒子位置（和其它盒子之间的距离）；
>
> 四个方向的外边距： `margin-top`  、  `margin-right` 、`margin-bottom`、`margin-left`;
>
> 可以设置正值也可以设置负值；
>
> 元素设置左、上外边距移动元素自身，设置下、右外边距移动其它元素；
>
> 外边距的设置影响盒子实际占用空间的大小





