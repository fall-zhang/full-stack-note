> Create by **fall** on 12 Apr 2023
> Recently revised in 12 Apr 2023

## Nginx

开源、高性能、可靠的 web 反向代理服务器。

其占用内存少、并发能力强、能支持高达 5w 个并发连接数

适用协议：Nginx 仅能支持 http、https 和 Email 协议

### 应用场景

**Web 服务器**

静态资源代理，高性能 WEB 服务器软件，与 Apache 相比，它支持更多的并发连接且占用服务器资源少

**反向代理或负载均衡**

负载均衡（将同一个请求转到不同的服务器上），作为 HTTP SERVER 或 DB 等服务器的代理服务器，代理功能相对简单，不及（Haporxy）邮件代理服务软件。

**缓存服务器**

作为缓存服务器，类似于专业的缓存软件

> Nginx 和 Node.js 的很多理念类似， HTTP 服务器、事件驱动、异步非阻塞等，且 Nginx 的大部分功能使用 Node.js 也可以实现，Nginx 擅长于底层服务器端资源的处理， Node.js 更擅长上层具体业务逻辑的处理，两者可以完美组合。

### 安装

```bash
# 安装 nginx
yum install nginx -y
# 命令查看 Nginx 的安装信息：
rpm -ql nginx 
```

目录结构文件夹有两个：

```shell
# Nginx配置文件
/etc/nginx/nginx.conf # nginx 主配置文件
/etc/nginx/nginx.conf.default

# 可执行程序文件
/usr/bin/nginx-upgrade
/usr/sbin/nginx

# nginx库文件
/usr/lib/systemd/system/nginx.service # 用于配置系统守护进程
/usr/lib64/nginx/modules # Nginx模块目录

# 帮助文档
/usr/share/doc/nginx-1.16.1
/usr/share/doc/nginx-1.16.1/CHANGES
/usr/share/doc/nginx-1.16.1/README
/usr/share/doc/nginx-1.16.1/README.dynamic
/usr/share/doc/nginx-1.16.1/UPGRADE-NOTES-1.6-to-1.10

# 静态资源目录
/usr/share/nginx/html/404.html
/usr/share/nginx/html/50x.html
/usr/share/nginx/html/index.html

# 存放Nginx日志文件
/var/log/nginx
```

- `/etc/nginx/conf.d/` 是子配置项存放处， `/etc/nginx/nginx.conf` 主配置文件会默认把这个文件夹中所有子配置项都引入；
- `/usr/share/nginx/html/` 静态文件都放在这个文件夹，也可以根据你自己的习惯放在其他地方；

### 配置文件

```yaml
# main段配置信息
user  nginx;                        # 运行用户，默认即是nginx，可以不进行设置
worker_processes  auto;             # Nginx 进程数，一般设置为和 CPU 核数一样
error_log  /var/log/nginx/error.log warn;   # Nginx 的错误日志存放目录
pid        /var/run/nginx.pid;      # Nginx 服务启动时的 pid 存放位置

# events段配置信息
events {
    use epoll;     # 使用epoll的I/O模型(如果你不知道Nginx该使用哪种轮询方法，会自动选择一个最适合你操作系统的)
    worker_connections 1024;   # 每个进程允许最大并发数
}

# http段配置信息
# 配置使用最频繁的部分，代理、缓存、日志定义等绝大多数功能和第三方模块的配置都在这里设置
http { 
    # 设置日志模式
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;   # Nginx访问日志存放位置

    sendfile            on;   # 开启高效传输模式
    tcp_nopush          on;   # 减少网络报文段的数量
    tcp_nodelay         on;
    keepalive_timeout   65;   # 保持连接的时间，也叫超时时间，单位秒
    types_hash_max_size 2048;

    include             /etc/nginx/mime.types;      # 文件扩展名与类型映射表
    default_type        application/octet-stream;   # 默认文件类型

    include /etc/nginx/conf.d/*.conf;   # 加载子配置项
    
    # server段配置信息
    server {
     listen       80;       # 配置监听的端口
     server_name  localhost;    # 配置的域名
      
     # location段配置信息
     location / {
      root   /usr/share/nginx/html;  # 网站根目录
      index  index.html index.htm;   # 默认首页文件
      deny 172.168.22.11;   # 禁止访问的ip地址，可以为all
      allow 172.168.33.44；# 允许访问的ip地址，可以为all
     }
     
     error_page 500 502 503 504 /50x.html;  # 默认50x对应的访问页面
     error_page 400 404 error.html;   # 同上
    }
}
```





### 相关命令

```bash
# 开机配置
systemctl enable nginx # 开机自动启动
systemctl disable nginx # 关闭开机自动启动

# 启动Nginx
systemctl start nginx # 启动Nginx成功后，可以直接访问主机IP，此时会展示Nginx默认页面

# 停止Nginx
systemctl stop nginx

# 重启Nginx
systemctl restart nginx

# 重新加载Nginx
systemctl reload nginx

# 查看 Nginx 运行状态
systemctl status nginx

# 查看Nginx进程
ps -ef | grep nginx
```





## 参考文章

| 作者   | 文章名称                                                     |
| ------ | ------------------------------------------------------------ |
| 民工哥 | [2W 字总结 ！体系化带你全面认识 Nginx](https://segmentfault.com/a/1190000039873208) |

