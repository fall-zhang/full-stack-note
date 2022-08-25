> Create by fall on:2021-04-11
> Recently revised in:2022-03-13

## 路由中的两大对象

vue-router 是 vue 实现，控制路由的官方插件

其中有两大对象

$router 和 $route

下面来详细说说两者的不同：

`$router`表示的是全局路由对象

```js
$router.push('login')
$router.push({path:'home'})
$router.push({name:'user',params:{id:12314}})
$router.push({ path: 'register', query: { plan: '123' }})
$router.go(-1) // 回退
```

`$route` 当前路由对象

```
$route.path
字符串，对应当前路由的路径，总是解析为绝对路径，如 "/foo/bar"。
$route.params
      一个 key/value 对象，包含了 动态片段 和 全匹配片段，
      如果没有路由参数，就是一个空对象。
$route.query
      一个 key/value 对象，表示 URL 查询参数。
      例如，对于路径 /foo?user=1，则有 $route.query.user == 1，
      如果没有查询参数，则是个空对象。
$route.hash
      当前路由的 hash 值 (不带 #) ，如果没有 hash 值，则为空字符串。锚点
$route.fullPath
      完成解析后的 URL，包含查询参数和 hash 的完整路径。
$route.matched
      数组，包含当前匹配的路径中所包含的所有片段所对应的配置参数对象。
$route.name  当前路径名字
$route.meta  路由元信息
```

## 路由

### 路由执行顺序

- 导航被触发。
- 在失活的组件里调用 beforeRouteLeave 守卫。
- 调用全局的 beforeEach 守卫。
- 在重用的组件里调用 beforeRouteUpdate 守卫 (2.2+)。
- 在路由配置里调用 beforeEnter。
- 解析异步路由组件。
- 在被激活的组件里调用 beforeRouteEnter。
- 调用全局的 beforeResolve 守卫 (2.5+)。
- 导航被确认。
- 调用全局的 afterEach 钩子。
  - 触发 DOM 更新。
- 调用 beforeRouteEnter 守卫中传给 next 的回调函数，创建好的组件实例会作为回调函数的参数传入。

### 路由守卫

**全局守卫**

- router.beforeEach 全局前置守卫 进入路由之前
- router.beforeResolve 全局解析守卫(2.5.0+) 在beforeRouteEnter调用之后调用
- router.afterEach 全局后置钩子 进入路由之后

```js
// main.js 入口文件
import router from './router'; // 引入路由
router.beforeEach((to, from, next) => { 
  next();
});
router.beforeResolve((to, from, next) => {
  next();
});
router.afterEach((to, from) => {
  console.log('afterEach 全局后置钩子');
});
```

参数：

- to：表明前往的路由
- from：表明从哪里来
- next：表示进行接下来的内容，必须要进行调用，调用方式如下
  - `next()`：进入下一个路由
  - `next(false)`：取消进入下一个路由
  - `next('path')`：进入 path 路由，或者和 `router.push` 相同的参数

**独享守卫**

```js
const routers = [
  {
    path:'/path',
    component:()=>import('./Page.vue')
    beforeEnter: (to, from, next) => { 
      // 参数用法什么的都一样,调用顺序在全局前置守卫后面，所以不会被全局守卫覆盖
      // ...
    }
  }  
]
```

- beforeRouteEnter 进入路由前
- beforeRouteUpdate (2.2) 路由复用同一个组件时
- beforeRouteLeave 离开当前路由时

```JS
const route = {
  beforeRouteEnter (to, from, next) {
    // 在路由独享守卫后调用 不！能！获取组件实例 `this`，组件实例还没被创建
  },
  beforeRouteUpdate (to, from, next) {
    // 在当前路由改变，但是该组件被复用时调用 可以访问组件实例 `this`
    // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
    // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
  },
  beforeRouteLeave (to, from, next) {
    // 导航离开该组件的对应路由时调用，可以访问组件实例 `this`
  }
}
```

路由错误捕获

```js
router.onError(err=>{
	console.log(err)
})
```





## 文章参考

| 作者          | 连接                                       |
| ------------- | ------------------------------------------ |
| Ishmael丶Yoko | https://www.jianshu.com/p/fa0b5d919615     |
| OBKoro1       | https://juejin.cn/post/6844903641866829838 |


