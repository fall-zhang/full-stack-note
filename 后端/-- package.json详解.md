> Create by **fall** on ——
> Recently revised in 12/08/2022

## package.json

`package.json` 是一个项目清单，可以做很多互不相关的事情

- 存储元数据：元数据就是描述数据信息的数据
- 工具的配置中心（可以在该文件内放置工具的配置）
- `npm` 和 `yarn` 存储所有已经安装的包的名称和版本的地方。

最简单的 `package.json` 文件（其实就是最简单的 JSON 文件）：

```json
{} // 真的很简单 ^_^
```

`package.json` 的文件当然要符合语法规范

```json
{
  "name":"my-demo"
}
```

> 命令行工具快速创建 package.json： `npm init` 初始化当前环境。
>
> `npm init -y` 或者 `npm init -yes` 快速创建

### 属性值含义

所有属性都可以通过 npm 或者其它工具使用

> name 必须小于 214 个字符，不能包含空格，只能包含小写字母、连字符(`-`)、下划线（`_`）

| 值                   | 作用                                                         |
| -------------------- | ------------------------------------------------------------ |
| name（必填           | 设置应用程序 / 软件包的名称                                  |
| version（必填        | 表明当前的版本                                               |
| private              | 私有，防止应用程序 / 软件包被意外发布到 npm 公共仓库         |
| main                 | 设置应用程序需的入口点，也就是默认导入的时候，是哪个文件     |
| scripts              | 定义了一组可以运行的 node 脚本                               |
| description          | 应用程序 / 软件包的简短描述                                  |
| dependencies         | 设置了作为依赖安装的 npm 安装包列表                          |
| devDependencies      | 设置作为开发依赖安装的 `npm` 软件包的列表，不会作为依赖树被安装 |
| peerDependencies     | 于表示与另一个包的依赖与兼容性关系来警示使用者。             |
| optionalDependencies | 可选依赖，安装失败也不会报错，比如控制台高亮的 `chalk`       |
| type                 | type 为 module 可以表明当前使用 `import` 的方式引入包，`node>16` |
|                      |                                                              |
|                      |                                                              |

```json
{
  "name": "fall-template",
  "version": "0.0.6",
  "private": true,
  "main":"src/main.js",
  "scripts": {
    "dev": "vite",
  },
  "description":"what a nice package!",
  "dependencies": {
    "react": "^18.1.0"
  },
  "devDependencies": {
    "vite": "^3.0.9"
  },
  "peerDependencies": {
    "react-dom": ">=18.1.0"
  },
  "optionalDependencies": {
    "react-dom": ">=18.1.0"
  },
  "author": {
    "name": "Fall Zhang",
    "email": "a90172451@gmail.com",
    "url": "https://github.com/fall-zhang"
  },
  "repository": {
    "type": "git",
    "url": "https://github.com/Fall-zhang/vite-vue3-TS-lint"
  }
}
```

### script

标签的前缀和后缀

- 前缀：`pre`、`post`

```json
// script 标签通常可以添加前缀和后缀来执行一些任务
{
  "script":{
    "prepublish":"npm run build", 
    "postpublish":"git push"
  }
}
```

### config

```js
"config": {
  "port": "3001"
}
// 可以通过 process 访问到 config 中配置的内容
console.log(process.env.npm_package_config_port)
```

```json
{
  "publishConfig": {
    "registry": "https://registry.npmjs.org/"
  }
}
```

### 系统环境配置

| 值          | 作用                                            |
| ----------- | ----------------------------------------------- |
| engines     | 设置了此软件包 / 应用，在哪个版本的 node 上运行 |
| browerslist | 告知支持哪些浏览器                              |
| os          | 指定项目对操作系统的兼容性要求                  |
| cpu         | 指定项目只能在特定的 CPU 体系上运行。           |
|             |                                                 |
|             |                                                 |
|             |                                                 |

```json
{
  "engines": {
    "node": ">= 16.0.0",
    "npm": ">= 6.0.0",
    "yarn": "^0.13.0"
  },
   "browserslist": [
    "> 1%",
    "last 2 versions",
    "not ie <= 8"
  ],
  "os": ["darwin", "linux"]
}
```





