> 创建时间：2021-04-11
> 更新时间：2021-04-15

vue-router是vue实现，控制路由的官方插件

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
$route.params**
      一个 key/value 对象，包含了 动态片段 和 全匹配片段，
      如果没有路由参数，就是一个空对象。
**3.$route.query**
      一个 key/value 对象，表示 URL 查询参数。
      例如，对于路径 /foo?user=1，则有 $route.query.user == 1，
      如果没有查询参数，则是个空对象。
**4.$route.hash**
      当前路由的 hash 值 (不带 #) ，如果没有 hash 值，则为空字符串。锚点
**5.$route.fullPath**
      完成解析后的 URL，包含查询参数和 hash 的完整路径。
**6.$route.matched**
      数组，包含当前匹配的路径中所包含的所有片段所对应的配置参数对象。
**7.$route.name    当前路径名字**
**8.$route.meta  路由元信息
```

### 文章参考

| 作者          | 连接                                   |
| ------------- | -------------------------------------- |
| Ishmael丶Yoko | https://www.jianshu.com/p/fa0b5d919615 |

