## shell命令

### 命令格式

命令格式： 命令 [选项] [操作]

命令：要执行的操作		嫖娼

选项：怎么去做				网站，电线杆，小胡同	

参数：执行的目标			包小姐，包大姐，

#### pwd

- 显示当前目录

#### ls

- 显示当前目录所有文件和文件夹。

选项

- -a     列出所有文件和文件夹，包括隐藏的文件夹
- -l      以长格式显示文件和文件夹，长格式显示多种信息（修改时间，权限，大小）

> 可以直接书写为  ll   即  ls -l的缩写

书写方法

```shell
ls -la /etc
```

#### whoami

- 输出当前用户名

### 文件管理

#### touch:

- 创建或者修改文件的修改时间

#### cp

把一个文件复制到另一个文件中(copy)

- -r  
- -f

#### rm:  remove

用做删除文件和文件夹

- -f
- -r

`rm -rf /*`   :执行这个命令之后，可以跑路了。删除所有文件和文件夹

#### cat

用于查看文档，适合文档少的一部分

```
cat install.log
```

| 

把第一个命令的结果当作第二个命令的参数

####　more

从前向后进行信息检索

- 回车：显示一行
- 空格：显示下一页
- q：退出检索

#### less

从后向前进行信息检索

- 回车：显示一行
- 空格：显示下一页
- q：退出检索

#### head 

看开头的几行代码

```
head 20 
tail 20 -f  
只看后20行代码，并且持续刷新
```

### 系统管理



shutdown:关机或者重启

- -h 关机
- -r 重启

####　who

> 查看当前服务器用户列表

#### whoami

> 我是谁

#### ping 

> 结束命令操作Ctrl+c
>
> ping ip或者域名

#### hostname

>  查看服务的主机名

​	修改主机名和IP地址的映射：/etc/hosts

​	vim /etc/hosts

点击o，进入到编辑模式

按输入":wq"，保存并推出

#### ps

查看服务器进程

ps -ef :查看所有进程

#### kill

- -9 强制杀死进程

  进程号，发送信号让它自杀

#### netstat

查看网络端口号  8080  3306  1521   查看谁占用了这个端口，然后杀了他

- -nlptu
- 我们远程连接的时候用的是ssh协议

curl

抓取网页内容，部署项目到tomcat，或者部署web项目

```shell
curl www.searchtop.top
```

wget

```shell
wget http://down.qq.com/lol/dltools/LOL_V4.2.1.1_FULL_0_tgod_signed.exe
```

### 用户管理

- linux 分成 用户和组的概念

- 任何用户都属于某个或者某几个组

- 一个组内包含多个用户

- 拥护和组的关系是多对多

####　useradd

添加用户(需要root权限)

```shell
useradd zhangsan 
```

password 

配置密码

```shell
password zhangsan
```

#### su

切换用户

```
su 和 su- 的区别是，su只切换了root身份，shell环境仍然是普通用户，su-连环境也一起切换到shell中  
echo  $path 输出可以使用的环境变量
```

#### userdel 

删除用户

userdel zhangsan

把张三杀了，

- -r 把人杀了，把家拆了（home路径下的文件夹都没文件权限了）

### 文件权限

`ll` 查看文件权限

#### drwxr-x--x

第一个字母是文件的类型：

rwx: 代表的是文件所有者的权限

r-x: 代表的是文件所属组的权限

--x : 代表其他用户的权限

权限的表示方法，

- r: 可读
- w: 可写
- x：可移植性

数字表示权限

| 原表示法 | 二进制表示 | 转化为数字 |
| -------- | ---------- | ---------- |
| rwx      | 111        | 7          |
| r-x      | 101        | 5          |
| --x      | 001        | 1          |

#### chmod 修改权限

`chmod [ugoa] [+-=] [rwx]`

> - u:  拥有者
> - g：拥有组
> - o：其他人
> - a：所有人，以上三者

> - +:  添加
> - -:  删除
> - =:  赋值

```shell
chomd u+x 1.txt
```

### 压缩包管理

**压缩**

`tar -zcvf java.tar.gz 1.txt 2.txt movie`

- -z  压缩方式
- -c  创建压缩包
- -v  显示压缩信息
- -f   执行压缩包文件

**查看**

- `tar -tf java.tar.gz`

**解压**

- `tar -xvf java.tar.gz` 解压到当前文件夹内
- `tar -xvf java.tar.gz -C java` 解压到`java`文件夹内
    - -x  解压
    - -v  显示解压过程
    - -f  解压那个文件
    - -C  解压位置

### VIM

三种模式

- 编辑模式 ：o   i
- 命令模式:  进入后默认
- 行末模式：  set nu

进入编辑模式

- i   I
- a  A
- o  O
- s  S

末行模式：

- w 保存
- w  filename    另存为
- q  退出
- wq   保存并推出
- q！  强制退出
- wq！  保存并且强制退出
- set nu：显示行号

命令行模式：

>- G：最后一行
>- nG：第n行
>- gg：第一行

>^:  行首
>
>$:  行尾

> dd
>
> ndd

> P  粘贴当前行上面
>
> p  粘贴当前行下面

> yy: 复制
>
> nyy : 复制n行

> r: 替换一个字符
>
> R : 替换，直到esc停止

> u : 撤回操作
>
> ctrl+r : 前进操作=> 撤销撤回的操作

### linux软件的安装

1. 绿色版

    下载一个tar-解压-使用

2. rpm：RPM 

    - 对应的安装包
    - 问题：安装A软件的时候，如果A依赖于BC软件，需要用户手动下载并且安装BC软件后继续执行A的炒作
    - 解决方案：yum，有个在线的软件仓库

3. 源码安装：源码----gcc编译----安装



####　查询rpm

`rpm -qa` 查询 

`rpm -qa |grep java` 筛选查询结果

卸载： -e

`rpm -e`    

安装 ：

> rpm -ivh xxx.rpm

#### 环境变量的配置

查看yum仓库

​	`yum repolist all`

命令行上传，下载

rz 选中文件打开

sz 文件名

seLinux :主要有美国国家安全局开发，2.6及以上版本的linux内核已经集成了SELinux模块



mysql -u root -p登录

## 快捷键



ctrl+l 清屏

