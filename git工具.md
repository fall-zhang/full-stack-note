> **下载：**
>
> 从淘宝镜像上下载git
>
> https://npm.taobao.org/mirrors/git-for-windows/

## git版本控制

**初始化命令**

> 工作区-> 暂存区->远程仓库
>
> `git init` 在本地进行初始化（建立工作区）
>
> `.git` 存储当前项目的所有版本信息

### 远程仓库操作

> 连接克隆远程仓库 git clone https://https://e.coding.net/colorfree/P-weather.git
>
> 在项目的文件夹中打开`cmd命令行工具`（一般为含有readme的文件夹）
>
> `git add . `      		将代码添加到版本里面（添加到暂存区）
>
> `git commit -m`	“放置你想添加的内容” 
>
> 最后使用 `git push` 将本地库里面的代码提交到网络共享库里面

`git push origin master`

> 推到master上

### 生成密钥

> 命令行中执行命令：
>
> `ssh-keygen -t rsa -C "xxxx@gmail.com"` 必须填写自己使用的邮箱

### 分支操作

> 查看当前分支状态：`git status` 
>
> 切换到master分支下：`git checkout master`
>
> 创建名为`branchname`的分支`git checkout -b branchname`
>
> -b 意思为新建
>
> 获取当前分支`git branch`
>
> 打星号的是当前使用的分支
>
> 把login合并到当前分支`git merge login`
>
> 将当前子分支推到一个新创建的login分之中`git push -u origin login`
>
> -u origin 推送到该origin分支中

### 其他功能

> - 查看远程仓库`git remote -v`
> - 删除分支：`git branch -D dev`
> - 远程删除分支：`git push origin :dev`
> - 退回到上一个版本：`git reset --hard head`
> - 查看日志：`git log 或者 git reflog`
> - 查看工作区和暂存区版本区别`git diff`
> - 回退上一个版本`git reset --hard HEAD^` 每多一个`^`多回退一个版本
> - 回退到指定版本`git reset --hard version` version为版本号

