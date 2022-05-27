> Create by **fall** on ——
> Recently revised in 2022-02-08

## package.json

package.json 是一个项目清单，可以做很多互不相关的事情

存储元数据：元数据就是描述数据信息的数据

- 工具的配置中心（可以在该文件内放置工具的配置）
- npm 和 yarn 存储所有已经安装的包的名称和版本的地方。

最简单的 package.json 文件：

```json
{} // 真的很简单 ^_^
```

package.json 的文件当然要符合语法规范

```json
{
  name:'my_demo'
}
```

> 命令行工具快速创建 package.json ： `npm init` 初始化当前环境。
>
> `npm init -y` 或者 `npm init -yes` 快速创建

### 属性值含义

所有属性都可以通过 npm 或者其它工具使用

| 值           | 作用                                                  |
| ------------ | ----------------------------------------------------- |
| name         | 设置应用程序 / 软件包的名称                           |
| version      | 表明当前的版本                                        |
| main         | 设置应用程序需的入口点                                |
| description  | 应用程序 / 软件包的简短描述                           |
| private      | 私有，设置后可以防止应用程序 / 软件包被意外发布到 npm |
| scripts      | 定义了一组可以运行的 node 脚本                        |
| dependencies | 设置了作为依赖安装的 npm 安装包列表                   |
| engines      | 设置了此软件包 / 应用，在哪个版本的 node 上运行       |
| browerslist  | 告知支持哪些浏览器                                    |

> name 必须小于 214 个字符，不能包含空格，只能包含小写字母、连字符(`-`)、下划线（`_`）

### 其它可选值

> 和标准的 json 文件格式相同即可

**author**：列出软件包的作者名称

```json
{
  "author":{
    "name":'Taly',
    "email":'taly@163.com'
  }
}
```

**contributors**：贡献者

```json
// 写法1
{"contributors":['personA','personB']}
// 写法2
{
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

> 写法：`"bugs":"https://github.com/sosos/issues"`

**homepage**：设置软件包的主页

> `"homepage":"http:nodejs.cn"`

**license**：软件包的许可证

> `"license":"MIT"`

**keywords**：属性包含与软件包相关的关键字词组

```json
{
  "keywords":[  "email","machine learning","ai"]
}
```

**repository**：指定了程序包仓库所在的位置

> `"repository":"github:nodejscn/node-api-cn"`

```json
"repository":{
  "type":"svn",
  "url":""
}
```

**devDependencies**：设置作为开发依赖安装的 `npm` 软件包的列表

即使用 `npm install --dev <PACKAGENAME>` 命令安装的会自动插入到该列表中

**engines**：表明软件包 / 应用程序要运行的 node.js 或其它版本

```json
"engines": {
  "node": ">= 6.0.0",
  "npm": ">= 3.0.0",
  "yarn": "^0.13.0"
}
```

**browserslist**：支持的浏览器版本

```json
"browserslist": [
  "> 1%",
  "last 2 versions",
  "not ie <= 8"
]
```

### 软件包版本描述

**语义化版本控制**：简单来讲所有版本都有三个数字

比如说：`2.6.5`

- 第一个数字是主板本，进行不兼容的 API 更改时，升级主板本。
- 第二个数字是次版本，进行不兼容的 API 更改时，升级主板本。
- 第三个数字是补丁版本，向后兼容的缺陷修复时，升级补丁版本

> - `~`：如果写入是 `~0.13.0` 则只更新补丁版本 `0.13.1` 可以 `0.14.0` 不行
> - `^` ：如果写入的是 `^` 表示需要更新补丁版本和次版本 `0.13.1` `0.14.0`
> - `*` ：如果写入 `*` 表示接受所有更新，包括主版本升级
> - `>` ：接受高于指定版本的任意版本
> - `<` ：接受低于指定版本的任何版本
> - `<= `和 `>=` ：接受大于等于，或者小于等于指定版本的任何版本
> - 无符号：只接受特指的版本
> - `latest` ：使用可用的最新的版本
> - `-`: 接受一定范围的版本。例如：`2.1.0 - 2.6.2`。
> - `||`: 组合集合。例如 `< 2.1 || > 2.6`。

## package-lock.json

package-lock.json 和 package.json 文件一样，只不过， package-lock.json 会固化当前安装的每个软件包的版本，当运行 `npm install`时，`npm` 会使用这些确切的版本。如果不存在，就会自动生成该文件。

> 为什么单一的 package-lock.json 不能确定唯一的依赖树？
>
> 不同的 npm 版本导致的 npm 安装依赖的策略和算法不同，根据 `package.json` 中的 [semver-range version](https://link.juejin.cn?target=https%3A%2F%2Fdocs.npmjs.com%2Fcli%2Fv6%2Fusing-npm%2Fsemver) 更新依赖，可能某些依赖自上次安装以后，己经发布了新的版本。

> 没有 `package-lock.json` 时，会通过包名查找位置，然后包的依赖，之后进行安装，有了`package-lock.json` 后，可以直接从 package-lock.json 中直接查找地址进行下载，在 npm 5.0.0 之后的版本支持该特性。即，安装时更快，更高效。
>
> `package-lock.json` 文件需要被提交到 Git 仓库，以便被其他人获取（如果项目是公开的或有合作者，或者将 Git 作为部署源）。

