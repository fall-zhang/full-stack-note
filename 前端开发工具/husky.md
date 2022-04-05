> Create by **fall** on 2022-04-05
> Recently revised in 2022-04-05

## husky

用于将代码推送到 git 上

```bash
npm i lint-staged husky -D
npm set-script prepare "husky install" # 在 package.json 中添加脚本
npm run prepare # 初始化 husky，将 git hooks 钩子交由，husky 执行
```

在初始化之后，会在根目录创建 `.husky` 文件夹

添加命令：`npx husky add .husky/pre-commit "npx lint-staged"`

lint-satged 用于 lint 的缓存。





## 参考文章

| 作者             | 链接                                       |
| ---------------- | ------------------------------------------ |
| jpliu            | https://juejin.cn/post/7038143752036155428 |
| 啥也不是的小垃圾 | https://juejin.cn/post/6982192362583752741 |

