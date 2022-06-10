> Create by fall on:2022-03-13
> Recently revised in:2022-06-10

## 生命周期

挂载时：

父组件（`beforeCreate`）->父（`created`）->父（`beforeMount`）->子组件（`beforeCreate`）->子（`created`）->子（`beforeMount`）->子（`mounted`）->父（`mounted`）

子组件更新

父组件（`beforeUpdate`）->子组件（`buforeUpdate`）->子组件（`updated`）->父组件（`updated`）

父组件更新

父组件（`beforeUpdate`）->父组件（`updated`）

销毁

父 （`beforeDestroy`）->子 （`beforeDestroy`）->子 （`destroyed`）->父 （`destroyed`）

## keep-alive

实现组件缓存，组件切换时，不会对当前组件进行卸载。

使用场景是嵌套 `router-view`

```vue
<keep-alive>
  <router-view></router-view>
</keep-alive>
```

被 `keep-alive` 包含的组件/路由中，会多出两个生命周期的钩子：`activated` 与 `deactivated`。`activated` 会在组件第一次渲染时调用，之后如果激活了，也会去调用。



## Vue.extend

const app = createApp(App)

app.use()

## 自定义指令

## diff算法

根节点是否相同：

## 各个文件的作用

`src` 目录下创建不同名称的文件夹以区分模块

| 文件夹     | 内容                                                   |
| ---------- | ------------------------------------------------------ |
| main       | 整个项目的入口js文件，构建打包生成js文件的起点就是它   |
| router     | vue路由文件                                            |
| `api`      | ajax请求的 `api` 方法文件                              |
| asset      | css样式、iconfont、图片之类的文件                      |
| components | 存放公用的组件                                         |
| store      | 存放 vuex 仓库数据文件；数据多的时候一可以拆分多个模块 |
| utils      | 存放小工具文件                                         |
| views      | 页面组件，一个页面可以分成多个单文件组件               |
| App.vue    | 主要是放置路由和一些路由跳转动画                       |
| layout     | 布局                                                   |
| page       | 按照页面进行划分，                                     |

## 模块的导入导出

导入以使用模块，导出模块，可以提供给其他模块使用

**导入模块**

导入常量，函数，文件，模块等，方便进行使用

`import Name from './path/file'`

**导出模块**

export 和 export default 都可以用于导出常量、函数、文件、模块等。

export 和 export default 的区别

使用 export 导出的内容都必须使用大括号进行引用

```js
// module.js
export const fake = '虚伪的人' 
// main.js
import {fake}
```


