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
$route.name    当前路径名字
$route.meta  路由元信息
```

## 路由执行顺序

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



### 文章参考

| 作者          | 连接                                   |
| ------------- | -------------------------------------- |
| Ishmael丶Yoko | https://www.jianshu.com/p/fa0b5d919615 |

