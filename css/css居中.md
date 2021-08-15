### 空白缝隙的解决方案

1. 物理删除空隙——去掉HTML中的空格
2. 使用margin负值——不适合大规模
3. 使用`font-size:0`

```
.parent {
	font-size:0;
}
.child {
	font-size:16px;
}
```

	4. 使用letter-spacing或者word-spacing（类似于上一条）



# Html

```html
<div class="parent" style="width: 200px; height: 200px; background-color: red;"> 
    <div class="child" style="height: 100px; width: 100px; background-color: blue;">
        DEMO
    </div>
 </div>
```



# 垂直居中

### table-cell + vertical-align

> 多行文字垂直居中

```css
.child{
    display: table-cell;
    vertical-align: middle;
}
```





# 水平居中

### table + margin

> 适用于单元素

(或设置为其他块级元素，==前提设置宽度width==，不然会拉伸成父元素的宽度)

<!--在child div的内容过长时拓展不好-->

```css
<!--宽度默认由内容决定，兼容IE8-->
.child {
    display:table;
    margin: auto;
}
```



### margin

> 此方法只能进行水平居中，且对浮动元素或绝对定位元素无效。
>
> - 如果没有设置 **width** 属性(或者设置 100%)，居中对齐将不起作用。

```css
.child {
    margin:0 auto;
}
```



### float

若居中的元素为浮动元素

```css
.child {
    float:left;
    position:relative;
    left:50%;
    margin-left:-50px;
}
```



### fit-content（行内元素）

```html
 <div class="parent"> 
    <div class="child">
        DEMO
    </div>
 </div>
```

```css
.parent{
    background-color: red;
    width: fit-content;		// 父元素的宽度随子元素的内容而定
    margin: auto;
}
```





# 水平垂直居中

### flex 布局

> 特点：
>
> 1. `Flexbox` 是 `CSS3` 新增属性
> 2. 设计初衷是为了解决像垂直居中这样的常见布局问题
> 3. 适用于子元素浮动、绝对定位、内联元素，均可水平居中,元素高度未知。
> 4. 只需把要处理的块元素的父级设置就可
>

方式一：

```css
.parent {
  display: flex;
  justify-content: center;	/* 水平居中 */
  align-items: center;		/* 垂直居中 */
}
```

方式二：

```css
.parent{
	display: flex;
}
.child{
	margin: auto;
}
```

方式三：

```css
.parent{
	display: flex;
}
.child{
	align-self: center;	/* 垂直居中 */
    margin: auto;
}
```



### 定位

```css
.parent{
    position: relative;
}
.child{
    position: absolute;                
    left: calc(50% - 50px);
    top: calc(50% - 50px);
}
```



### 定位 + transform

> 宽度默认由内容决定，优点是居中的元素不会对其他元素产生影响，脱离正常流
>
> 特点：
>
> 1. 内容可自适应
> 2. 可以封装为一个公共类
> 3. 可做弹出层
> 4. 可能干扰其他 transform 效果
>
> 1. 使用场景：元素高度未知
>
> 2. 优点：适用于子元素为浮动，绝对定位，内联元素

```css
.parent {
  position:relative;
}
.child {
  position: absolute;	/*参照物是父容器*/
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%); 
}
```



### 定位 + margin: 负值

> 特点：
>
> 1. 良好的跨浏览器特性,兼容 `IE6 - IE7`
> 2. 灵活性差，不能自适应
> 3. 宽高不支持百分比尺寸和 min-/max- 属性

```css
.parent{
    position: relative;
}
.child {
    position: absolute;
    top: 50%;
    left: 50%;
    margin-top: -50px;
    margin-left: -50px;
}
```



### 定位 + margin: auto

> 优点：
>
> - 可以实现在正中间
> - 还可以在正左方，正右方
> - 元素的宽高支持百分比 % 属性值和 min-/max- 属性
> - 可以封装为一个公共类，可做弹出层
> - 浏览器支持性好
>
> 缺陷： 
>
> - 定位元素必须有固定的宽高

```css
.parent{
    position: relative;
}
.child {
    position: absolute;	
    /* // 设置 top、bottom，元素就抓到可用空间 */
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    margin: auto;
} 
```



### 文本内容居中（行内元素）

```css
.child{
  /*高度设为文字父容器的高度*/
    line-height: 100px;		/* // 实现垂直居中,适用于单行文字,若是p元素则还要设置：margin: 0; */
    text-align: center;		/* // 实现水平居中,相对于行内块元素有效果*/
}
```



### padding

> 父元素不能设置固定高度，子元素不能设置固定宽度

```css
.parent{
    padding: 20px;
}
```



### 伪元素

> 好处：子元素居中不需要特别设定高度

```css
.parent {
    font-size: 0;
    text-align:center;	/* 与子元素display: inline-block配合使用，可实现水平居中 */
    background-color: red;
}
.parent::before{
    content: '';
    width: 0;
    height: 100%;
    display: inline-block;
    vertical-align: middle;
}
.child{
    font-size: 15px;
    display:inline-block;
    vertical-align: middle;
    background-color: blue;
}
```



### calc(宽高相等)

```css
.child {
  padding: calc((100% - 100px) / 2);		/*  子元素的大小和父元素的大小一样 */
  background-clip: content-box;			/* 让背景颜色只对content生效，而不对padding生效 */
}
```



### table-cell 

> - 适用于子元素 display 为 `inline-block`, `inline` 类型的元素
> - 需要已知父元素的宽高，且父元素的宽高不能设为百分比数。
>

```
.parent {
  display: table-cell;
  vertical-align: middle;
  text-align: center;
}

.child {
  display: inline-block;
}
```



### grid

```css
.parent{
    display: grid;
}
.child{
    align-self: center;
    justify-self: center;
}
```



### margin + transfrom

```css
.parent{
    overflow: hidden;
}
.child{
    margin: 50% auto;
    transform: translateY(-50%);
}
```





### inline-block + vertical-align

> 子元素中的文字水平垂直居中，子盒子水平居中

```css
.parent{
    text-align: center;
}
.child{
    display: inline-block;
    vertical-align: middle;
    line-height: 100px;
}
```



