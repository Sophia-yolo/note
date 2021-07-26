## 刷新方式

全局刷新

> 整个浏览器被新的数据覆盖。在网络中传输大量的数据，浏览器需要加载，渲染页面。

局部刷新

> 在浏览器内部发起请求，获取数据，改变页面中的部分内容。 

![局部刷新](assets/Ajax/局部刷新-16272655004291.png)

**Ajax：用于局部刷新的一种技术**



# AJAX 

Asynchronous JavaScript and XML（异步的 JavaScript 和 【XML:可扩展标记语言，被设计用来传输和存储数据】）

![百度局部刷新](assets/Ajax/百度局部刷新-16272655421832.png)

- **Ajax 不是一种新的编程语言，而是一种用于创建更好更快以及交互性更强的Web应用程序的技术。**
- 增加B/S的体验性
- 核心：`XMLHttpRequest`对象（XHR）

> 需要服务器的数据：xml：网络中的传输的数据格式👉`json`



# 优点

1. 可以无需刷新页面而与服务器端进行通信
2. 允许你根据用户事件来更新部分页面内容



# 缺点

1. 没有浏览历史，不能回退
2. 存在跨域问题(同源)
3. `SEO` 不友好



# HTTP协议

https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Overview

## HTTP 请求交互的基本过程

1. 前后应用从浏览器端向服务器发送HTTP 请求(请求报文)
2. 后台服务器接收到请求后, 调度服务器应用处理请求, 向浏览器端返回HTTP响应(响应报文)
3. 浏览器端接收到响应, 解析显示响应体/调用监视回调



## HTTP 请求报文

### 请求行

1. 请求类型：GET / POST
2. 请求路径：url
3. HTTP协议版本：HTTP/1.1 

不同类型的请求及其作用

1. `GET`: 从服务器端**读取**数据（查）
2. `POST`: 向服务器端**添加**新数据 （增）
3. `PUT`: **更新**服务器端已经数据 （改）
4. `DELETE`: **删除**服务器端数据 （删）

POST 请求体参数格式

1. Content-Type: application/x-www-form-urlencoded;charset=utf-8
   用于键值对参数，参数的键值用=连接, 参数之间用&连接
   
   > 例如: name=%E5%B0%8F%E6%98%8E&age=12
   
2. Content-Type: application/json;charset=utf-8
   用于 json 字符串参数

   > 例如: {"name": "%E5%B0%8F%E6%98%8E", "age": 12}

3. Content-Type: multipart/form-data
   用于文件上传请求

### 请求头

1. Host：www.baidu.com
2. Cookie：`BAIDUID=AD3B0FA706E; BIDUPSID=AD3B0FA706;`
3. Content-Type：`application/x-www-form-urlencoded 或者application/json`
4. User-Agent：`chrome 83`

```js
// 设置请求体内容的类型
xhr.setRequesHeader('Content-Type','application/x-www-from-urlencoded');
// 自定义头信息
xhr.setRequesHeader('name', 'ykyk');
```

自定义头信息需要在`server.js`中设置响应头允许自定义请求头 post改成all

```javascript
response.setHeader('Access-Control-Allow-Header','*');
```

### 空行

### 请求体

```
username=tom&pwd=123
{"username": "tom", "pwd": 123}
```

## HTTP 响应报文

### 响应状态行：status statusText

1. 协议版本
2. 响应状态码：404、403、401、500、200
3. 响应状态字符串

常见的响应状态码

1. 200 OK 请求成功。一般用于GET 与POST 请求
2. 201 Created 已创建。成功请求并创建了新的资源
3. 401 Unauthorized 未授权/请求要求用户的身份认证
4. 404 Not Found 服务器无法根据客户端的请求找到资源
5. 500 Internal Server Error 服务器内部错误，无法完成请求

### 多个响应头

1. Content-Type： text/html;charset=utf-8
2. Content-length：2048
3. Content-encoding：gzip
4. Set-Cookie: BD_CK_SAM=1;path=/

### 响应体

> html  文本/json  文本/js/css/图片...



