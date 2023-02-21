> Create by **fall** on ——
> Recently revised in 2022-08-16

## nvm 的使用

nvm 是 node 版本控制工具

> 注：windows 上运行的 nvm 和 linux & MacOS 上的 nvm 工具不是一个项目，它们是两个团队做出来的东西。

nvm（Linux、Unix、OS X）的安装：https://github.com/creationix/nvm

nvm（Windows）安装：https://github.com/coreybutler/nvm-windows

### 常用命令

```bash
# 安装最新版本的 node
nvm install node
nvm install latest
# 当前所拥有的 node 的版本
nvm list
nvm ls
# 切换到淘宝镜像
nvm use taobao
# 全局安装 nvm 命令
npm install -g nvm
# 当前nvm工具的版本
nvm -v
# 使用 12.22.12 版本的 node
nvm use 12.22.12
# 卸载该版本的 node.js
nvm uninstall 8.4.0
```

## 参考文章

| 文章            | 链接   |
| --------------- | ------ |
| 深入浅出 nodejs | 第二章 |



