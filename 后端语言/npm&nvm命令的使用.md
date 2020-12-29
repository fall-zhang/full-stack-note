## NPM命令的使用

### NPM下载

> LTS:  Long Term Support
>
> [官方网址](https://nodejs.org)  https://nodejs.org
>
> [安装npm组件](https://www.npmjs.com/)  https://www.npmjs.com

NPM 是随同 Node.js 一起安装的包管理工具，以便解决 Node.js 代码部署上的很多问题

- 允许用户从NPM服务器下载别人编写的**第三方包**到本地使用。
- 允许用户从NPM服务器下载并安装别人编写的**命令行程序**到本地使用。
- 允许用户将自己编写的包或命令行程序上传到NPM服务器供别人使用。

**配置环境变量意义** ：配制好环境变量后在任何文件夹下都可以使用该命令

### npm包安装位置

- 本地的安装包：使用`npm install <package-name>` 安装，并且放置在node_modules文件夹中
- 全局的安装包：`npm install <package-name> -g` 全局安装，并放在固定的位置

> **通常所有软件包都应该本地安装**，可以确保计算机中有数十个应用程序，如果需要，每个应用都可以运行不同的版本。更新全局安装包时，所有的项目都使用新的版本，可能导致维护上的噩梦，可能会破坏原来的依赖项和兼容性等。

### npm命令

检测是否安装成功：`npm -v`

**安装或者更新包**

> 从官网进行安装
> npm install npm -g
>
> 安装淘宝镜像
> npm install -g cnpm --registry=https://registry.npm.taobao.org
>
> 之后就可以通过 cnpm 代替 npm 进行安装
>
> **其它特性**
>
> 可执行文件会放在 `node_modules` 文件夹内的 `.bin` 下。
>
> `./node_modules/.bin/cowsay` 可以输入该路径和名称运行它，但 `npx` 命令更方便，直接使用 `npx cowsay`

**卸载命令**

> `npm uninstall <package-name>`  卸载 node.js 指定的包
>
> `npm uninstall <package-name> -g` 安装全局模块 -g 后进行全局模块的卸载
>
> 如果安装时使用 -S(即--save) ，卸载时必须添加 -S ，移除在 package.json 中的引用
>
> 同理，使用-D(--save-dev)，卸载时必须添加 -D

**其他命令**

> `npm list`  列出当前工作区已经安装模块
>
> `npm list -g`  查看全局安装的模块（会查找所有全局安装模块，使用`npm list -g --depth 0`）
>
> `npm root -g` 查看全局模块的安装路径(使用nvm管理工具，位置可能会不同)
>
> `npm search <key-word>` 按照关键字搜索模块
>
> `npm init`  创建JSON文件，初始化开发环境
>
> `npm update` 升级当前目录下的项目的所有模块
>
> `npm view <package-name> version` 查看当前最新的版本
>
> `npm view cowsay versions` 查看软件包所有版本
>
> `npm publish` 发布模块

**命令详解**

```markdown
npm install gulp@3.9.1 --save-dev
使用 npm 安装 gulp 特定版本
--save  表示安装在当前文件夹下
--save  的简写为： -S
-dev    将安装的信息保存在package.json中
--save-dev 会将其视为开发依赖项，添加到 devDependencies 列表，简写为：-D
gulp@3.9.1 表示下载 3.9.1版本的gulp
npm install gulp@3.9.1 --sava-dev 的简写:
npm i gulp@3.9.1 -D
```

### 语义化版本控制

简单来讲所有版本都有三个数字

- 第一个数字是主板本
- 第二个数字是次版本
- 第三个数字是补丁版本

发布版本跟新时，遵循以下原则

- 进行不兼容的 API 更改时，升级主板本。
- 向后兼容方式添加功能时，升级次版本
- 向后兼容的缺陷修复时，升级补丁版本

### NPX工具

> npx是一个工具，可以自动寻找当前文件夹(node_modules)文件夹下的可执行插件，正确引用并且执行
>
> 如果当前文件夹下没有下载可执行插件，那就会在网络中寻找后运行
>
> `npx cowsay hello world`
>
> 和 node 特定版本结合，`npx node@10 -v #10.18.1`

### npm插件的安装

#### PostCSS

> `npm install postcss-cli -g`
>
> PostCSS 是一个运行环境，用于使用 JavaScript 改变 CSS 的环境
>
> 官方解释：A tool for transforming CSS with JavaScript

**postcss-sprites**

> `cnpm i postcss-sprites`
>
> 将多张图片自动合成为一张图片(雪碧图|sprites)

```js
const sprites = require('postcss-sprites');
module.exports = {
	plugins :[
		cssnext,
		stylelint({
            "rules" : {
            "color-no-invalid-hex" true;
            }
		}),
		sprites({
		spritePath : './dist'
		})
	]
}
```

**postcss-cssnext**

> `cnpm i postcss-cssnext`
>
> 对css进行降级，支持更早的浏览器版本

```js
const cssnext = require('postcss-cssnext');
module.exports = {
	plugins :[
		cssnext
	]
}
```

**postcss-import**

> `cnpm i postcss-import`
>
> 对于多个css文件进行合并

```js
const postcss = require('postcss-import');
module.exports = {
	plugins :[
		postcss
	]
}
```

#### autoprefixer

> `cnpm i autoprefixer`
>
> 自动添加浏览器前缀，进行浏览器兼容

```javascript
// 配置文件中引入
const autoprefixer = require('autoprefixer');
module.exports = {
	plugins :[
		autoprefixer({
			browsers : ['> 0%']// 对所有浏览器兼容
		})
	]
}
```

#### stylelint

> 命令行安装`cnpm i stylelint`
>
> 进行CSS文本纠错

```js
const cssnext = require('postcss-cssnext');
module.exports = {
	plugins :[
		cssnext,
		stylelint({
            "rules" : {
            "color-no-invalid-hex" true;
            }
		})
	]
}
```

#### Animate.css

> `npm install animate.css --save`
>
> animate.css 是一些CSS动画的集成

#### cssnano

> `cnpm i cssnano`
>
> 对于css进行压缩

```js
const postcss = require('postcss-import');
module.exports = {
	plugins :[
		cssnano
	]
}
```

## nvm命令的使用

> nvm是用来对node进行版本控制的工具
>
> windows上的nvm和linux&MacOS上的nvm工具不是一个项目，不是一个团队做出来的东西

#### nvm(Linux、Unix、OS  X)的安装

安装教程网址：https://github.com/creationix/nvm

#### nvm(Windows)

安装教程网址：https://github.com/coreybutler/nvm-windows

### 命令行工具

> nvm install node & nvm install latest (安装最新版本的node)
>
> nvm list  &   nvm ls 当前所拥有的npm版本
>
> nvm use taobao 切换到淘宝镜像
>
> cnpm install -g nvm  全局安装nvm命令
>
> nvm -v 当前nvm工具的版本
>
> nvm use 8.4.0 使用8.4.0版本的node
>
> nvm uninstall 版本号 卸载该版本的node.js