# Express框架

1. 初始化环境

```shell
npm init --yes
```

2. 下载express包

```shell
npm install express --save
```

3. 编写 j s 代码

```js
//引入express
const express = require('express')

//创建应用对象
const app = express()

//创建路由规则
app.get('/',(request,response)=>{
    //设置响应头，设置允许跨域
    response.setHeader('Access-Control-Allow-Origin',"*");
    //设置响应体
    response.send("HELLO!!!!")
})
app.post('/server', (request, response) => {
  // 设置响应头, 设置允许跨域
  response.setHeader('Access-Control-Allow-Origin', '*');
  // 设置响应体
  response.send("Hello Ajax POST");
});

//监听端口启动服务
app.listen(8000,()=>{
    console.log("服务已经启动，8000 端口监听中")
})
```

4. 运行 j s 程序

```js
node server.js
```





# AJAX异步对象步骤

### 创建对象方式

https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest

```js
var xmlHttp = new XMLHttpRequest();
```

### 初始化请求参数

方法：

```
 open(method,url,async) ： 初始化异步请求对象 
```

参数说明： 

- method：请求的类型；GET 或 POST 

- url：服务器的 servlet 地址 

- async：true（异步）或 false（同步） 

  > `xmlHttp.open`(请求方式get|post, "服务器端的访问地址", 同步|异步请求（默认是true，异步请求）)

  ```js
  xmlHttp.open(“get”,”http:192.168.1.20:8080/myweb/query”,true)
  //可以设置请求头，一般不设置
  xmlHttp.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
  ```

###  发送请求

```js
xmlHttp.send(body) //get请求不传 body 参数，只有post请求使用
```

### 绑定事件

`onreadystatechange` ：当异步对象发起请求即 readyState 改变 时，获取了数据都会触发这个事件。 这个事件需要指定一个处理函数 function， 在函数中处理状态的变化。通过判断 XMLHttpReqeust 对象的状态，获取服务端返回的数据。

语法： 

```js
xmlHttp.onreadystatechange= function() {
 	if( xmlHttp.readyState == 4 && xmlHttp.status == 200){
		处理服务器返回数据 
 	}
 }
```

属性说明：

> 一个 js 函数名 或 直接定义函数，每当 readyState 属性 改变时，就会调用该函数

readyState 属性： 

- 0: 请求未初始化，创建异步请求对象 `var xmlHttp = new XMLHttpRequest()` 
- 1: 初始化异步请求对象， `xmlHttp.open(请求方式，请求地址，true)` 
- 2: 异步对象发送请求， `xmlHttp.send()` 
- 3: 服务端返回的部分结果。XMLHttpRequest 内部处理。 
- 4: 异步请求对象已经将数据解析完毕，服务端返回的全部结果

status 属性：

1. 200: "OK" 👉网络请求成功，一般用于GET 与POST 请求
2. 201：“Created”👉 已创建。成功请求并创建了新的资源
3. 401：“Unauthorized”👉 未授权/请求要求用户的身份认证
4. 404: “Not Found”👉服务器无法根据客户端的请求找到资源
5. 500：“Internal Server Error” 👉服务器内部错误，无法完成请求





# JSON使用

  ajax发起请求-------servlet（返回的一个json格式的字符串 { name:"河北", jiancheng:"冀","shenghui":"石家庄"}）
  json分类：

1. json对象 ，JSONObject ,这种对象的格式   名称:值， 也可以看做是 `key:value` 格式。

2. json数组， JSONArray

   > 基本格式 ：
   >
   >  [{ name:"河北", jiancheng:"冀","shenghui":"石家庄"} , { name:"山西", jiancheng:"晋","shenghui":"太原"} ]

为什么要使用 json ：

> 1. json格式好理解
> 2. json格式数据在多种语言中，比较容易处理。 使用java， javascript读写json格式的数据比较容易。
> 3. json格式数据他占用的空间下，在网络中传输快， 用户的体验好。

  处理json的工具库： gson（google）； fastjson（阿里），jackson， json-lib

