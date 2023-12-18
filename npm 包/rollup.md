> Create by **fall** on  17 Feb 2022
> Recently revised in 18 Dec 2023

## Rollup

Rollup 是一款基于 ESmodule 的打包软件（webpack 基于 commonjs）

```js
import pkg from "./package.json" assert { type: 'json' };
// 在 package.json 中配置 main，作为 cjs 默认导入内容，module 作为 esm 导入内容
import json from "@rollup/plugin-json";
import resolve from "@rollup/plugin-node-resolve";
import commonjs from "@rollup/plugin-commonjs";
import { babel } from '@rollup/plugin-babel'
import vuePlugin from 'rollup-plugin-vue'
// vue-plugin-vue 描述了需要哪些包
export default {
  input: "./src/immer/index.vue",
  output: [{
      file: pkg.main,
      format: "cjs",
    },{
      file: pkg.module,
      format: "esm",
      // 将这些包作为单独的包导出
      manualChunks: {
				lodash: ['lodash']
			}
    },
  ],
  plugins: [
    vuePlugin(/* options */), // 用于解析 .vue 文件
    json(),
    commonjs({
      include: /node_modules/,
    }),
    resolve({
      preferBuiltins: true,
      jsnext: true,
      main: true,
      brower: true,
    }),
    babel({ exclude: "node_modules/**" }),
  ],
};
```

### TreeShaking

Rollup 必须保守地删除代码，以确保最终结果将正确运行。无论是对你正在使用的模块中的某些部分还是对全局环境，Rollup 都会使这些副作用。

## 插件

插件分为官方插件（以 @rollup/plugin 开头）和社区插件（rollup-plugin 开头）

### rollup-plugin-visualizer

用来查看打包后的包体积大小

```js

```

### @rollup/plugin-json

可以处理 JSON 文件

### @rollup/plugin-node-resolve

可以解析 node 中的包，将代码打包到产物中

### @rollup/plugin-alias

```js
{
  plugins: [
    vuePlugin({
      target: 'broswer'
    }),
    sucrase({
      exclude: ['node_modules/**'],
      transforms: ['jsx']
    }),
    alias({
      entries: [
        // { find: 'packages/', replacement: '@/' },
        { find: '@', replacement: __dirname + '/packages' },
        { find: 'utils', replacement: __dirname + '/packages/utils/index.js' },
      ]
    }),
    // 让 Rollup 查找到外部模块，打包到产物内
    resolve({
      // 将自定义选项传递给解析插件
      moduleDirectories: ['node_modules']
    })
    // alias({
    //   entries: [
    //     { find: 'utils', replacement: '../../../utils' },
    //     { find: 'batman-1.0.0', replacement: './joker-1.5.0' }
    //   ]
    // })
  ]
}
```

















