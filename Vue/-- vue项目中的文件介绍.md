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



