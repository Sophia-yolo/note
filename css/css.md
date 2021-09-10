## 浏览器私有前缀

| 私有前缀 |        代表含义         |
| :------: | :---------------------: |
|  -moz-   | Firefox 浏览器私有属性  |
|   -ms-   |    IE 浏览器私有属性    |
| -webkit- | Safari、Chrome 私有属性 |
|   -o-    |     Opera 私有属性      |



## CSS规范

#### 空格规范

1. 选择器与 { 之变包含空格；
2. 属性名与之后的:不能包含空格，属性值与前面的：必须包含空格；

#### 选择器规范

- 并集选择器的每个选择器必须都独占一行

#### 属性规范

1. 属性另起一行
2. 属性定义后必须有分号结束

##### 属性基本顺序

1. **布局定位属性**：display/position/float/clear/visibility/overflow
2. **自身属性**：width/height/margin/padding/border/background
3. **文本属性**：color/font/text-decoration/text-align/white-space/break-word
4. **其他属性（css3）**：content/curson/border-radius/box-shadow/text-shadow/background：linear-gradient



##  CSS样式表

#### 行内式

**（内联样式）**

- 基本语法：

  **<标签名 style="属性1:属性值1;  属性2:属性值2;  属性3:属性值3;">内容**

- 缺点：没有实现样式分离。

#### 内部样式表

**（内嵌样式表）**

- 只能控制当前页面

- 基本语法： 

  ```css
  <style type="text/css">        //type="text/css"在html5中可以省略`
  	选择器  {
  		属性1:属性值1；
  		属性2:属性值2;`
  		属性3:属性值3;`
  	} 	     
  </style>   
  ```


#### 外部样式表

**（外链式）**

- 将所有样式放在一个或多个.css为扩展名的外部样式表文件中，通过link标签（单标签）将外部样式表链接到HTML中

- 基本语法：

  ```css
  <head>
  <link rel="stylesheet(表示被链接文档是样式表文件)"   type="text/css"  href="url(css文件路径)" />  
  </head>
  ```

  

##  CSS选择器⭐

#### 基础选择器

> 1. 选择器通常是您需要改变样式的 HTML 元素。
>
> 2. 每条声明由一个属性和一个值组成。

#### 新增选择器👉css3

类选择器、属性选择器、伪类选择器权重为**10**



#### 标签选择器

- 也称元素选择器，即以 html 标签作为 css 修饰所用的选择器。可以把**某一类(同类)标签全部选择**出来。
- 语法格式：**`S`{属性1:属性值1;    属性2:属性值2;   属性3:属性值3;}**（S为选择器名）。



#### 类选择器

- 用于描述一组元素的样式，class 选择器有别于id选择器，class可以在多个元素中使用。
- 语法格式：**`.S`{属性1:属性值1;    属性2:属性值2;   属性3:属性值3;}**（S为了类名）。
- HTML用法：class="类名"
- 特殊用法（多类名）：**<标签名  class="类名1   类名2">内容**



#### id 选择器

- 可以为标有特定 id 的 HTML 元素指定特定的样式**,具有唯一性。**
- 语法格式：**`#S`{属性1:属性值1;    属性2:属性值2;   属性3:属性值3;}**（S为了id名）。
- HTML用法： id="类名"。



#### 属性选择器👉css3

语法形式为：[ 属性=属性值]

> 1. E[att]	选择具有att属性的E元素
>
> 2. E[att="val"]	选择具有att属性且属性值等于val的E元素
>
> 3. E[att^="val"]	选择具有att属性且属性值以val开头的E元素
>
> 4. E[att$="val"]	选择具有att属性且属性值以val结尾的E元素



#### 通配符选择器

- 语法形式为：**`*`{属性：属性值}**。它的作用是匹配 html 中的所有元素标签。



#### 后代选择器

- 指定目标选择器必须处在某个选择器对应的元素内部，
- 语法格式：**`.A B`{...}** （A为类名，B为标签。A为外层标签，B为内层标签）。
- 这种形式：**`A B`{...}**的形式（A，B是标签，表示对处于A中的B标签有效）。



#### 子元素选择器

- 类似于后代选择器，指定目标选择器必须处在某个选择器对应的元素内部，
- 两者区别在于后代选择器允许"子标签"甚至"孙子标签"及嵌套更深的标签匹配相应的样式，而SS强制指定目标选择器作为 包含选择器对应的标签 内部的标签，
- 语法格式：**`A>B`{...}**（A、B为HTML元素/标签）。



#### 交集选择器

- 既是...又是的关系
- 语法格式：**`A.B`{...}**（.B 为类名，A为标签）。



#### 并集选择器⭐

- 通常用于集体声明
- 语法格式：**`A,B`{...}**（A、B为HTML元素/标签或任何形式的选择器）



#### 伪类选择器⭐

- 用于向某些选择器添加特殊的效果（lvha顺序不可改）

- 语法格式：（a为标签，因为a链接浏览器具有默认样式，所以实际中要单独指定样式）

  |   语句    |          含义           |
  | :-------: | :---------------------: |
  |  a:link   |    未访问链接的状态     |
  | a:visited |   已访问的链接的状态    |
  |  a:hover  | 鼠标移动到链接上的状态⭐ |
  | a:active  |     选定的链接状态      |



#### 结构伪类👉css3

根据**文档结构**来选择器元素，常用于根据父级选择器里面的子元素。

> 1. E:first-child——匹配父元素中的第一个子元素
>
> 2. E:last-child——匹配父元素中的最后一个E元素
>
> 3. E:nth-child(n)——匹配父元素中的第n子元素E：一个或多个—会把所有元素排个序号
>
> >  ✍even偶数(2n)、odd奇数(2n+1)
> >
> >  ✍nth-child(n)代表选择了所有孩子
> >
> >  ✍n+5  第五个（包含5）到最后
>
> 4. E:first-of-type——指定类型E的第一个
>
> 5. E:last-of-type——指定类型E的最后一个
>
> 6. E:nth-of-type(n)——指定元素排列序号





#### 伪元素选择器👉css3

利用css创建一个新标签元素，属行内元素，before和after必须有content属性

`::before`——在元素内部的前面插入内容

> 格式如下：

```
A:before {
	content:" ";
}
```

`::after`——在元素内部的后面插入内容

使用场景：

* 字体图标
* 视频经过
* 清除浮动



#### 兄弟选择器

- 语法格式：**`A~B`{...}**（选择元素后面的多个元素）

- 语法格式：**`A+B` {...}**（选择某个元素的后面的元素）



##  CSS标签显示模式

#### 块级元素

- 常见块元素有 `h1~h6`、`p`、`div`、`ul`、`ol`、`li`

- 特点：

  > 1. 独占一行；
  > 2. 宽度、高度、外边距和内边距都可以控制
  > 3. 宽度默认为容器的100%
  > 4. 是一个容器及盒子，可以行内元素或块元素

- 注意：文字类块级标签不能放块元素。

#### 行内元素

- 常见的行内元素有：`a`、`strong`、`b`、`em`、`i`、`del`、`s`、`ins`、`u`、`span`等

- 特点：

  > 1. 相邻行内元素在一行上，一行可以显示多个；
  > 2. 高、宽直接设置是无效的；
  > 3. 默认宽度就是它本身内容的宽度；
  > 4. 行内元素只能容纳文本或其他行内元素

#### 行内块元素

- 常见的有：`img` 、`input` 、`td`

- 特点：

  > 1. 和相邻元素在一行上，但是之前会有空白缝隙。一行可以显示多个
  > 2. 默认宽度就是他本身内容的宽度
  > 3. 高度、行高、外边距以及内边距都可以控制

#### display转换

- 块转行内：`display:inline`;
- 行内转块：`display:block`;
- 块、行内元素转换为行内块：`display:inline-block`;

#### 元素的显示与隐藏

##### display显示⭐

1. 先隐藏对象
2. 不保留位置

> 1. display：none；隐藏对象
>
> 2. display：block；（除了转换为块级元素之外，同时显示位置）

##### visibility（可见性）

> 显示或隐藏元素而不更改文档的布局

|  属性值  |            含义            |
| :------: | :------------------------: |
| inherit  |   继承上一个对象的可见性   |
| visible  |          对象可视          |
|  hidden  |     隐藏对象；保留位置     |
| collapse | 主要用于隐藏表格中的行和列 |

##### overflow溢出

| 属性值  |                  含义                  |
| :-----: | :------------------------------------: |
| visible |        不剪切内容，不添加滚动条        |
|  auto   | 超出自动显示滚动条，不超出不显示滚动条 |
| hidden  |        不显示超过对象尺寸的内容        |
| scroll  |             总是显示滚动条             |

##### opacity透明度

CSS 里的`opacity`属性用来设置元素的透明度。

> 1. 值 1 代表完全不透明。
> 2. 值 0.5 代表半透明。
> 3. 值 0 代表完全透明。



##  CSS文本样式

#### 长度单位

##### PX

相对长度单位，相对于屏幕的分辨率

px 特点

- 优点：稳定 & 精确
- 缺点：改变浏览器字体大小，布局会被打破

px 作用

- 给定具体大小，协助em和rem重写具体单位

##### EM

相对长度单位，相对于当前元素的文本尺寸,如果当前元素文本尺寸未设置则相对于浏览器默认字体尺寸

特点：

1. em值不固定; 
2. 首先查找自己有无设置 font-size
3. 会继承父类字体大小

- 注意(通常 `1em=16px`)👉html默认字体就是16px

  1. body选择器中声明

     ```
     Font-size=62.5%；
     
     em值变为 16px*62.5%=10px
     ```

  2. 将你的原来的`px`数值除以10，然后换上`em`作为单位；

  3. 重新计算那些被放大的字体的em数值。避免字体大小的重复声明。



##### REM

**root em**：相对长度单位,只相对于HTML根元素

特点：

- 优点：只需修改根元素大小就可以成比例地调整所有字体大小,且避免了字体大小逐层复合的连锁反应，且IE8+的浏览器都支持
- Tip：为应对不支持的浏览器,可以多写一个绝对单位的声明，例如：

```css
p {
   font-size:14px; 
   font-size:.875rem;
}
```

- 总结：rem对应px的值取决于html元素字体大小，此大小会被浏览器中字体大小的设置影响，除非显示重写一个具体单位.

作用：

- 保证无论用户如何设置自己的浏览器，布局都能调到合适大小
- 维护用户拥有自己体验偏好的权利



##### %

- 特点：
  - 普通元素的百分比定位基于父类.
  - 设置了position: fixed的元素的百分比定位基于浏览器窗体.
  - 设置了position: absolute的元素的百分比定位相对于static定位以外第一个父元素进行定位.



##### vw

`viewport width, viewport指的是浏览器内部可视区域大小`

- 特点：
  - 计算： `1vw = 1% * width_viewport`



##### vh

`viewport height`

- 特点：
  - 计算： `1vh = 1% * height_viewport`



##### vm

`viewport min`

- 特点：
  - 计算： `1vm = 1% * (width<height?width: height)`

- 实际使用：

  - 元素**严格不可缩放**时，使用`px`
  - 一切可扩展都应该用`rem`, 包括媒体查询
  - 千万不要用`em`控制字体的大小
  - `em`用于缩放一些没有默认字体大小的元素，当字体变大整个组件也能随之变大
  - 多列布局用`%`较好
  - `vw`、`vh`、`vm`做



#### font

综合性写法(严格按照顺序写font）：**font:font-style     font-weight**    **font-size/line-height**    **font-family**;

|        属性        | 含义                                                  |
| :----------------: | :---------------------------------------------------- |
|     font-size      | 字号大小                                              |
|    font-family     | 字体（若指定多个字体，中间以逗号隔开）                |
|    font-weight     | 指定字体的粗细（normal=400、bold=700...无单位100~900) |
|     font-style     | 文本的字体样式（normal(标准)、italic(斜体））         |
| white-space:nowrap | 让文字强制一行内显示                                  |

font-family

说明：

字体名指的是“微软雅黑”、“宋体”、“Times New Roman”等。

举例：`“font-family:微软雅黑;”`

- [Google 字体](https://fonts.google.com/)是一个免费的字体库，可以通过在 CSS 里面设置字体的 URL 来引用。

- ```css
  <link href="https://fonts.googleapis.com/css?family=Lobster" rel="stylesheet" type="text/css">
  ```




#### color

|      属性值       |       含义       |
| :---------------: | :--------------: |
|        red        |  颜色名称的颜色  |
| #ff0000——简写#f00 | 十六进制值的颜色 |
|   rgb(255,0,0)    |  rgb 代码的颜色  |

> **颜色半透明：color：rgba（r，g，b，a）a是alpha（透明）的意思，取值0-1**





| 属性            | 说明                           |
| --------------- | ------------------------------ |
| text-decoration | 下划线、删除线、顶划线         |
| text-transform  | 文本大小写                     |
| font-varient    | 将英文文本转换为“小型”大写字母 |
| text-indent     | 段落首行缩进                   |
| text-align      | 文本水平对齐方式               |
| line-height     | 行高                           |
| letter-spacing  | 字间距                         |
| word-spacing    | 词距                           |



#### text-alight

| 属性值 | 含义               |
| :----: | ------------------ |
|  left  | 左对齐left（默认） |
| right  | 右对齐             |
| centor | 居中对齐           |

`text-align="justify"`

- 每一行被展开为宽度相等，左，右外边距是对齐（如杂志和报纸）。

- 也可以使行内元素和行内快元素居中对齐



#### text-index

属性值可为不同单位的数值、em字符宽度的倍数、或相对浏览器窗口宽度的百分比%，允许使用负值。

- 通常我们用于段落首行缩进2个字的距离 
- text-index：2em；



#### text-decoration

用来设置或删除文本的装饰。

|    属性值    | 含义   |
| :----------: | ------ |
|     none     | 无     |
|    blink     | 闪烁   |
|   overline   | 上划线 |
| line-through | 贯穿线 |
|  underline   | 下划线 |



#### text-shadow

语法描述：text-shadow：水平阴影  垂直阴影  模糊距离（虚实）    阴影颜色 ，...... ；

|  value   |                                  |
| :------: | -------------------------------- |
| h-shadow | 水平阴影的位置，允许负值（必需） |
| v-shadow | 垂直阴影的位置，允许负值（必需） |
|   blur   | 模糊距离（可选）                 |
|  color   | 阴影颜色（可选）                 |



#### text-transform

| Value        | Result                                   |
| :----------- | :--------------------------------------- |
| `lowercase`  | "transform me"  \|  转换为小写           |
| `uppercase`  | "TRANSFORM ME"  \|  转换为大写           |
| `capitalize` | "Transform Me"  \|  开头第一个字母为大写 |
| `initial`    | 使用默认值                               |
| `inherit`    | 使用父元素的`text-transform`值。         |
| `none`       | **Default:**不改变文字。                 |





#### 边框样式

##### 边框属性

边框样式属性指定要显示什么样的边界。

综合性写法(没有顺序)：`boder:boder-width;boder-style;boder-color;`

**border-style**（边框的样式）

| 属性值 | 含义             |
| :----: | ---------------- |
|  none  | 默认无边框       |
| dotted | 定义一个点线边框 |
| dashed | 定义一个虚线边框 |
| solid  | 定义实线边框     |

**border-width** （边框指定宽度）

1. 可以指定长度值 ，比如 2px 或 0.1em(单位为 px, pt, cm, em 等)
2. 也可thick 、medium（默认值） 和 thin。

**border-color** （边框的颜色）

**表格的细线边框**：`boder-collapse:collapse`（表示相邻边框合并在一起）



##### 边框局部样式

边框可以单独指定样式：上边框  下边框  左边框  右边框

<（在指定一条边框时，可以先boder:none在单独设置边框。）>

1. 上边框border-top
2. 下边框border-bottom
3. 左边框border-left
4. 右边框border-right



#### 单行文字溢出显示省略号

条件：

> 1. 强制一行内显示文本；white-spsce：nowrap（normal自动换行）； 
>
> 2. 超出的部分隐藏；overflow：hidden； 
> 3. 文字用省略号替代超出的部分;text-overflow：ellipsis；

多行文字溢出显示省略号

1. 有较大兼容问题
2. 适合与webkit浏览器或移动端

代码：

1. ```
   超出的部分隐藏；overflow：hidden；
   ```

2. ```
   文字用省略号替代超出的部分;text-overflow：ellipsis；
   ```

3. ```
   弹性伸缩盒子模型显示：display：-webkit-box； 
   ```

4. ```
   限制在一个块元素显示的文本的行数：-webkit-line-clamp：2；
   ```

5. ```
   设置或检索伸缩盒对象的子元素的排列方式：-webkit-box-orient：vertical；
   ```

   



##  CSS外观属性👉css3

### filter 

|     用法     | 含义                                       |
| :----------: | ------------------------------------------ |
| grayscale()  | 设置灰度，1是百分之百                      |
| brightness() | 设置亮度，默认为1，正常亮度                |
|   sepia()    | 设置褐色，1是百分之百褐色，正常为0         |
|    blur()    | 设置模糊度，单位像素                       |
|  contrast()  | 设置对比度，正常是1；0为无对比度，变为灰色 |
|  saturate()  | 设置饱和度                                 |
|   invert()   | 胶片底色效果                               |
| hue-rotate() | 色相旋转                                   |



### animation(动画) 

1. 定义动画

```css
@keyframs 动画名称 {
	//第一种写法
		from {
			......
		}
		to {
			......
		}
	//第二种写法
		0% {
			......
		}
		100% {
			......
		}
}
```

2. 调用动画

|           value           | 含义                                                         |
| :-----------------------: | ------------------------------------------------------------ |
|         @keyframe         | 规定动画                                                     |
|         animation         | 动画名称  持续时间  运动曲线  播放次数  是否反方向   动画起始或者结束的状态 |
|      animation-name       | 动画名称                                                     |
|    animation-duration     | 持续时间（s/ms)                                              |
| animation-timing-function | 运动曲线，默认是 “ease”                                      |
|      animation-delay      | 何时开始                                                     |
| animation-iteration-count | 重复次数（infinity无限次）                                   |
|    animation-direction    | 是否反方向播放（默认：normal，反方向：alternate）            |
|    animation-fill-mode    | 动画结束后的状态（保持：forward，回到起始：backwards）       |
|   animation-paly-state    | 规定动画是否在运行或暂停（默认running，暂停：pause           |

动画序列

> - 0% 是动画的开始，100% 是动画的完成。这样的规则是动画序列
> - 在 @keyframes 中规定某项 css样式，就能创建由当前样式逐渐改为新样式的动画效果
> - 可以改变任意多的样式、任意多的次数

动画简写

```css
animation: 动画名称  持续时间  运动曲线  播放次数  是否反方向   动画起始或者结束的状态
```

> - 简写属性里卖弄不包含 animation-play-status
> - 暂停动画：animation-play-status: puased  经常和鼠标经过等其他配合使用
> - 



### 过渡⭐ 

```css
transition：要过渡的属性	花费时间(单位：s)	运动曲线(默认ease)	何时开始；(与hover搭配使用)
```

- transition-property：要过渡效果的属性
- transition-duration：过渡时间长度
- transition-timing-function：运动曲线

> 1. ease：(默认值)，从慢到快在慢
>
> 2. linear：设置线性速度，匀速 = cubic-bezier( 0.25 , 0.25 , 0.75 , 0.75 )；
>
> 3. ease-in：从慢到快
>
> 4. ease-out：从快到慢 = cubic-bizier( 0 , 0 , 0.58 , 1 )
>
> 5. cubic-bezier(X1, Y1, X2, Y2)：贝塞尔曲线
>
> 6. step()：指定了时间函数中间隔数量（步长）"分几步完成动画"

**贝塞尔曲线实现杂耍球运动**

​	下面的例子模拟了杂耍球运动：

```
cubic-bezier(0.3, 0.4, 0.5, 1.6);
```

注意 y2 的值是大于 1 的。虽然贝塞尔曲线是在 1*1 的坐标系统内 x 值只能在 0 到 1，但是 y 值是可以大于 1 的。这样才能模拟杂耍球运动。

- transition-delay：设置延迟时间



### 转换

> transform

设置透明度：opacity:##;

#### `2D`转换

注意：

- 同时使用多个转换

```css
transform: translate() rotate() scale()
```

- 顺序会影响转换的效果
- 当同时有位移和其他属性的时候，记得要将位移放到最前



> 特点：
>
> 1. 不会影响到其他的位置
> 2. translate中的百分比的那位是相对与自身元素的 translate: (50%,50%)
> 3. 对行内标签没有作用

移动

```css
transform: translate(x,y)；
```

- 水平移动  -->  `x`代表水平移动的距离（translateX()）
- 竖直移动  -->  `y`代表垂直移动的距离（translateY()） 

旋转

> 重点
>
> 1. rotate中的读书，单位是 deg ，比如 `rotate(45deg)`
> 2. 角度为正时，顺时针；角度为负时，为逆时针
> 3. 默认旋转的中心的是元素的中心点

```css
transform: rotate(#deg)；—绕中心点旋转
```

> 元素沿着 X 轴（横向）翻转指定的角度——`transform:skewX/y(#deg);`

设置元素旋转的中心点：

```css
transform-origin: x y;		//参数可以百分比、像素、或者是方位名词
```

> 重点：
>
> 1. 参数 x 和 y 需要用空格隔开
> 2. x y 默认转换的中心点是元素的中心点（50%, 50%）
> 3. 还可以给 x y 设置像素或者 方位名词（top bottom left right cneter）

缩放

> 特点：
>
> 1. 不会影响其他盒子
> 2. 可以设置缩放的中心点

```css
transform:scale(x, y)	// x 为宽度，y 是高度
```

🌰：

```css
transform: scale(2, 1)	// 修改宽度为原来的2倍，高度不变
transform: scale(0.5)	// 等比例缩放
```



#### `3D`转换

> 特点：
>
> 1. 近大远小
> 2. 物体后面遮挡不可见

三维坐标：

- x 轴——水平向右
- y 轴——垂直向下
- z 轴——垂直屏幕

<img src="C:\Users\Area1\AppData\Roaming\Typora\typora-user-images\image-20210910153345034.png" alt="image-20210910153345034" style="zoom: 33%;float: left" />

位移(`2D` + Z轴)

```css
transform: translateZ()		// 需要用到透视
```

> 简写形式：`transform: translate3d(x, y, z)`	——=="x，y，z 不可以省略，没有就写0"==

透视

> 也称为视距，即是人的研究到屏幕的距离	“==近大远小==”

```css
perspective: 12px;
```

<img src="https://i.loli.net/2021/09/10/kDVBtf2YLA8rTXU.png" alt="image-20210910160830534" style="zoom:50%;" />

> 透视写在被观察元素的==父盒子==上
>
> - d：就是视距
> - z：就是 z 轴，物体距离屏幕的距离，z 轴越大(正值)，我们看到的物体距离就越大

旋转

```css
transform: rotate3d(X,Y,Z,##deg)；
```

- transform: rotateX(`45deg`)	——沿着 x 轴正方向旋转45度
- transform: rotateY(`45deg`)	——沿着 y 轴正方向旋转45度
- transform: rotateZ(`45deg`)	——沿着 z 轴正方向旋转45度

==rotateX==旋转方向

> 左手准则：
>
> - 左手的手拇指指向 x 轴的正方向
> - 其余手指的弯曲方向就是该元素沿着 x 轴旋转的方向

![image-20210910235550041](https://cdn.jsdelivr.net/gh/wiwth/note/img/202109110016097.png)

 ==rotateY==旋转方向		“类似钢管舞”

> 同左手准则

![image-20210910163216991](https://i.loli.net/2021/09/10/z5kbQY8dRqUEl74.png)

==rotateZ==旋转方向		“类似抽奖盘”

------

`3D`呈现

> 设置在父元素上，保留子元素3d效果
>
> - 控制子元素是否开启三维立体环境

```css
transform-style: preserve-3d;	// 子元素开启立体空间，默认是flat(不开启3d立体空间)
```





### 圆角边框

代码：

boder-radius：ength； （填写数值或百分比=50%“表示高度和宽度的一半”）

圆角矩形：boder-radius：高度的一半；

圆角矩形可以分别为四个角设置圆度，但是有顺序

1. boder-top-left-radius：
2. boder-top-right-radius：
3. boder-bottom-right-radius：
4. boder-bottom-left-radius：

总结：boder-radius：左上  右上  右下  左下；

### 字体图标

方式：

1. Unicode
2. font-class
3. symbol



##  CSS背景

background：背景颜色、背景图片地址、背景平铺、背景滚动、背景位置

#### linear-grafient()——线性渐变

语法：

```css
background: linear-gradient(gradient_direction, 颜色 1, 颜色 2, 颜色 3, ...);
```

第一个参数指定了颜色过渡的方向 - 它的值是角度，90deg 代表垂直渐变，45deg 的渐变角度和反斜杠方向差不多。剩下的参数指定了渐变颜色的顺序：

例子：

```css
background: linear-gradient(90deg, red, yellow, rgb(204, 204, 255));
```

#### linear-gradient()——重复指定的渐变

- 角度就是渐变的方向。
- 起止渐变颜色值代表渐变颜色及其宽度值，由颜色值和起止位置组成
- 起止位置用百分比或者像素值表示。

在下列例子里，渐变开始于 0 像素位置的`yellow`，然后过渡到距离开始位置 40 像素的`blue`。由于下一个起止渐变颜色值的起止位置也是 40 像素，所以颜色直接渐变成第三个颜色值`green`，然后过渡到距离开始位置 80 像素的`red`。

下面的代码可以帮助理解成对的起止渐变颜色值是如何过渡的：

> 0px [黄色 -- 过渡 -- 蓝色] 40px [绿色 -- 过渡 -- 红色] 80px

```
background: repeating-linear-gradient(
      45deg,
      yellow 0px,
      yellow 40px,
      black 40px,
      red 80px
    );
```



#### 背景颜色

**background-color**：颜色值（默认：transparent（透明的 ）），页面的背景颜色使用在body的选择器中

- 色相
  - hsl( 色相（hue）、饱和度（saturation）、亮度（lightness）);
  - **色相**是色彩的基本属性，就是平常所说的颜色名称，如红色、黄色等。以颜色光谱为例，光谱左边从红色开始，移动到中间的绿色，一直到右边的蓝色，色相值就是沿着这条线的取值。在`hsl()`里面，色相用色环来代替光谱，色相值就是色环里面的颜色对应的从 0 到 360 度的角度值。
  - **饱和度**是指色彩的纯度，也就是颜色里灰色的占比，越高色彩越纯，低则逐渐变灰，取0-100%的数值。
  - **亮度**决定颜色的明暗程度，也就是颜色里白色或者黑色的占比，100% 亮度是白色， 0% 亮度是黑色，而 50% 亮度是“一般的”。



#### 背景图像

| 属性                  | 说明                                         |
| --------------------- | -------------------------------------------- |
| background-image      | 定义背景图像的路径                           |
| background-repeat     | 定义背景图像显示方式，例如纵向平铺、横向平铺 |
| background-position   | 定义背景图像在元素哪个位置                   |
| background-attachment | 定义背景图像是否随内容而滚动                 |



##### background-image

- background-image：url / none（url不要加" ")



##### background-repeat

1. **repeat**：背景图片在纵向和横向向上平铺，"平铺"
2. **no-repeat**：背景图片不平铺
3. **repeat-x**：背景图片在横向向上平铺
4. **repeat-y**：背景图片在纵向平铺



##### background-position⭐

- 必须指定background-image属性
- **background-position：length**||**length（**百分数|由浮点数字和单位标识符组成的长度值）
- **background-position：position**  **position（top**|**center**|**bottom**|**left**|**center**|**right**方位名词，与顺序无关，若指定一个方位名词，另一个值默认居中对齐**）**
- **background-position：x坐标  y坐标；（**若指定一个数值，那该数值一定是x坐标，另一个值默认垂直居中**）**



##### 背景附着

- **background-attachment：scroll（**背景图像随对象内容滚动，默认**）/fixed（**背景图像固定**）**



##### 背景透明

- **background：rgba(r,g,b,a) **a是alpha（透明）的意思，取值0-1**
- css3版本



##### 图片底侧空白缝隙解决方案

1. 给图片添加vertical-align：midder\top\bottom等（提倡）
2. 把图片转换成块级元素display：block；



##  CSS三大特性

#### css层叠性

- 就近原则 

#### css继承性

-  子承父业（text-	  font-   line-   color)

#### css优先级

🔔权重计算公式

- 选择器相同，则执行层叠性。
- 同类型，同级别的样式后者先于前者 
- !important  ∞>>  style"行内样式表"  `1,0,0,0`  >>  id选择器  `0,1,0,0`)  >  每个类(伪类、class类选择器)、属性选择器 `0,0,1,0`  >>  标签选择器 |  伪元素选择器  `0,0,0,1`  >>  继承 | *  `0,0,0,0`

🔔权重叠加

> 比如结果为：1093 比 1100，按位比较，从左到右，只要一位高于则立即胜出， 否则继续比较。

- 注意：数位之间没有进制
- 继承的权重是0（修改标签的样式时）
  - 若标签选中，则按公式计算权重，执行样式
  - 若没有选中，则权重为0。





## 盒子模型

![image-20210730102300255](https://i.loli.net/2021/07/30/bYvhrHFCBe4Gw8y.png)

|      内容       | 含有                               |
| :-------------: | :--------------------------------- |
| Margin(外边距)  | 清除边框外的区域，外边距是透明的。 |
|  Border(边框)   | 围绕在内边距和内容外的边框。       |
| Padding(内边距) | 清除内容周围的区域，内边距是透明的 |
|  Content(内容)  | 盒子的内容，显示文本和图像。       |

**`内盒尺寸大小计算=内容的宽度和高度+内边距+外边距+边框`**

**布局稳定性**：width>padding>margin



#### 清除元素默认的内外边距

代码：`*{    padding：0；    margin：0； }`

注意：行内元素为了照顾兼容性，最好只设置**左右内外边距**，不要设置上下内外边距。



### padding

——内边距样式

> - 左内边距(padding-left)  
> - 右内边距(padding-right)  
> - 上内边距(padding-top)  
> - 下内边距(padding-bottom)

简写：

- `padding：属性1，属性2，属性3，属性4`（上->右->下->左(顺时针)）

- `padding：属性1，属性2，属性3`（上->左右->下）

- `padding：属性1，属性2`（上下->左右）

- `padding：属性1`（上下左右属性）


特殊情况:若盒子没有宽度，若指定padding-left或padding-right不撑开盒子。



### margin

**外边距样式**：控制盒子与盒子之间的距离 "用法与padding类似"

> - 左外边距(margin-left)  
> - 右内边距(margin-right)  
> - 上内边距(margin-top)  
> - 下内边距(margin-bottom)    

**margin负值有利于页面布局：**

让每个盒子移动-1px，刚好压住相邻盒子边框

鼠标经过某个盒子时，提高当前盒子的层级。（若没有定位则加相对定位(保留位置)；若有定位则加z-index）



#### 外边距合并

🔸相邻块元素垂直外边距合并（外边距塌陷）

- 当上下两个元素相邻时，上元素有margin-bottom，下元素有margin-top，则它们的垂直间距为两个值中的较大值。
  - 解决方法：尽量只给一个盒子添加外边距

🔸嵌套块元素垂直外边距合并（塌陷）👉解决方案

- 为父元素定义上边框，颜色设置transparent（透明）

- 为父元素定义上内边距
- 为父元素添加**overflow:hidden**
- 还有浮动、固定、绝对定位等方法。



### 边框border



### 盒子阴影👉css3

用法：`box-shadow：水平阴影  垂直阴影  模糊距离（虚实）  阴影尺寸（影子大小）  阴影颜色  内外阴影`

> h-shadow：水平阴影的位置，允许负值（必需）；
>
> v-shadow：垂直阴影的位置，允许负值（必需）；
>
> blur：模糊距离（可选）；
>
> spread：阴影尺寸（可选）；
>
> color：阴影颜色（可选）；
>
> inset：将外阴影转换成内阴影（可选），默认outset；

`box-shadow`属性的每个阴影依次由下面这些值描述：

- `offset-x`阴影的水平偏移量；
- `offset-y`阴影的垂直偏移量;
- `blur-radius`模糊距离；
- `spread-radius`阴影尺寸；
- 颜色。

术语表：blur-radius => 模糊半径，spread-radius => 辐射半径，transparent => 透明的，border-radius => 圆角边框。



### 盒子宽度

|          用法           | 含义                                            |
| :---------------------: | ----------------------------------------------- |
| width：calc(100%-80px)  | 可以使用+-*/计算                                |
| box-sizing：content-box | 盒子大小（默认）                                |
|  box-sizing：boder-box  | 盒子大小为width<br />width=width+padding+border |

`content-box` 是默认值。

> eg：盒子的宽度 = css中设置的width + border + padding

`border-box` 

> 内容区的实际宽度会是width减去border + padding的计算值。

eg：盒子的宽度 = css设置的宽度width

> (包含其它的border和padding)



## **css**用户界面样式

### 鼠标样式cursor

**{ cursor：属性值；}**

|   属性值    |     含义     |
| :---------: | :----------: |
|   default   | 小白（默认） |
|   pointer   |     小手     |
|    move     |     移动     |
|    text     |     文本     |
| not-allowed |     禁止     |



### 表单轮廓outline

- 添加outline或outline：none；样式之后就可以取消默认的蓝色边框。



### 防止拖曳文本域

- textarea{ **resize**：none；}



### 图片样式

#### 图片大小width和height

> - width：像素值;
> - height：像素值;

PS：可以使用width和height来定义你想要的高度和宽度

#### 图片边框border

> - border-width：像素值;
> - border-style：属性值;
> - border-color:颜色值;

#### 图片水平对齐text-align

#### 图片垂直对齐vertical-align

设置图片或者表单（行内块元素）和文字垂直对齐

属性值：

- baseline：基线对齐，元素位置默认放在父元素的基线上；
- top：把元素的顶端行中最高元素的顶端对齐
- middle：把此元素放置在父元素的中部
- bottom：把元素的顶端行中最低元素的顶端对齐



### 列表样式

#### list-style-type

有序列表

| 属性值      | 说明                     |
| ----------- | ------------------------ |
| decimal     | 默认值，数字1、2、3……    |
| lower-roman | 小写罗马数字i、ii、iii…… |
| upper-roman | 大写罗马数字I、II、III…… |
| lower-alpha | 小写英文字母a、b、c……    |
| upper-alpha | 大写英文字母A、B、C……    |

无序列表

| 属性值 | 说明              |
| ------ | ----------------- |
| disc   | 默认值，实心圆“●” |
| circle | 空心圆“○”         |
| square | 实心正方形“■”     |

> list-style-type：none;

#### 自定义列表项符号list-style-image

> list-style-image：url(图像地址);



### 表格样式

#### 表格边框合并border-collapse

| border-collapse属性值 | 说明                               |
| :-------------------- | :--------------------------------- |
| separate              | 默认值，边框分开，不合并           |
| collapse              | 边框合并，如果相邻，则共用一个边框 |

#### 表格边框间距border-spacing

> border-spacing：像素值;

#### 表格标题位置caption-side

| caption-side属性值 | 说明               |
| :----------------- | :----------------- |
| top                | 默认值，标题在顶部 |
| bottom             | 标题在底部         |