### json数据请求

```javascript
app.all('/json-server', (request, response) => {
  // 设置响应头, 设置允许跨域
  response.setHeader('Access-Control-Allow-Origin', '*');
  // 设置响应头, 设置允许自定义头信息
  response.setHeader('Access-Control-Allow-Headers', '*');
  // 响应一个数据
  const data = {
    name: 'atguigu'
  };
  // 对 对象 进行 字符串 转换
  let str = JSON.stringify(data)
  // 设置响应体 
  response.send(str);
});

```

```js
 const result = document.getElementById('result');
    // 绑定键盘按下事件
    window.onkeydown = function(){
      // 发送请求
      const xhr = new XMLHttpRequest();
      // *2*.(自动转换) 设置响应体数据的类型(自动转换)
      xhr.responseType = 'json';
      // 初始化
      xhr.open('GET', 'http://127.0.0.1:8000/json-server');
      // 发送
      xhr.send();
      // 事件绑定
      xhr.onreadystatechange = function(){
        if(xhr.readyState === 4){
          if(xhr.status >= 200 && xhr.status < 300){
            console.log(xhr.response);
            // 1. 手动对数据转化 (字符串再转换成json)
            // let data = JSON.parse(xhr.response); //转换成json
            // result.innerHTML = data.name;
            // *2*. (自动转换)自动转换(自动转换)
            result.innerHTML = xhr.response.name; //已经自动变成json
          }
        }
      }
```





# IE 缓存

```js
xhr.open("get","/testAJAX?t="+Date.now());
```



# 网络超时与网路异常

```js
// 超时设置 （2秒）
xhr.timeout = 2000;
// 超时回调
xhr.ontimeout = function(){
	alert('网络超时，请稍后重试')
}
// 网络异常回调
xhr.onerror = function(){
	alert('网络异常，请稍后重试')
}
xhr.open('GET','http://127.0.0.1:8000')
```

## 取消请求

```js
// 手动取消
xhr.abort()
```





# 请求重复发送问题

1. 防抖
2. 节流

```js
//添加变量,是否正在发送请求
let isString = false
```





#  jQuery 中的AJAX

## get 请求

> ```js
> ⭐$.get(url, [data], [callback], [type])
> ```

```js
$.get('http://127.0.0.1:8000/jquery-server',{a:200,b:200},function(){
	console.log(data)
},'json')
```

注：

1. `url`：请求的URL 地址
2. data：请求携带的参数
3. callback：载入成功时回调函数
4. type：设置返回内容格式，xml, html, script, json, text, _default

##  post 请求

> ```js
> ⭐$.post(url, [data], [callback], [type])
> ```

```js
$.post('http://127.0.0.1:8000/jquery-server',{a:200,b:200},function(){
	console.log(data)
},'json')
```

## 通用方法⭐

```js
$.ajax({
	// url
	url: 'http://127.0.0.1:8000/jquery-server',
	// 参数
	data: {a:100, b:200},
	// 请求类型
	type: 'GET',
	// 响应体结果
	dataType: 'json',
	// 成功的回调
	success: function(data){console.log(data);},
	// 超时时间
	timeout: 2000,
	// 失败的回调
	error: function(){console.log('出错拉~');},
	// 头信息，注意添加自定义请求 
	headers: {
		c: 300,
		d: 400
	}	
})

```





# fetch函数

https://developer.mozilla.org/zh-CN/docs/Web/API/WindowOrWorkerGlobalScope/fetch

```js
btn.onclick = function(){
	fetch('http:127.0.0.1:8000/fetch-server',{
		//请求方法
		method: 'POST'
		//请求头
		headers: {
			name: '大baby'
		}
		//请求体
		body: 'username=admin&password=admin'
	}).then(response=>{
        return response.text()
        //如果是json格式
        return response.json()
    }).then(response=>{
        console.log(response)
    })
}
```





# 同源策略

- 同源策略(Same-Origin Policy)最早由Netscape 公司提出，是浏览器的一种安全策略
- 同源： 协议、域名、端口号必须完全相同
- 跨域： 违背同源策略就是**跨域**



