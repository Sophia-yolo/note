## 骨架格式

```html
<!DOCTYPE html>                      //声明为HTML5 
<html>                               //根标签 
<head>                           //包含文档元数据 	
<meta charset="utf-8">  
  	//定义网页编码格式为UTF-8,charset字符集，常用的字符集有UTF-8、gbk、gb2312 
    <title>文档标题</title>               //描述文档标题 
</head>  
<body>                 //包含页面内容 	
    文档内容...... 
</body>  
</html>
```

```html
 <meta name="viewport" content="width=device-width,initial-scale=1.0">
```

**注意：**对于中文网页需要使用`meta charset="utf-8"`*声明编码，否则会出现乱码。*

- **lang属性**：en英文，zh-CN中文.`html lang="en"`
- 项目描述  `meta name="description"  content=" "`
- 搜索关键词  `meta name="keywords"  content=" "`
- 项目标签图标  `link rel="shortcut icon" href="favicon.ico" type="image/x-icon"`

| head内部标签 | 说明                                   |
| :----------: | :------------------------------------- |
|   <title>    | 定义网页的标题                         |
|    <meta>    | 定义网页的基本信息（供搜索引擎）       |
|   <style>    | 定义CSS样式                            |
|    <link>    | 链接外部CSS文件或脚本文件              |
|   <script>   | 定义脚本语言                           |
|    <base>    | 定义页面所有链接的基础定位（用得很少） |

## 标签

### 排版标签

**（显示网页结构，用于网页布局）**

