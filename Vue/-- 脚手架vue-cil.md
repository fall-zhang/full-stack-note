## 安装及简单的介绍

快速生成一个Vue项目结构，简化一个项目的创建流程

### 安装

全局安装cli `npm install -g @vue/cli`

### 简介

`@vue/cli` 有三个主要的组件

**CLI** 

`@vue/cli` 全局安装的包，提供了终端里面的 `vue` 命令，可以通过 `vue create` 快速搭建一个新的项目，或者使用 `vue ui` 通过图形化界面管理你的所有项目。

**CLI 服务**

这是一个开发依赖的包，局部安装在每一个 `@vue/cli` 创建的项目中。构建在 `webpack` 和 `webpack-dev-server` 之上的，它包含了项目内部使用的 `vue-cli-service` 命令，提供了 `serve` 、`build` 等命令。

**CLI 插件**

向项目提供一些可选的功能的 `npm` 安装包，例如 `Babel/TypeScript` 、`ESLint` 集成，单元测试和 `end-to-end` 测试等，插件名称通常为 `@vue/cli-plugin-` （作为内建插件）`@vue-cli-plugin-`（社区插件）在项目中运行 `vue-cli-service` 会自动解析并加载所有列出的插件。

## 快速生成一个项目

**命令行创建**

`vue create` 通过命令行工具的方式进行创建一个 vue 项目

`vue ui` 使用图形化界面，可以创建一个 vue 项目

## CLI服务

`@vue/cli-service` 安装了一个名为 `vue-cli-service` 的命令，可以在 `package.json` 中的 `script` 以 `vue-cli-service` 进行调用和访问，或者是`./node_module/.bin/vue-cli-service` 访问这个命令。

当然，这个命令也可以通过 `npx` 工具进行调用：`npx vue-cli-service serve`。

`npx vue-cli-service serve` 这个命令会启动一个基于 `webpack-dev-server` 的服务器，这个服务器自带热模块重载 `Hot-module-Replacement` 除了命令行，也可以通过 `vue.config.js` 进行配置。

```bash
vue-cli-service serve [options] [entry] 
# 将命令放置在 package.json 中的 script 中。
# [entry] 作为程序的入口
# 选项：
#  --open    在服务器启动时打开浏览器
#  --copy    在服务器启动时将 URL 复制到剪切版
#  --mode    指定环境模式 (默认值：development)
#  --host    指定 host (默认值：0.0.0.0)
#  --port    指定 port (默认值：8080)
#  --https   使用 https (默认值：false)
```

`npx vue-cli-service build` 

```bash
用法：vue-cli-service build [options] [entry|pattern]

# 选项：
#  --mode        指定环境模式 (默认值：production)
#  --dest        指定输出目录 (默认值：dist)
#  --modern      面向现代浏览器带自动回退地构建应用
#  --target      app | lib | wc | wc-async (默认值：app)
#  --name        库或 Web Components 模式下的名字 (默认值：package.json 中的 "name" 字段或入口文件名)
#  --no-clean    在构建项目之前不清除目标目录
#  --report      生成 report.html 以帮助分析包内容
#  --report-json 生成 report.json 以帮助分析包内容
#  --watch       监听文件变化
```

## 脚手架的自定义配置

如果想要让vue项目跑起来后自动打开，可以在 `package.json` 文件里面添加该配置

```json
{
  "vue":{
    "devServer":{
    	"port":8888,// 端口号更改为 8888
      "open":true // 编译完成后，自动打开浏览器
    }
  }
}
```

当然，也可以通过单独的文件 `vue.config.js` 进行单独配置。

```js
// vue.config.js
module.exports ={
  devServer:{
    open:true,
    port:8899
  }
}
```

- [ ] 实现搭建一个 nuxt 页面