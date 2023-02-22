> Create by fall on 22 Feb 2023
> Recently revised in 22 Feb 2023

## 编写组件

- rollup 编写组件

项目目录

```markdown
|- src
    |- MyButton
        |- index.js
        |- index.vue
        |- index.scss
    |- MyInput
        |- index.js
        |- index.vue
        |- index.scss
    |- main.js
|- rollup.config.js
```

其中 index.js 文件负责导出，并且为组件提供单独安装功能

```js
import MyButton from "./index.vue";
MyButton.install = function (Vue) {
  Vue.component(MyButton.name, MyButton);
};
export default MyButton;
```

main.js 负责引入所有的组件，并且导出安装内容

```js
import MyButton from './MyButton.js'
import MyInput from './MyInput.js'
import { version } from '../package.json'
const componentList = [MyButton,MyInput] 
const install = (Vue)=>{
  componentList.forEach(component=>{
    Vue.use(component.name,component)
  })
}

export {
	MyButton,
  MyInput
}

export default {
  version:version,
  install:install
}
```

然后是配置打包工具 rollup

`rollup-plugin-vue` 插件来解析 vue 文件

是 5.x 版本解析 vue2，最新的 6.x 版本解析 vue3

```js
import resolve from "rollup-plugin-node-resolve";
import vue from "rollup-plugin-vue";
import babel from "@rollup/plugin-babel";
import commonjs from "@rollup/plugin-commonjs";
import scss from "rollup-plugin-scss";
import json from "@rollup/plugin-json";

const formatName = "MyUI";
const config = {
  input: "./src/main.js",
  output: [
    {
      file: "./lib/bundle.cjs.js",
      format: "cjs",
      name: formatName,
      exports: "auto",
    },
    {
      file: "./lib/bundle.js",
      format: "iife",
      name: formatName,
      exports: "auto",
    },
  ],
  plugins: [
    json(),
    resolve(),
    vue({
      css: true,
      compileTemplate: true,
    }),
    babel({
      exclude: "**/node_modules/**",
    }),
    commonjs(),
    scss(),
  ],
};
export default config;
```

## 参考文章

| 作者   | 文章名称                                                     |
| ------ | ------------------------------------------------------------ |
| 谢小飞 | [从零开始发布自己的NPM包](https://juejin.cn/post/7052307032971411463) |
|        |                                                              |
|        |                                                              |