- **h**元素标题元素,HTML 标题（Heading）是通过 h1 - h6 标签来定义的，`h1`定义最大的标题**, ** `h6`定义最小的标题。
- **p**元素段落标签, `<p >文本内容/<p>`>定义一个段落。
- **hr** 元素（单标签）可用于分隔内容,`hr/`定义水平线
- **br**元素(单标签），强制换行
- **div**元素是块级元素，它可用于组合其他 HTML 元素的容器。一行只能放一行div
- **span**元素，**文本**一行可以用好几个span

### 文本格式化标签✍

- **b**元素定义加粗文本，strong 的意思是 "强调"。**strong**使用更多，语义更强烈。
- **em**元素加重字体，**i**元素定义斜体字。**em**使用更多，语义更强烈。
- **s**元素和**del**元素使文字以加删除线方式显示。**del**使用更多，语义更强烈
- **u**元素和**ins**元素使文字以加下划线方式显示。**ins**使用更多，语义更强烈
- **sup**设置上标，**sub**设置下标



### 图像标签⭐ img

语法如下：

```html
 <img src="" alt="" title="" width="">
```

- **src**属性（属性值：url）描述图像路径。
- **alt**属性（属性值：文本）描述不能显示时的替换文本。
  > alt=“ ”时，即alt设为空，通常不会被屏幕阅读器处理
  >
  > alt=“XXX”，无图片是**显示文本内容XXX**
- **title**属性（属性值：文本）鼠标悬停时显示的内容
- **width**属性，height属性修改图像大小，用于设置图像的高度与宽度，属性值：像素

### 链接标签⭐ a

语法如下

```html
<a href="跳转目标" target="-目标窗口的弹出方式"> 文本或图像 </a>
```

- **href**属性，作用：用于指定链接目标的url地址，（必须属性）当为标签应用href属性

- **target**属性，用于指定链接的打开方式

- | target属性值 | 说明                           |
  | :----------- | :----------------------------- |
  | _self ⭐      | 默认方式，即在当前窗口打开链接 |
  | _blank ⭐     | 在一个全新的空白窗口中打开链接 |
  | _top         | 在顶层框架中打开链接           |
  | _parent      | 在当前框架的上一层里打开链接   |

### div ✊span ✊ label

> > - div是块元素，可以包含任何块元素和行内元素，不会与其他元素位于同一行
> > - span 是行内元素，可以与其他行内元素位于同一行。
>
> > - div常用于页面中较大块的结构划分，然后配合CSS来操作
> > - span 一般用来包含文字等, 它没有结构的意义，纯粹是应用样式。当其他行内元素都不适合的时候，可以用span来配合CSS 操作。
>
> > - div和span是无语义标签，但label 是有语义标签。
> > - label 只适用于表单中，用于显示在输入控件旁边的说明性文字。

### 块元素和行内元素

1. 常见块元素有：h1~h6、p、hr、div等。
2. 常见行内元素有：strong、em、span等。

### 注释

> 快捷键：ctrl+?或ctrl+shift+/

### **预格式标签pre**

（不常用，不好控制）：按照原先规划好的文字格式显示页面，保留空格和换行等。

### **特殊符号**

特殊符号表：http://www.lvyestudy.com/html/special-symbols

​			空格——&nbsp；

```html
	    <——&lt；
	    >——&gt；
	   ........
```

### 标签属性

- 标签可以拥有多个属性，必须写在开始标签中，位于标签名后面。
- 属性之间不分先后顺序，标签名与属性、属性与属性之前均以空格分开。
- 属性总是以名称/值对的形式出现，**比如：name="value"**。

### time—datetime👉HTML5

- `time`是一个行内标签，用于在页面中呈现日期或时间
- `datetime`属性保存了日期的有效格式，辅助设备可以访问这个值。

通过标准化时间格式，即使时间在文本中是以非正式的或口语化的形式编写，辅助设备依然可以获取准确的时间和日期。

举个例子：

```html
<time datetime="2013-02-13">last Wednesday</time>, which ended in a draw.
```

### accesskey 属性

> ——在链接之间快速导航（html）

HTML 提供`accesskey`属性，用于指定激活标签或者使标签获得焦点的快捷键。

HTML5 允许在任何标签上使用这个属性。该属性对于交互类标签（如链接、按钮、表单控件等）十分有用。

举个例子：

```html
<button accesskey="b">Important Button</button>
```

### tabindex属性

当它在标签上时，表示标签可以获得焦点。它的值**可以是零、负整数及正整数**，并决定了标签的行为。

当用户在页面中使用 tab 键时，有些标签，如：链接、表单控件，可以自动获得焦点。它们获得焦点的顺序与它们出现在文档流中的顺序一致。我们可以通过将`tabindex`属性值设为 0，来给其他标签赋予相同的功能，如：`div`、`span`、`p`等。举个例子：

```html
<div tabindex="0">I need keyboard focus!</div>
```

**注意：**
`tabindex`属性值为负整数（通常为 -1）的标签也是有焦点的，只是不可以通过 tab 键来获得焦点。这种方法通常用于以编程的方式使内容获得焦点（如：激活用于弹出框的`div`标签），但是它超出了当前挑战的范围。

> 使用 tabindex 指定多个元素的键盘焦点顺序
>
> > - `tabindex`属性值为 1 的标签将首先获得键盘焦点，
> > - 然后焦点将按照指定的`tabindex`的值（如：2，3 等）的顺序进行移动，
> > - 直到回到默认的或`tabindex`值为 0 的标签上，如此循环。



## 路径⭐❗

- 目录文件夹：根目录

### 相对路径

当保存于不用目录的网页引用同一个文件时，所使用的路径将不相同。

> - 同一级的相对路径：只需输入图像的名称即可
> - 下一级的相对路径（“儿子”）：同级文件夹/图像名称
> - 上一级的相对路径：../（../../......"两级")图像所处文件夹/图像名称

### 绝对路径

- 当所有网页引用同一个文件夹时，所使用的路径都是一样的（不提倡用），或完整的网页地址。

分类：1.常规元素（双标签） 2.空元素（单标签）

关系：1.嵌套关系（“父子关系”）  2.并列关系（“兄弟关系”）

应用：排版标签 文本格式标签 图像标签  链接 相对路径，绝对路径的使用

### 描点定位

1.找目标:使用相应的id名标注跳转位置

2.使用`<a href="#id名>链接文本(被点击)</a>`

### base元素

1.base可以设置整体链接的打开状态

2.base写到`<head></head>`



## 表格👉table

作用：常见显示、展示表格式数据

| 标签  | 语义                          | 说明   |
| :---- | :---------------------------- | :----- |
| table | table（表格）                 | 表格   |
| tr    | table row（表格行）           | 行标签 |
| td    | table data cell（表格单元格） | 单元格 |

### **创建**表格

```html
<table >             //定义一个表格标签   
<tr>                                      //行标签        
    <td>Header 1</td>          //一个单元格，就像一个容器，可以容纳所有元素        
    <td>Header 2</td>    
</tr> 
</table>
```

