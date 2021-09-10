## 变量

Sass使用$符号来声明变量

```sass
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

`$font-stack` 和 `$primary-color`输出为标准的`CSS`,并把变量值写入`CSS`中.

-------当我们需要在`CSS`中多次输入同一颜色值的时候------------

```sass
body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}
```



## 嵌套

需要注意的是,过度使用Sass嵌套会写出不易维护,而且不合理的`CSS`.

```sass
nav {  
	ul {    
		margin: 0;    
		padding: 0;    
		list-style: none;  
	}   
	li { display: inline-block; }   
	a {    
		display: block;    
		padding: 6px 12px;    
		text-decoration: none;  
	} 
}
```



## Sass部分组成文件

组成文件就是创建一个Sass文件,并且名字前面带有下划线

```sass
 _partial.scss
```

Sass部分组成文件用 @import 导入



## 导入

有两个Sass文件,`_reset.scss` and `base.scss`.我们想把`_reset.css`引入`base.scss`文件中:

```sass
// _reset.scss

html,
body,
ul,
ol {
   margin: 0;
  padding: 0;
}
```

```sass
// base.scss

@import 'reset';

body {
  font: 100% Helvetica, sans-serif;
  background-color: #efefef;
}
```



## 混入

`mixin`功能让我们把想重用的`CSS`声明组成一个可重用的组,甚至还可以传入数值,让我们的`mixin`功能更有扩展性.

一个用`mixin`功能添加浏览器前缀的例子:

```sass
@mixin border-radius($radius) {
  -webkit-border-radius: $radius;
     -moz-border-radius: $radius;
      -ms-border-radius: $radius;
          border-radius: $radius;
}

.box { @include border-radius(10px); }
```

在例子中,创建`minxin`,首先要写`@minxin`标识符,然后命名为border-radius,在圆括号()内写入变量$radius,这样就可以传入半径值.

创建`mixin`后,我们就可以把它作为`CSS`声明用,使用@include方式调用 *(@include空格加上`mixin`名字和里面的实参)*。



## 继承

这是Sass中最有用的功能,使用@extend 让我们从一个选择器中共用`CSS`属性到另一个选择器.在我们的例子中,我们将创建一个包含错误,警告,成功的简单的系列提示信息

```sass
.message {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

.success {
  @extend .message;
  border-color: green;
}

.error {
  @extend .message;
  border-color: red;
}

.warning {
  @extend .message;
  border-color: yellow;
}
```