# axios 实现发送请求

```js
//声明构造函数
        function Axios(config){
            this.config = config;
        }
        Axios.prototype.request = function(config){
            //发送请求
            //创建了一个promise对象
            let promise = Promise.resolve(config)                
            //声明一个数组
            let chains = [dispatchRequest, undefined]//underfind作用是占位
            //调用then 方法指定回调
            let result = promise.then(chains[0],chains[1])
            //返回 promise 结果
            return result
        }

        // dispatchRequest 函数
        function dispatchRequest(config){
            //调用适配器发送请求
            return xhrAdapter(config).then(response =>{
                //响应的结果进行转换
                // console.log(response);
                return response
            },error =>{
                throw error;
            })
        }


        //adapter 适配器
        function xhrAdapter(config){
            return new Promise((resolve,reject)=>{
                //发送 ajax 请求
                let xhr = new XMLHttpRequest()
                //初始化
                xhr.open(config.method,config.url)
                //发送
                xhr.send()
                //绑定事件
                xhr.onreadystatechange = function(){
                    if(xhr.readyState === 4){
                        //判断成功的条件
                        if(xhr.status >= 200 && xhr.status <300){
                            //成功的状态
                            resolve({
                                //配置对象
                                config: config,
                                //响应体
                                data: xhr.response,
                                //响应头
                                headers:  xhr.getAllResponseHeaders(),//字符串 parseHeaders
                                //xhr 请求对象
                                request: xhr,
                                //响应状态字符串
                                status: xhr.status,
                                //响应状态字符串
                                statusText: xhr.status
                            })
                        }else{
                            //失败的状态
                            reject(new Error('请求失败 失败的状态码为'+ xhr.status))
                        }
                    }
                }
            })
        }

        //创建 axios 函数
        let axios = Axios.prototype.request.bind(null)

        axios({
            method: 'GET',
            url: 'http://127.0.0.1:3000/posts'
        }).then(response => {
            console.log(response);
        })
```

结果：

![image-20210713194425940](C:\Users\Area1\AppData\Roaming\Typora\typora-user-images\image-20210713194425940.png)