# JSONP

> JSONP(JSON with Padding)，是一个非官方的跨域解决方案，只支持get 请求。

在网页有一些标签天生具有跨域能力，比如：img link iframe script。
JSONP 就是利用script 标签的跨域能力来发送请求的。

##  JSONP 的使用

##### 动态的创建一个script 标签

```js
var script = document.createElement("script");
```

##### 设置script 的`src`，设置回调函数

```js
script.src = "http://localhost:8000/testAJAX?callback=abc";
function abc(data) {
	alert(data.name);
};
```

##### 将script 添加到body 中

```js
document.body.appendChild(script);
```

##### 服务器中路由的处理

```js
router.get("/testAJAX" , function (request , response) {
	console.log("收到请求");
	var callback = request.query.callback;
	var obj = {
		name:"孙悟空",
		age:18
	}
	res.send(callback+"("+JSON.stringify(obj)+")");
});
```



## jQuery中发送jsonp请求

> crossorigin="anonymous" 在引入文件时添加此代码取消警告

```js
$('button').eq(0).click(function () {
	$.getJSON("http://127.0.0.1:8000/jQuery-jsonp?callback=?",function(data) {
		console.log(data);
		$('#result').html(`
			名称：${data.name},<br>
			年龄：${data.age}
		`)
    });
});

```

```js
app.get("/jQuery-jsonp" , function (request , response) {
	const data = {
		name:"孙悟空",
		age:18
	}
    let str = JSON.stringify(data)
	//接受callback参数
	var callback = request.query.callback;
	response.end(`${callback}(${str`);
});
```





# CORS

https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CORS

> 特点是不需要在客户端做任何特殊的操作，完全在服务器中进行处理，支持get 和post 请求。跨域资源共享标准新增了一组HTTP 首部字段，允许服务器声明哪些源站通过浏览器有权限访问哪些资源

CORS 是通过设置一个响应头来告诉浏览器，该请求允许跨域，浏览器收到该响应以后就会对响应放行

### CORS 的使用

```js
app.get("/testAJAX" , function (request , response) {
	//通过response 来设置响应头，来允许跨域请求
	//response.set("Access-Control-Allow-Origin","http://127.0.0.1:3000");
	response.set("Access-Control-Allow-Origin","*");
	response.send("testAJAX 返回的响应");
});

```





# AJAX 请求状态

`xhr.readyState` 可以用来查看请求当前的状态
https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/readyState

> - 0: 表示XMLHttpRequest 实例已经生成，但是open()方法还没有被调用
> - 1: 表示send()方法还没有被调用，仍然可以使用setRequestHeader()，设定HTTP请求的头信息
> - 2: 表示send()方法已经执行，并且头信息和状态码已经收到
> - 3: 表示正在接收服务器传来的body 部分的数据
> - 4: 表示服务器数据已经完全接收，或者本次接收已经失败了





#  API总结

- XMLHttpRequest()：创建 XHR 对象的构造函数
- status：响应状态码值，如 200、404
- statusText：响应状态文本，如 ’ok‘、‘not found’
- readyState：标识请求状态的只读属性 0-1-2-3-4
- onreadystatechange：绑定 readyState 改变的监听
- responseType：指定响应数据类型，如果是 ‘json’，得到响应后自动解析响应
- response：响应体数据，类型取决于 responseType 的指定
- timeout：指定请求超时时间，默认为 0 代表没有限制
- ontimeout：绑定超时的监听
- onerror：绑定请求网络错误的监听
- open()：初始化一个请求，参数为：(method, url[, async])
- send(data)：发送请求
- abort()：中断请求 （发出到返回之间）
- getResponseHeader(name)：获取指定名称的响应头值
- getAllResponseHeaders()：获取所有响应头组成的字符串
- setRequestHeader(name, value)：设置请求头

### 接收服务器响应的数据

1. responseText：获得字符串形式的响应数据
2. responseXML：获得 XML 形式的响应数据

