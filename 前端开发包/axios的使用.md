## axios的使用

基于Promise，用于浏览器和 node.js 的HTTP客户端(可以调用一个 http 的接口)，能拦截请求和响应，自动转化 json 数据。

```js
axios.get('/data')
//也可以使用 restful方式进行传输 axios.get('/data')
.then(res=>{
  console.log(res.data) // res.data获取后台响应的数据
})
```

### 数据的请求

**get 方式请求数据**

```js
axios.get('/data',{
  // params 可以自动将对象数据转换成拼接字符串进行传输
  params:{
    id:233
  }
}).then((res)=>{console.log(res.data)})
```

**post 数据的传输**

```js
// 第一种 post 数据传输方式，如果后台支持 json，会更简单
axios.post('/data',{
  id:10010
  data:"请不要回应"
}).then(function(res){
  console.log(res.data)
})
// 第二种 post 数据的传输方法
const params = new URLSearchParams()
params.append('name','lihua')// 可以通过该方法写多个数据
axios.post('/data',params).then(res=>{
  console.log(res.data)
})
```

**put 数据的传输**

```js
axios.put('/data',{
  id:10010
  data:"请不要回应"
})
```

### axios 的返回对象

data：返回的数据

headers：响应头信息

status：响应状态吗

statusTest：响应状态信息

```js
axios.put('/data',{
  username:'liushaoye'
}).then(data=>{
  data.status
})
```

### axios 的全局配置

```js
axios.defaults.timeout = 3000 // 响应超时时间
axios.defaults.baseURL = 'http://localhost:3000' // 默认基准地址
axios.defaults.headers['mytoken']= 'adacocizuzxoui322ucuzcoiu' // 设置响应头
```

### axios拦截器

**请求拦截器**

发送的请求需要经过请求拦截器才能进行发送，送往服务器。

```js
axios.interceptors.request.use(function(config){
  console.log(config.url)
  config.headers.mytoken = 'hello' // 在header中添加了 mytoken : hello
  return config
},function(err){
  console.log(err)
})
```

**响应拦截器**

接受的响应，经过响应拦截器，进行加工处理之后才会被axios进行处理

```js
axios.interreceptors.response.use(function(res){
  // 对返回的数据进行处理
  var data = res.data
  return data
},function(err){
  console.log('有错误信息'+err)
  // 处理响应错误信息
})
axios.get('/data').then((res)=>{
  console.log(res)// 上面返回的是就是res.data,所以取出的值为res.data
})
```

中断（取消）请求

```js
var CancelToken = axios.CancelToken
var source = CancelToken = CancelToken.source()
axios.get('user',{
  cancelToken:source.token
})
```

## axios的配置

```js
import axios from 'axios'
import config from './config'
const httpFetch = axios.create(config)
// 配置拦截请求
httpFetch.interreceptors.request.use(req=>{
  // setting
})
httpFetch.interreceptors.response.use(res=>{
  if(res.data && typeof response.data == 'string'){
    response.data = JSON.parse(response.data)
  }
  // 其他操作
})
// 配置拦截响应
```

解决跨域问题

如果 `server` 端是自己开发的，那么修改相关代码支持跨域即可。如果不是自己开发的，那么可以自己写个后端转发该请求，用代理的方式实现。

跨域这个行为是**浏览器禁止**（浏览器不允许当前页面的所在的源去请求另一个源的数据）的，但是服务端并不禁止。



## 参考文章

| 文章名称         | 文章地址                               |
| ---------------- | -------------------------------------- |
| 【vue学习】axios | https://www.jianshu.com/p/d771bbc61dab |
|                  |                                        |

