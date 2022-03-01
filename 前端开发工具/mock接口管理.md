> Create by **fall** on 2022-03-01
> Recently revised in 2022-03-01

## Mock

### mock数据方案

- 直接写代码内
- 接口管理工具（后端写接口文档，做假数据，后端控制该流程）
  - rap、swagger、[YAPI](https://hellosean1025.github.io/yapi/documents/)、[moco](https://link.juejin.cn?target=https%3A%2F%2Fgithub.com%2Fdreamhead%2Fmoco) 
- 本地 node 服务器（可以独立使用，创建一个本地小型数据库）
  - `json-server` 
- 请求拦截（拦截特定请求，生成给定的随机数据，以此模拟数据）
  - mock.js 
- 抓包工具（将 URL 映射到本地文件）
  - `charles` 、`Fiddler` 等代理工具
- 组合模式（就是组合）
  - easy-moke、

## 配置

会自动配置时间

```js
Mock.setup({
    timeout: 400
})
```





## 随机数生成数据

生成示例的文档：http://mockjs.com/examples.html

基本数据

```js
Mock.mock('@color') 
"#f279ba"
Mock.mock('@email')
"k.fxnx@newvwi.gf"
Mock.mock('@ip')
"44.122.28.106"
Mock.mock('@region')
"东北"
// 随机生成日期
Random.date()
// => "2020-10-23"
Random.date('yyyy-MM-dd')
// => "1998-01-29"
Random.time()
// => "22:44:56"
Mock.mock('@time')
// => "01:48:17"
```

中文文本

```js
// 随机生成姓名
Random.cname()
// 生成随机文本
Random.paragraph()
```

其他类型文件

```js
// 随机生成图片
// Random.image( size, background, foreground, format, text )
Random.image('200x100', '#894FC4', '#FFF', 'png', Random.cname())
Random.image()
```

> 生成图片是通过 https://dummyimage.com/ 网站进行生成的

## 参考文章

| 作者/文章名称 | 链接                                       |
| ------------- | ------------------------------------------ |
| tager         | https://juejin.cn/post/7026165301255340045 |
| mock.js       | http://mockjs.com/                         |

