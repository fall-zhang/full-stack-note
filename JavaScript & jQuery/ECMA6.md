# 技术前沿

### **异步流程控制**

JavaScript 流程控制的演进过程，分以下 5 部分：

- 回调函数Callbacks
- 异步JavaScript
- Promise / a+ 规范
- 生成器Generators/ yield ( es6 )
- Async/ await ( es7 )

### 前端开发四阶段

- Html/css/js（基础）
- jQuery、jQuery-ui，Extjs（曾经流行）
- Backbone（mvc），Angularjs、Vuejs（当前流行）
- React组件化（未来趋势）、Vuejs
- serverless云开发（新趋势）

```js
var parent = {
    foo() {
        console.log('Hello from the Parent')
    }
}
var self = {
    foo() {
        super.foo()
        console.log("这是你的")
    }
}
var son = {
    foo() {
        super.foo()
        console.log('到底是啥鸟')
    }
}
Object.setPrototypeOf(self, parent)
Object.setPrototypeOf(son, self)
son.foo()
```

## 数据操作

### 迭代器

> 提供了next()遍历一个序列

```js
var arr = [11,12,13];
var itr = arr[Symbol.iterator]();// 自定义一个对象的迭代器
 
itr.next(); // { value: 11, done: false }
itr.next(); // { value: 12, done: false }
itr.next(); // { value: 13, done: false }
 
itr.next(); // { value: undefined, done: true }
```

### Generators

Generator 函数是 ES6 的新特性，它允许一个函数返回的可遍历对象生成多个值。

在使用中你会看到 * 语法和一个新的关键词 yield:

```js
function *infiniteNumbers() {
  var n = 1;
  while (true){
    yield n++;
  }
}
var numbers = infiniteNumbers(); // returns an iterable object
 // 每次返回值，值会变成下一个
numbers.next(); // { value: 1, done: false }
numbers.next(); // { value: 2, done: false }
numbers.next(); // { value: 3, done: false }
```

## Promise

Promise 是用来管理异步编程的，**它本身不是异步的**，Promise用于优化不断调用造成的回调地狱

`new Promises()` 传入构造函数，参数为构造函数

```js
var p = new Promise(function(resolve, reject) {  
  if (/* condition */) {
    // fulfilled successfully
    resolve(/* value */);  
  } else {
    // error, rejected
    reject(/* reason */);  
  }
});
// p.then()内传入方法，
// 第一个方法执行成功后执行 resolve 中的函数
// 第二个方法执行方法的传入值为 reject 的参数 
p.then(()=>{
  /* 成功后的执行内容 */
},()=>{
  /* 失败后的执行内容 */
})
```

> 错误会像冒泡一样，如果第一个出现错误，那么接下来的都会出现错误
>
> 可以利用这一特性，在最后调用的接口上实现对于错误的处理，简化操作
>
> 注：实现该特性需要两点注意，第一点每次调用 then 都要返回一个新的 Promise ；不管第一个参数的返回值是什么，

**捕获错误**

```js
const p = new Promise((res,rej)=>{
  if(math.random()>0.5){
    res("成")
  }else{
    rej("败")
  }
})
let p1 = p.catch((error)=>{
  console.log("因为错了"+ error)
})
```

> 是否执行 reslove , reject 都是取决于是否执行 reslove() & reject() 或者是函数本身出现异常

**当执行的函数出现错误时**

```js
new Promise(resolve=>{
  resolve(a)
}).then(result=>{
  console.log("成功"+result)
},reason=>{
  console.log("失败"+reason)
}).then(result=>{
  console.log("success"+result)
},reason=>{
  console.log('failure')
})

// 该函数第一次执行失败，调用失败的函数
// 第二次由于没有返回值，以成功执行计算
```

> 能解决回调地狱的问题，但是由于充满了 then 方法，使得可读性不强，所以使用 async & await作为语法糖，很多人认为 async & await 就是回调地狱的最终解决方案。

### Promise 的方法

**Promise.resolve()** 返回一个给定值解析后的 Promise 对象

`Promise.resolve('foo')` 

等价于`new Promise(resolve => resolve("foo"))`

## async & await

async/await 的实现是基于 Promise的，async 函数就是返回 Promise 对象，是 generator 的语法糖。

- 语法简洁，更像是同步代码，也更符合普通的阅读习惯；
- 改进JS中异步操作串行执行的代码组织方式，减少callback的嵌套；
- Promise 中不能自定义使用 try/catch 进行错误捕获，但是在 Async/await 中可以像处理同步代码处理错误。

因为 await 将异步代码改造成了同步代码，如果多个异步代码**没有依赖性却使用了 await 会导致性能上的降低**。

await 意思是，等待 await 里面的函数全部执行完成，再接着执行函数

> 任务队列（宏任务）
>
> 基于微任务的技术有 MutationObserver、Promise 以及以 Promise 为基础开发出来的很多其他的技术，本题中resolve()、await fn()都是微任务。
>
> 不管宏任务是否到达时间，以及放置的先后顺序，每次主线程执行栈为空的时候，引擎会优先处理微任务队列，**处理完微任务队列里的所有任务**，再去处理宏任务。

```js
let p1 = Promise.resolve(1)
let p2 = new Promise(resolve=>{
  setTimeout(()=>{
    resolve(2)
  },2000)
})
async function fun(){
  console.log(1)
  let resu2 = await p1
  console.log(3)
  let resu1 = await p2
  console.log(4)
}
fun()
console.log(2)
```

根据HTML5 的标准，setTimeout最少为 4ms