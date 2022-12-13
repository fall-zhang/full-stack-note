## 代码隔离

在文件名称的扩展名之前添加 `module.` 即可改变代码作用域，比如说在 less 中，通过`module.less` 实现代码隔离。

> 使用 `React.lazy()` 包裹的内容中，如果引入了 `module.less` 等内容，则会自动打包生成文件。

## CSS

### classnames

引入之后，可以实现解析为之后的类名

```tsx
import classnames from "classnames"
const bottomCardSty=classNames({
  [styles.ownBHeight]: true,
  [styles.isBChecked]: checked,
  [styles.noBChecked]: !checked,
  [styles.noBCheckedMq]:!checked&&dataSet.dsCodeType==3,
})

```

```jsx
import classnames from 'classnames'
import style from './style.css'
const oneDOM = <div className={style.class1, style.class2}></div>
```

### css-module

create-react-app 中会内置该方法

`className` 中传入的是对象，所以是双括号

```jsx
function MyComponent(){
  return(
    <div className={{marginTop:8}}></div>
  )
}
```

css 隔离

- css-module 类似于 vue 中的 scoped

```jsx
/* style.module.css */
.text{
  color:blue
}
/* app.tsx */
import style from './style.module.css'
function FallComponent(){
  return(
  	<div className={style.text}>隔离后的CSS</div>
  )
}
// 编译后
.text_fdu25RER{
  color:blue
}
```

### styled-components

```jsx
import syled from 'styled-components'
// 创建一个名称为 Title 的 div
const Title = styled.div`
	font-size:30px;
	background-color:cyan;
`
function App(){
  return(
  <Title>CSS in JS</Title>
  )
}
```

### 直接引入

```jsx
import 'index.module.less'
```

更改全局样式

```less
// 更改 ant-design 的全局样式
:global(.ant-result .ant-result-title) {
  color: white;
  .ant-result-subtitle {
    color: rgba(255, 255, 255, 0.45);
  }
}
```

## Tailwind

## 3d

经典回顾：**如何用 React Three Fiber 构建令人惊叹的 3D 场景** - 如果你想用 React 在浏览器中构建 3D 可视化，本文是一篇很好的入门介绍。(这是一年前的文章了，但是现在再看仍然很酷)。

**长按识别二维码查看原文**

https://varun.ca/modular-webgl/

## 参考文章

| 文章名称 | 文章链接                                   |
| -------- | ------------------------------------------ |
| 官方文档 | https://reactjs.org                        |
| ConardLi | https://juejin.cn/post/7085542534943883301 |