### 信息描述

可选值的格式和标准的 json 文件格式相同

**author**：列出软件包的作者名称

```json
{
  "author":{
    "name":'taly',
    "email":'taly@163.com'
  },
  "author":"Fall"
}
```

**contributors**：贡献者

```json
{
  "contributors":['personA','personB'],
  "contributors":[
    {
      "name":'Person',
      "email":"sss@199.com",
      "url":"http://nodejs.cn"
    }
  ]
}
```

**bugs**：连接到软件包的问题跟踪器，最常用的是 GitHub 的 issues 页面

```json
{
  "bugs":"https://github.com/sosos/issues"
}
```

**homepage**：设置软件包的主页

```json
{
  "homepage":"http:nodejs.cn"
}
```

**license**：软件包的许可证

```json
{
  "license":"MIT"
}
```

**keywords**：属性包含与软件包相关的关键字词组

```json
{
  "keywords":[  "email","machine learning","ai"]
}
```

**repository**：指定了程序包仓库所在的位置

```json
{
  "repository":"github:nodejscn/node-api-cn",
  "repository":{
    "type":"svn",
    "url":""
  }
}
```

### 软件包版本描述

**语义化版本控制**：简单来讲所有版本都有三个数字

比如说：`2.6.5`

- 第一个数字是主板本，进行不兼容的 API 更改时，升级主板本。
- 第二个数字是次版本，当你做了向下兼容的功能性新增，升级次板本。
- 第三个数字是补丁版本，向后兼容的缺陷修复时，升级补丁版本

语义化符号控制：

| 符号        | 示例             | 含义                                                  |
| ----------- | ---------------- | ----------------------------------------------------- |
| `~`         | `~0.13.0`        | 只更新补丁版本 `0.13.1`、`0.13.2` 可以，`0.14.0` 不行 |
| `^`         | `^2.2.1`         | 更新补丁版本和次版本                                  |
| `*`         | `*`              | 接受所有更新，包括主版本升级                          |
| `>`         | `>2.2.1`         | 接受高于指定版本的任意版本                            |
| `<`         | `<2.2.1`         | 接受低于指定版本的任何版本                            |
| `<= `、`>=` | `<=2.2.1`        | 大于等于，或者小于等于指定版本                        |
| `latest`    | `latest`         | 使用可用的最新的版本                                  |
| `-`         | `2.1.0-2.6.2`    | 接受一定范围的版本                                    |
| `||`        | `< 2.1 || > 2.6` | 组合集合                                              |
| 无符号      | `2.2.1`          | 只接受特指的版本                                      |

## package-lock.json

`package-lock.json` 和 `package.json` 文件一样，只不过， `package-lock.json` 会固化当前安装的每个软件包的版本，当运行 `npm install` 时，`npm` 会使用这些确切的版本。如果不存在，就会自动生成该文件。

没有 `package-lock.json` 时，会通过包名查找位置，然后包的依赖，之后进行安装，有了`package-lock.json` 后，可以直接从 package-lock.json 中直接查找地址进行下载，在 npm 5.0.0 之后的版本支持该特性。即，安装时更快，更高效。

`package-lock.json` 文件需要被提交到 Git 仓库，以便被其他人获取（如果项目是公开的或有合作者，或者将 Git 作为部署源）。

其它的包管理器也有类似于 `package-lock.json` 的功能，比如说 `yarn` 工具中的 `yarn.lock` 文件，和 `pnpm` 包管理工具中的

**为什么单一的 package-lock.json 不能确定唯一的依赖树？**

不同的 npm 版本导致的 npm 安装依赖的策略和算法不同，根据 `package.json` 中的 [semver-range version](https://link.juejin.cn?target=https%3A%2F%2Fdocs.npmjs.com%2Fcli%2Fv6%2Fusing-npm%2Fsemver) 更新依赖，可能某些依赖自上次安装以后，己经发布了新的版本。

## 资料参考

| 文章       | 链接                           |
| ---------- | ------------------------------ |
| 语义化版本 | https://semver.org/lang/zh-CN/ |

