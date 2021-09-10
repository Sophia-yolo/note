## HTML、XHTML和HTML5

### XHTML

1. XHTML标签必须闭合。
2. XHTML标签以及属性必须小写
3. XHTML标签属性必须用引号
4. XHTML标签用 id 属性代替name属性

### HTML5

HTML5可以省略属性值的属性：

| 省略形式 |                       |
| -------- | --------------------- |
| checked  | checked=nchecked"     |
| readonly | readonly="readonly"   |
| defer    | defer="defer"         |
| ismap    | ismap="ismap"         |
| nohref   | nohref="nohref"       |
| noshade  | noshade="noshade"     |
| nowrap   | nowrap="nowrap"       |
| selected | selected="selected"   |
| disabled | ciisabled="disableci" |
| multiple | multiple="multiple"   |
| noresize | noresize="disabled"   |





## 语义化标签

都有兼容性的问题（IE9+以上版本的浏览器）

> 注意：
>
> * 主要针对搜索引擎的
> * 可以多次使用
> * 在IE9中，需转换成块级元素：`display: block`
> * 语义化标签，在移动端支持比较友好

**header** 头部标签

**nav** 导航标签

**article** 内容标签

**section** 定义文档某个区域

**footer** 尾部标签

**aside** 侧边栏标签

**figure**可视化信息及其标题标签 "多媒体标签"

**figcaption**标签

![image-20210909160102894](https://i.loli.net/2021/09/09/bkdywmUcHLZG6BV.png)

```html
<figure>  
    <img src="roundhouseDestruction.jpeg" alt="Photo of Camper Cat executing a roundhouse kick">  <br>  
    <figcaption>Master Camper Cat demonstrates proper form of a roundhouse kick.</figcaption></figure>
```



## 多媒体标签

#### 音频：<`audio`>

语法：

```html
<audio src="文本地址" controls="controls"></audio>
```

```html
<audio controls="controls" width="300">
	<source src="move.ogg" type="video/ogg">
	<source src="move.mp4" type="video/mp4">
</audio>
```

![img](https://i.loli.net/2021/09/09/ynTcJpkl84zQdRF.png)

属性：

> - **autoplay：autoplay**；视频自动播放（谷歌浏览器需要添加`muted`来解决自动播放问题）
> - **controls：controls；**向用户显示播放控件
> - **loop：loop；**循环播放
>
> - **src：url；**



#### 视频：<`video`>⭐

语法：

```html
<video src="文本地址" controls="controls"></video>
```

```html
<video controls="controls" width="300">
	<source src="move.ogg" type="video/ogg">
	<source src="move.mp4" type="video/mp4">
</video>
```

![img](https://i.loli.net/2021/09/09/FPdims5BwcOW7Dt.png)

属性：

> - **autoplay：autoplay**；视频自动播放（谷歌浏览器需要添加muted来解决自动播放问题）
> - **controls：controls；**向用户显示播放控件
> - **width：单位px；**
> - **height：单位px；**
> - **loop：loop；**循环播放
> - **preload：auto（预先加载视频）/none（不应加载视频）**
> - **src：url；**
> - **poster：Imgurl；**加载等待的画面图像
> - **muted：muted；**静音播放



### 总结

- 音频标签与视频标签使用基本一致
- 多媒体标签在不同浏览器下情况不同，存在兼容性问题
- 谷歌浏览器把音频和视频标签的自动播放都禁止了
- 谷歌浏览器中视频添加 muted 标签可以自己播放
- 注意：重点记住使用方法以及自动播放即可，其他属性可以在使用时查找对应的手册





## 新增的input类型

属性值：

> 1. emall / url / date / time / month / week / **number**（限制属性）
>
> 2. **tel**：手机号码
> 3. **search**：搜索框
> 4. color：生成一个颜色选择表单

**HTML5表单属性**：

- required：required；必填
- **placeholder：提示文本；**默认不显示
- autofocus：autofocus；自动聚焦属性
- autocomplete：off/on；默认之前所填写的字段，同时加上name属性，同时成功提交
- **multiple：multiple；**可以多选文件提交



## 新增表单属性

![img](https://i.loli.net/2021/09/09/8AQ439SCV5yqxZR.png)

