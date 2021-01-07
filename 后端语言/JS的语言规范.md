## CommonJS规范

> 每一个文件就是一个模块，拥有自己独立的作用域，变量，以及方法等，对其他的模块都不可见。每个模块内部，module变量代表当前模块。这个变量是一个对象，它的exports属性（即module.exports）是对外的接口。加载某个模块，其实是加载该模块的module.exports属性。require方法用于加载模块。
>
> - 所有代码都运行在模块作用域，不会污染全局作用域
> - 模块可以被多次加载，但只会运行一次，然后将结果进行缓存，之后调用会直接调用缓存的结果，如果想调用，必须清除缓存
> - 模块的加载顺序和代码顺序相同
>
> 注：
>
> - CommonJS 规范是服务器规范，一般先下载到本地再调用。
> - 读取速度非常，快采用同步的执行方式

> **浏览器为何不能兼容CommonJS**
>
> 缺少四个环境变量
>
> module/exports/require/global

```js
// test.js 向外暴露接口
module.exports = function(){
  console.log("这就是调用的东西")
}
// 其他文件使用test.js
var ss =  require("./test")
ss()
```

### CommonJS使用

> - 下载插件到本地
>   - npm install API --save-dev
> - 通过require()引入文件
> - 查阅插件的文档

## AMD规范

AMD规范：(客户端 / 浏览器）

```js
// 声明：
define(function(){
  return{
    outA:showA,
    outB:showB
  }
})
// 引入：异步执行
require("moduleA.js",function(moduleA){
  // 在模块引入后执行
  moduleA.outA()
  moduleA.outB()
})
```

## ECMA6规范

```js
export={
	outA:showA,
  outB:showB
}
import moduleA from "moduleA.js"
moduleA.outA()
moduleA.outB()
```

> **CMD规范**
>
> 阿里的一名员工编写的规范，已经不使用了

## RequireJS 语法

Require.js 是实现模块化开发的语法，而模块化开发逐渐淘汰了 Require.js，Require.js 在 MVC 模式开发初期开创了辉煌。

> 注：每一个.html都要一个入口文件：管理当前.html页面使用的所有.js代码
> 注：除了 require.js 的后缀名，其他文件的后缀名都可以省略

```js
// 客户端.js文件遵从AMD规范
// add.js
define(function(){
  function add(x,y){
    return x+y
  }
  function show(){
    console.log('hello world')
  }
  return {
    outAdd:add,
    outShow:show
  }
})
// main.js
// 引入的路径必须为数组
require(["add"],function(getObj){
  var res = getObj.outAdd(1024,2048)
  console.log(res)
})
```

```js
// 实现路径的自动配置
require.config({
  path:{
    // 假设文件路径在demo下的add中
    thePath:'demo/add'
  }
})
require(['thePath'],function(){
  var res = addObj.outAdd(10,20)
  addObj.outShow()
})
```

**子模块使用子模块的方法**

```js
// main.js
require(['path/funA','path/funB'],function(){
  var res = addObj.outAdd(10,20)
  addObj.outShow()
}])
// funA.js
define(function(){
  function addA(a,b){
    return a+b
  }
  return {
    addA:addA
  }
})
// funB.js
define(['path/funA'],function(addA){
  add(10,11)
})
```

## AMD规范和CommonJS规范

| AMD规范  | 都是为了模块化 | 非同步加载模块，允许指定回调函数         |
| -------- | -------------- | ---------------------------------------- |
| 规范     | 相同点         | 不同点                                   |
| CommonJS |                | 同步加载，只有加载完成才能完成后面的操作 |

两者不同点