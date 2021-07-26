# axios 实现拦截器功能

```js
//构造函数
        function Axios(config){
            this.config = config;
            this.interceptors = {
                request: new InterceptorManager(),
                response: new InterceptorManager()
            }
        }
        Axios.prototype.request = function(config){
            //创建一个Promise对象
            let promise = Promise.resolve(config)
            //创建一个数组
            const chains = [dispatchRequest,undefined]
            //处理拦截器
            //请求拦截器 将请求拦截器的回调 压入到 chains 的前面——遍历request.handles = []
            this.interceptors.request.handles.forEach(item => {
                chains.unshift(item.fulfilled,item.rejected)
            })
            //响应拦截器
            this.interceptors.response.handles.forEach(item => {
                chains.push(item.fulfilled,item.rejected)
            })
            while(chains.length >0 ){
                promise = promise.then(chains.shift(),chains.shift() )
            }
            return promise
        }
        function dispatchRequest(config){
            //返回一个promise队形
            return new Promise((resolve,reject) => {
                //成功
                resolve({
                    status: 200,
                    statusText:'ok'
                })
            })
        }
        
        //创建实例
        let context = new Axios({})
        //创建axios函数
        let axios = Axios.prototype.request.bind(context)
        //将content 属性 config interceptors 添加至 axios 函数对象上
        Object.keys(context).forEach(key =>{
            axios[key] = context[key]
        })
        //拦截器管理器构造函数
        function InterceptorManager(){
            this.handles = []
        }
        InterceptorManager.prototype.use = function(fulfilled,rejected){
            this.handles.push({
                fulfilled,
                rejected
            })
        }
        // 添加请求拦截器
        axios.interceptors.request.use(function (config) {
            console.log('请求拦截器成功 -1')
            return config;
        }, function (error) {
            console.log('请求拦截器失败 -1')
            return Promise.reject(error);
        });
        axios.interceptors.request.use(function (config) {
            console.log('请求拦截器成功 -2')
            return config;
        }, function (error) {
            console.log('请求拦截器失败 -2')
            return Promise.reject(error);
        });

        // 添加响应拦截器
        axios.interceptors.response.use(function (response) {
            console.log('响应拦截器成功 -1')
            return response;
        }, function (error) {
            console.log('响应拦截器失败 -1')
            return Promise.reject(error);
        });
        axios.interceptors.response.use(function (response) {
            console.log('响应拦截器成功 -2')
            return response;
        }, function (error) {
            console.log('响应拦截器失败 -2')
            return Promise.reject(error);
        });
        axios({
            method: 'GET',
            url: 'http://127.0.0.1:3000/posts'
        }).then(response =>{
            console.log('ooooooo')
        }).catch(reason=>{
            console.log('aaaaaa')
        })
```



结果：

![image-20210713211147275](C:\Users\Area1\AppData\Roaming\Typora\typora-user-images\image-20210713211147275.png)

