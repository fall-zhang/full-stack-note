> Create by **fall** on:2021-08-23
> Recently reviced in:2022-04-05

## yarn 

yarn参考链接

yarn 和 pnpm 都是为了解决 npm 上出现的一些固有的错误，而进行开发的。

### 安装插件

`yarn` 或者是 `yarn install`

### 添加插件

`yarn add [packageName]`

### 更新插件

`yarn upgrade [packageName]`

### 移除插件

`yarn remove [packageName]`

### yarn 的意义

比起 npm，yarn 解决了 npm 最初设计上的一些问题。

**确定性**: npm v5 之前并没有 package-lock.json 机制（只有默认并不会使用的 npm-shrinkwrap.json），yarn 通过 yarn.lock 等机制，让依赖即使是不同的安装顺序，相同的依赖关系在任何的环境和容器中，都可以以相同的方式安装。

**采用模块扁平化的安装模式:** 将不同版本的依赖包，按照一定的策略，归结为单个版本;以避免创建多个版本造成工程的冗余（目前版本的npm 也有相同的优化）

**网络性能更好:** `yarn` 采用了请求排队的理念，类似于并发池连接，能够更好的利用网络资源，同时也引入了一种安装失败的重试机制。

**采用缓存机制,实现了离线模式** (目前的 npm 也有类似的实现)

### 安装机制

检测（checking）---> 解析包（Resolving Packages）---> 获取包(Fetching) ---> 链接包(Linking Packages) ---> 构建包(Building Packages)

**检测包**

目的就是检测我们的项目中是否存在 npm 相关的文件,比如`package-lock.json`等；如果有，就会有相关的提示用户注意：这些文件可能会存在冲突。在这一步骤中也会检测系统 OS，CPU 等信息。

**解析包**

解析依赖树中的每一个包的信息，首先，获取到首层依赖，即当前所处的项目中的 `package.json` 定义的 `dependencies`、`devDependencies`、`optionalDependencies` 的内容。

紧接着**会采用遍历首层依赖的方式来获取包的依赖信息**，以及递归查找每个依赖下嵌套依赖的版本信息，并将解析过的包和正在进行解析包呢`用Set数据结构进行存储`，这样就可以保证`同一版本范围内的包`不会进行重复的解析。

举个例子

- 如果 A 包没有解析过，首次尝试从 `yarn.lock` 中获取版本信息，并且标记为已解析
- 如果在`yarn.lock`中没有找到包A， 则向`Registry`发起请求获取满足版本范围内的已知的最高版本的包信息,获取之后将该包标记为已解析。

解析包之后，已经确定了包的具体版本信息和包的下载地址。

**获取包**

这一步首先我们会检查缓存中是否有当前依赖的包，同时呢将缓存中不存在的包下载到缓存的目录中。但是这里有一个小问题需要大家思考一下:

比如：如何去判断缓存中有当前的依赖包呢？

yarn 中会根据 `cacheFolder+[slug]+node_modules+pkg.name` 生成一个路径，判断系统中是否存在该 path，如果存在证明已经有缓存，不用重新下载。这个 path也就是依赖包缓存的具体路径。

> 基于字符串位置参数绑定的 URL 方式，被称为 **slug**。

那么对于没有命中的缓存包呢？在 `Yarn` 中存在一个 Fetch 队列，按照具体的规则进行网络请求。如果下载的包是一个 file 协议，或者是相对路径，就说明指向一个本地目录，此时会调用 Fetch From Local 从离线缓存中获取包，否则调用 Fetch From External 获取包，最终获取的结果使用 fs.createWriteStream 写入到缓存目录。

**链接包**

把项目中的依赖复制到 `node_modules` 目录下，并且需要目录扁平化。复制依赖之前，`Yarn` 会先解析 `peerDepdencies`，如果找不到符合要求的`peerDepdencies` 的包，会有 `warning` 提示，并最终拷贝依赖到项目中。

**构建包**

如果依赖包中存在二进制包需要进行编译，那么会在这一步进行。

比如 `package-lock.json` 下面的一条内容

```
"@babel/highlight@^7.10.4":
  version "7.16.10"
  resolved "https://registry.npmjs.org/@babel/highlight/-/highlight-7.16.10.tgz"
  integrity sha512-5FnTQLSLswEj6IkgVw5KusNUUFY9ZGqe/TRFnP/BKYHYgfh7tc+C7mwiy95/yNP7Dh9x580Vv8r7u7ZfTBFxdw==
  dependencies:
    "@babel/helper-validator-identifier" "^7.16.7"
    chalk "^2.0.0"
    js-tokens "^4.0.0"
```

其中：

- `version` 表示版本
- `resolved` 表示依赖包的安装源，即下载地址。
- `integrity` 表示完整性的 Hash 值
- `dependencies` 表示它的依赖包

## PNPM

> Fast, disk space efficient package manager.