### 属性

> 1. **boder**表格边框（默认boder="0")   width表格宽度   height表格高度
>
> 2. **alight**设置表格在网页中的水平对齐方式：left、right、center（居中对齐）
>
> 3. **cellspacing**设置单元格和单元格的距离
>
> 4. **cellpadding**设置单元格内容与单元格边框的距离



### 表格结构

| 标签  | 语义         | 说明           |
| :---- | :----------- | :------------- |
| thead | table head   | 表头           |
| tbody | table body   | 表身           |
| tfoot | table foot   | 表脚           |
| th    | table header | 表头单元格标签 |

表格完整结构

```html
<table>

    <caption>表格标题</caption>

    <!--表头-->
    <thead>
        <tr>
            <th>表头单元格1</th>
    		<th>表头单元格2</th>
        </tr>
    </thead>

    <!--表身-->
    <tbody>
        <!---第一行-->
        <tr>
            <td>标准单元格1</td>
            <td>标准单元格2</td>
        </tr>
        <!---第二行-->
        <tr>
            <td rowspan="2">标准单元格1</td>
            <td>标准单元格2</td>
        </tr>
        <!---第二行-->
        <tr>
            <td>标准单元格1</td>
        </tr>
    </tbody>

    <!--表脚-->
    <tfoot>
        <tr>
            <td>标准单元格1</td>
            <td>标准单元格2</td>
        </tr>
    </tfoot>
</table>
```



### 合并单元格

1. 跨**行**合并：rowspan="合并单元格的个数"
2. 跨**列**合并：colspan="合并单元格的个数"

合并顺序：先上 后下 先左 后右（记得得删除多余的单元格）



## 表单

（收集用户信息）

### input 控件

单标签**type**属性设置不同的属性值用来指定不同的控件类型  

`<input type="属性值"/>`			

> 1. **text **👉单行文本输入框	
> 2. **password **👉 密码输入框	
> 3. **radio **👉 单选按钮：通过相同name可以实现单选
> 4. **checkbox** 👉 复选框
> 5. **button** 👉 普通按钮，需要填写value值=> `<buttom value="submit">`



#### 属性值

**value**属性 ——值  `<input value="值"/>`

| 属性值 | 含义                                |
| :----: | ----------------------------------- |
| submit | 提交按钮                            |
|  rest  | 重置按钮                            |
| image  | 图像形式的提交按钮，必须包含src属性 |
|  file  | 文件域                              |
|  date  | 时间选择器                          |

**name**属性 ——后台可以通过这个名字找到这个表单

**checked**属性——表示默认选中状态，较常见于单选按钮和复选按钮-checked="checked"

**hidden**属性可以隐藏输入框



### **label**标签

——作用：用于绑定一个表单元素，当点击label标签的时候，被绑定的表单元素就会获得输入焦点。

- `<label>文本<input type="属性值" /></label>`
- `<label for="id名">文本</label><input type="属性值"  id="id名" />`



### **textarea**

控件（文本域）：可多行输入文本

`<textarea rows="行数" cols="列数">多行文本框内容</textarea>`



### **select**

下拉列表（少）

<select>                                   //至少包含一对option          
	<option>选项 1</option>          //select="select"时，默认选中项
	<option>选项 2</option>
	.....     
</select>
```css
<select>                                   //至少包含一对option          
	<option>选项 1</option>          //select="select"时，默认选中项
	<option>选项 2</option>
	.....     
</select>
```




### **form表单域**

```css
<form action="url地址"  method="提交方式get"内容显示"/post“内容不显示"   name="表单名称">
		各种单元控件                         //name的重要性 	     
</form>
```



## 列表

（用来布局，自由组合度更高）

| 标签 | 语义            | 说明     |
| :--- | :-------------- | :------- |
| ol   | ordered list    | 有序列表 |
| ul   | unordered list  | 无序列表 |
| dl   | definition list | 定义列表 |

### ul无序列表

```html
<ul>                                   //不能输入其他标签    
    <li>Header 1</li>          //一个容器，可以存放其他元素    
    <li>Header 2</li> 
</ul>
```



### ol有序列表

