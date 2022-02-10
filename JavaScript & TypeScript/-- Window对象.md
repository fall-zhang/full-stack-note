> Create by **fall** on 2021-12-13
> Recently revised in 2021-12-13

Window 对象上的内容

## navigator

导航器对象，浏览器所处环境，和 cookie

```js
// 浏览器的代码名
navigator.appCodeName // "Mozilla"
// 浏览器的名称
navigator.appName // "Netscape"
// 浏览器平台和版本信息
navigator.appVersion // "5.0 (Windows)"
// 浏览器是否启用 cookie
navigator.cookieEnabled // true
// 运行浏览器的操作平台
navigator.platform // "Win32"
// user-agent 就是向服务器发送的请求头中的 user-agent
navigator.userAgent //"Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:95.0) Gecko/20100101 Firefox/95.0"
```

## screen

显示器对象

```js
// 显示屏幕的可用高度
screen.availHeight  // 1040
// 显示屏幕
screen.availWidth  // 1920
// 屏幕高度
screen.height // 1080
// 屏幕宽度
screen.width  // 1920
// 屏幕颜色的位数
screen.colorDepth // 32
```

## history

浏览器历史对象

```js
// 返回前一个URL
history.back()
// 返回下一个URL
history.forward()
// 前进后退
history.go(-1) // 回退一次
```

## Location

位置对象

```js
// 对象上的属性
// 哈希值，URL 中从 # 开始，之后的内容
location.hash() 
// 主机名，和当前的 URL 的端口号
location.host( // 主机名，或者是域名
// 完整的域名
location.href() // "https://limestart.cn/"
// 当前的网络请求路径
location.pathname // "/"
// 使用协议
location.protocol // "https:"
// 查询字符串
location.search //

// 对象上的方法
// 重新加载文档
location.assign(URL)
// 重新加载当前界面
location.reload()
// 用新的文档替换当前文档
location.replace(newURL)
```

## Document

集合

```js
// 描点对象数组
document.anchors[]
// 图片对象数组
document.images[]
// 连接对象数组
document.links[]
// 表单对象数组
document.forms[]
```

属性

```js
// 设置或者返回当前文档中有关的所有 cookie
document.cookie
// 当前文档的域名
document.domain
// 当前文档的 URL
document.referrer
// 当前文档的标题
document.title
```

方法

```js
// 打开一个新的文档，并擦除旧文档内容
document.open()
// 关闭文档输出流
document.close()
// 向当前文档追加写入文本
document.write()
```

## 窗口控制

```js
// 按照给定像素移动指定窗口
window.moveBy(X,Y) // 移动指定的位置
// 将窗口移动到指定的位置
window.moveTo(X,Y)
// 调整当前窗口的大小
window.resizeBy(X,Y) // 大于0 时扩大，小于 0 时缩小
// 改变当前窗口的大小
window.resizeTo(X,Y) // 改变成为指定的长宽
// 水平位移量，垂直位移量
window.scrollBy(X,Y) // 参照当前位置进行移动
// 窗口内容滚动到指定的位置
window.scrollTo(X,Y)
```

## 焦点控制

```js
// 得到焦点
window.focus
// 失去焦点
window.blur
```

## 打开窗口

```js
window.open(URL,'WindowName','WindowStyle')
// 窗口风格
// height:number>100 窗口高度
// width:number>100 窗口宽度
// left:number>=0 窗口左坐标
// top:number>=0 窗口上坐标
// location:boolean 是否显示地址栏
// menubar:boolean 是否显示菜单栏
// resizable:boolean 是否可以改变窗口的大小
// scrollbars:boolean  是否允许出现滚动条
// status:boolean 是否显示状态栏
// toolbar:boolean 显示工具栏
window.close() // 关闭浏览器窗口
```

## 定时器

```js
// 定时器
setTimeout
clearTimeout
setInterval
clearInterval
```

## 对话框

```js
// 提示
window.alert('提示内容')
// 确认
window.confirm('提示内容') // 会返回 true or false
// 内容
window.prompt('提示字符串','默认内容') // 返回内容，或者是 null
```

## 其他属性

**状态栏**

```js
// 状态栏的默认显示
window.defaultStatus
// 临时改变浏览状态的显示
window.status
```