pnpm 的[官方文档](https://pnpm.io/zh/pnpm-cli)

特点：空间利用率高，极快的安装速度

安装：`npm i pnpm -g`

> 幽灵依赖，比如 moment.js 被 antd 引用，在 package.json 中安装 antd，然而 `import` 的时候，能引用 moment.js ，此时就成为幽灵依赖，是 yarn 或者 npm，为了避免引用嵌套引用，拍平了依赖，导致的问题。

### pnpm 如何工作

在 `node_modules` 中，会产生一个 `.pnmp` 文件夹，用于存放目录树（文件夹名），被称为虚拟存储目录，通过 `package-name>@<version>` 实现相同模块不同版本之间隔离和复用。

那么如何将这些文件夹和资源关联？

`Store` + `Links`

Store

pnpm 资源在磁盘上的存储位置

Mac/Linux 中会设置在 `{home dir}>/.pnpm-store/v3`；windows 会设置在当前目录的根目录，比如C（`C/.pnpm-store/v3`）、D盘（`D/.pnpm-store/v3`）。

可以在不同的磁盘上设置同一个存储，但在这种情况下，`pnpm` 将**复制包**而不是**硬链接**（详情可见 linux 章节，或者自行查询）它们。硬链接只能发生在同一文件系统同一分区上。

需要注意的是一般用户权限下只能硬链接到文件，**不能用于目录**。

Links

比如说 100 个项目中用到了 lodash，`npm` 和 `yarn` 会安装 100 次，而 pnpm 只会安装一次，之后都会使用 `hardlink` 硬链接。

由于`hark link`只能用于文件不能用于目录，但是`pnpm` 的 `node_modules` 是树形目录结构， 通过 `symbolic link`（也可称之为软链或者符号链接）来链接到文件。

全局的 Store 也会存在一些问题，比如：store 会随着时间越来越大，所以使用 `pnpm store prune` 命令解决问题。
比如：有个包 `axios@1.0.0` 被一个项目所引用了，但是某次修改使得项目里这个包被更新到了 `1.0.1` ，那么 store 里面的 1.0.0 的 axios 就就成了个不被引用的包，执行 `pnpm store prune` 就可以在 store 里面删掉它了，注意不要经常使用。

### PeerDependencies

pnpm 的最佳特征之一是，在一个项目中，`package`的一个特定版本将始终只有一组依赖项。 这个规则有一个例外 -那就是具有 [peer dependencies ](https://docs.npmjs.com/files/package.json#peerdependencies)的`package`。

通常，如果一个`package`没有 peer 依赖项（peer dependencies），它会被硬链接到其依赖项的软连接（symlinks）旁的 `node_modules`，就像这样：

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/08fc3d6dd49f4d2a92d1d31a9a9999e6~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

如果 `foo` 有 peer 依赖（peer dependencies），那么它可能就会有多组依赖项，所以我们为不同的 peer 依赖项创建不同的解析：

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4dd2ecc8c09b4cf7a01d72e6f5113102~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

`pnpm`创建` foo@1.0.0_bar@1.0.0+baz@1.0.0` 或`foo@1.0.0_bar@1.0.0+baz@1.1.0`内到`foo`的软链接。 因此，Node.js 模块解析器将找到正确的 peers。

`peerDep`的包命名规则如下(看起来就很麻烦)

```
.pnpm/<organization-name>+<package-name>@<version>_<organization-name>+<package-name>@<version>/node_modules/<name>

// peerDep组织名(若无会省略)+包名@版本号_组织名(若无会省略)+包名@版本号/node_modules/名称(项目名称)
复制代码
```

> *如果一个`package`没有 peer 依赖（peer dependencies），不过它的依赖项有 peer 依赖，这些依赖会在更高的依赖图中解析*, 则这个传递`package`便可在项目中有几组不同的依赖项。 例如，`a@1.0.0` 具有单个依赖项 `b@1.0.0`。 `b@1.0.0` 有一个 peer 依赖为 `c@^1`。 `a@1.0.0` 永远不会解析`b@1.0.0`的 peer, 所以它也会依赖于 `b@1.0.0` 的 peer 。

如果需要解决peerDep引入的多实例问题，可以通过 [`.pnpmfile.cjs`](https://link.juejin.cn?target=https%3A%2F%2Fpnpm.io%2Fzh%2Fpnpmfile)文件更改依赖项的依赖关系。

### 命令的使用

命令和 npm 的使用极其相似

安装所有包

`pnpm install`

安装特定的包

`pnpm install <package-name>`

`pnpm update <package-name>` 更新包

将本地项目连接到另一个项目。注意，使用的是硬链接，而不是软链接。如:`pnpm link ../../axios`

### 支持 monorepo

### 配置

`shamefully-hoist=true` 可以让包名提升，即还可以实现幽灵引用

```
// .npmrc
shamefully-hoist=true
```

## 参考文章

| 作者          | 链接                                       |
| ------------- | ------------------------------------------ |
| 酒窝yun过去了 | https://juejin.cn/post/7060844948316225572 |
| 金虹桥程序员  | https://juejin.cn/post/7043998041786810398 |


