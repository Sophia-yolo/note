# 源码目录结构

```
├── /dist/				# 项目输出目录
├── /lib/ 				# 项目源码目录
│ ├── /adapters/       # 定义请求的适配器 xhr、http
│ │ ├── http.js       # 实现 http 适配器(包装 http 包)
│ │ └── xhr.js        # 实现 xhr 适配器( 包装 xhr 对象)
│ ├── /cancel/         # 定义取消功能
│ ├── /core/ 		   # 一些核心功能
│ │ ├── Axios.js	  # axios 的核心主类
│ │ ├── dispatchRequest.js # 用来调用 http 请求适配器方法发送请求的函数
│ │ ├── InterceptorManager.js # 拦截器的管理器
│ │ └── settle.js 			  # 根据 http 响应状态，改变 Promise 的状态
│ ├── /helpers/ 			   # 一些辅助方法
│ ├── axios.js 				   # 对外暴露接口
│ ├── defaults.js 			   # axios 的默认配置
│ └── utils.js                 # 公用工具
├── package.json			    # 项目信息
├── index.d.ts  			    # 配置 TypeScript 的声明文件
└── index.js 					# 入口文件
```



# axios 与 Axios 的关系

1. 从语法来看：axios 不是 Axios 的实例
2. 从功能上来说：axios 是Axios的实例
3. axios 是 Axios.prototype.request 函数 bind() 返回的函数
4. axios 作为对象由 Axios 原型对象上的所有方法，由 Axios 对象上所有属性



# instance 与 axios 的区别

相同:

> 1. 都是一个能发任意请求的函数: request(config)
> 2. 都有发特定请求的各种方法: get()/post()/put()/delete()
> 3. 都有默认配置和拦截器的属性: defaults/interceptors

不同:

> 1. 默认配置很可能不一样
> 2. instance 没有 axios 后面添加的一些方法: create()/CancelToken()/all()



# axios 整个流程

![image-20210713234448716](C:\Users\Area1\AppData\Roaming\Typora\typora-user-images\image-20210713234448716.png)

>  整体流程:
> request(config) ==> dispatchRequest(config) ==> xhrAdapter(config)

1. request(config):

   将请求拦截器 / dispatchRequest() / 响应拦截器 通过 promise 链串连起来,
   返回 promise

2. dispatchRequest(config):

  转换请求数据 ===> 调用 xhrAdapter()发请求 ===> 请求返回后转换响应数
  据. 返回 promise

3. xhrAdapter(config):
  创建 XHR 对象, 根据 config 进行相应设置, 发送特定请求, 并接收响应数据,
  返回 promise



#  axios 的请求/ 响应拦截器

![image-20210713234627111](C:\Users\Area1\AppData\Roaming\Typora\typora-user-images\image-20210713234627111.png)

## 请求拦截器/响应拦截器

- 在真正发送请求前执行的回调函数
- 可以对请求进行检查或配置进行特定处理
- 成功的回调函数, 传递的默认是 config(也必须是)
- 失败的回调函数, 传递的默认是 error



# axios 的请求/ 响应数据转换器

## 请求转换器

> 对请求头和请求体数据进行特定处理的函数

```js
if (utils.isObject(data)) {
	setContentTypeIfUnset(headers, 'application/json;charset=utf-8');
	return JSON.stringify(data);
}
```



## 响应转换器

> 将响应体 json 字符串解析为 js 对象或数组的函数

```js
response.data = JSON.parse(response.data)
```





#  response 的整体结构

```js
{
    data,
    status,
    statusText,
    headers,
    config,
    request
}
```



# error 的整体结构

```json
{
    message
    response,
    request,
}
```



# 取消未完成的请求

1. 当配置了 cancelToken 对象时, 保存 cancel 函数

  > - 创建一个用于将来中断请求的 cancelPromise
  > - 并定义了一个用于取消请求的 cancel 函数
  > - 将 cancel 函数传递出来

2. 调用 cancel()取消请求

  > 1. 执行 cacel 函数, 传入错误信息 message
  > 2. 内部会让 cancelPromise 变为成功, 且成功的值为一个 Cancel 对象
  > 3. 在 cancelPromise 的成功回调中中断请求, 并让发请求的 proimse 失败,失败的 reason 为 Cancel 对象