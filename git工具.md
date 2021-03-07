> **下载：** 从淘宝镜像上下载git
>
> https://npm.taobao.org/mirrors/git-for-windows/

<img src="http://www.ruanyifeng.com/blogimg/asset/2015/bg2015120901.png" alt="img" style="zoom:80%;" />

> - Workspace：工作区
> - Index / Stage：暂存区
> - Repository：仓库区（或本地仓库）
> - Remote：远程仓库

## git 工具

### git的介绍

**git 的使用流程**

- clone 克隆
- 提交commit 和推送 push
- 拉取 pull ，获取 fetch
- 版本回退 reset
- 检出 checkout
- 标签 tag

*****

**从远程克隆仓库 clone**

将远程的代码下载到本地

**提交 commit 和 push**

commit 将修改提交到本地仓库，push将本地仓库的内容提交到远程库

**拉取 pull 和 获取 fetch**

pull 将远程最新的代码拉取到本地，自动合并 merge

fetch 将远程最新的代码拉取到本地，不合并 merge

**版本回退**

reset 将代码回退到选定的版本

**检出checkout**

创建分支，切换分支

**标签 tag**

tag 就是给版本打个标记，方便识别

### 配置文件

`.config` 是git 的配置文件，可以用在用户主目录之下（全局配置），也可以用在项目目录下（项目配置）



## git 的操作

### 提交项目代码流程

> 连接克隆远程仓库 git clone https://https://e.coding.net/colorfree/P-weather.git
>
> 在项目的文件夹中打开`cmd命令行工具`（一般为含有readme的文件夹）
>
> `git add . `   	将代码添加到版本里面（添加到暂存区）
>
> `git commit -m`	“放置你想添加的内容” 
>
> 最后使用 `git push` 将本地库里面的代码提交到网络共享库里面

### 新建代码仓库

> - `git init` 在本地进行初始化（建立工作区）
> - `git init [project-name]` 新建一个目录，作为代码仓库
> - `git clone [url]` 
>
> `.git` 文件夹存储当前项目的所有版本信息

### 暂存区控制

```bash
$ git add [file1] [file2] ...  # 添加指定文件到暂存区
$ git add [dir] # 添加指定目录到暂存区，包括子目录
$ git add . # 添加当前目录的所有文件到暂存区

$ git add -p
# 确认所有文件的变化，并且有多个选项可作更改
# 对于同一个文件的多处变化，可以分多次提交

$ git rm [file1] [file2] ... # 删除工作区文件，并且将这次删除放入暂存区
$ git rm --cached [file] # 停止追踪指定文件，但该文件会保留在工作区
$ git mv [file-original] [file-renamed] # 改名文件，并且将这个改名放入暂存区
```

### 本地仓库

```bash
$ git commit -m "message" # 提交暂存区内容提交到仓库区
$ git commit [file1] [file2] ... -m [message] # 提交暂存区的指定文件到仓库区
$ git commit -a # 提交工作区自上次 commit 之后的变化，直接到仓库区
$ git commit -v # 提交时显示所有 diff 信息

$ git commit --amend -m [message]
# 使用一次新的commit，替代上一次提交
# 如果代码没有任何新变化，则用来改写上一次 commit 的提交信息 message

$ git commit --amend [file1] [file2] ... # 重做上一次commit，并包括指定文件的新变化
```

> `git push origin master`
>
> 推到 master 上

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
> 把 login 合并到当前分支`git merge login`
>
> 将当前子分支推到一个新创建的 login 分之中`git push -u origin login`
>

### 其他功能

> - 查看远程仓库`git remote -v`
> - 删除分支：`git branch -D dev`
> - 远程删除分支：`git push origin :dev`
> - 退回到上一个版本：`git reset --hard head`
> - 查看日志：`git log `或者` git reflog`
> - 查看工作区和暂存区版本区别`git diff`
> - 回退上一个版本`git reset --hard HEAD^` 每多一个`^`多回退一个版本
> - 回退到指定版本`git reset --hard version` version为版本号