```html
<ol>                                   //不能输入其他标签    
    <li>Header 1</li>          //一个容器，可以存放其他元素    
    <li>Header 2</li> 
</ol>
```



### dl自定义列表

对术语的解释与描述

```html
<dl>   
    <dt>Header 1</dt>          //名词一    
    	<dd>Header 2</dd>          //名词一的解释    
    <dt>Header 1</dt>          //名词二    
    	<dd>Header 2</dd>          //名词二的解释 
</dl>
```





## 浮动框架iframe

优点：

1. 可以完全由设计者定义宽度和高度，并且可以放置在一个网页的任何位置
2. 在浏览器窗口中嵌套的子窗口，整个页面并不一定是框架页面，但要包含一个框架窗口
3. 可以完全由指定宽度和高度决定。

语法：

```html
<iframe src="浮动框架的源文件" width="浮动框架的宽" height="浮动框架的高"></iframe>
```

PS：src属性是iframe的必须属性，它定义浮动框架页面的源文件地址

### scrolling

——是否显示滚动条

```html
<iframe src="浮动框架的源文件" width="浮动框架的宽" height="浮动框架的高" scrolling="取值"></iframe>
```

| scrolling属性值 | 说明                                                         |
| :-------------- | :----------------------------------------------------------- |
| auto            | 默认值，整个表格在浏览器页面中左对齐                         |
| yes             | 总是显示滚动条，即使页面内容不足以撑满框架范围，滚动条的位置也预留 |
| no              | 在任何情况下都不显示滚动条                                   |



## 语义化

### 标题语义化

1. 一个页面只能有一个h1标签
2. h1~h6之间不要出现断层：即按照“hl、h2、h3、h4”这样的顺序依次 排列下来，不要出现“hl、h3、h4”而漏掉h2的情况。
3. 不要用h1~h6来定义样式
4. 不要用div来代替h1~h6

### 图片语义化

1. **alt**属性和**title**属性
2. **figure** 元素和**figcaption**元素 👉 HTML5

> figure元素用于包含图片和图注，figcaption元素用于表示图注文字

### 表格语义化

PS：对于这种表格数据形式, 最好的选择还是table

### 表单语义化

#### label 标签

> label标签用于显示在输入控件旁边的说明性文字，即将某个表单元素和某段说明文字关联起来

语法：

`<label for=""> 说明性文字 </label>`

说明：

①语义上绑定了 label元素和表单元素。

②增强了鼠标可用性。也就是说我们点击label中的文本时，其所关联的表单元素也会 获得焦点。

关联方式：

```html
<div>
    <input id="cbk" type="checkbox" /><label for="cbk"> 复选框 </label> 
	<label>复选框<input id="cbk" type="checkbox"/></label>
</div>
```

#### fieldset标签和legend标签。

1. 增强表单的语义
2. 可以定义fieldset元素的disabled属性来禁用整个组中的表单元素



通常还会使用`legend`标签来为单选按钮组提供文字说明。屏幕阅读器也可以朗读这些文字。

当选项的含义很明确时，如：性别选择，`fieldset`标签与`legend`标签就可以省略。这时，使用含有`for`属性的`label`标签就足够了。

举个例子：

```html
<form action="index.aspx" method="post">
	<fieldset>
    	<legend>登录绿叶学习网</legend>
                <p>
                    <label for="name"> 账号：</1abel><input type="text" id="name" name="name" />
                </p>
                <label for="pwd"> 密码：</label><input type="password" id="pwd" name="pwd" />
                </p>
                <input type="checkbox" id="remember-me" name="remember-me" /> <label for="remember-me"> 记住我 </label>
                <input type="submit" value="登录" />            
	</fieldset>
```

下面是代码实现的界面：

<form action="index.aspx" method="post">
        <fieldset>
            <legend>登录绿叶学习网</legend>
            <p>
                <label for="name"> 账号：</1abel><input type="text" id="name" name="name" />
            </p>
            <label for="pwd"> 密码：</label><input type="password" id="pwd" name="pwd" />
            </p>
            <input type="checkbox" id="remember-me" name="remember-me" /> <label for="remember-me"> 记住我 </label>
            <input type="submit" value="登录" />
    	 </fieldset>

### 其他语义化

换行符 `<br/>`

无序列表ul

strong标签和em标签

del标签和ins标签

……

