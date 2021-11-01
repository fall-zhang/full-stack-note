## Element-UI

是一套基于 Vue2.0 的桌面端组件库

官网 https://element.eleme.cn/

**命令行安装**

安装依赖包 `npm i element-ui -S`

导入 `Element-UI` 的相关资源

```js
// src 中的 main.js 添加以下内容
import ElementUI from 'element-ui' // 导入
import 'element-ui/lib/theme-chalk/index.css';
Vue.use(ElementUI)
```

**图形化界面的自动安装**

- 运行 `vue ui` 命令，打开图形化界面的面板
- 计入到插件，添加插件中，进入查件查询面板
- 搜索 `vue-cli-plugin-element` 并且进行安装
- 配置插件，实现按需导入，从而减小打包后项目的体积