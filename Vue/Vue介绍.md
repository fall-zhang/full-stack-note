> Create by fall on:2022-03-13
> Recently revised in:2022-03-13

## 生命周期

挂载时：

父组件（`beforeCreate`）->父（`created`）->父（`beforeMount`）->子组件（`beforeCreate`）->子（`created`）->子（`beforeMount`）->子（`mounted`）->父（`mounted`）

子组件更新

父组件（`beforeUpdate`）->子组件（`buforeUpdate`）->子组件（`updated`）->父组件（`updated`）

父组件更新

父组件（`beforeUpdate`）->父组件（`updated`）

销毁

父 （`beforeDestroy`）->子 （`beforeDestroy`）->子 （`destroyed`）->父 （`destroyed`）

## keep-alive

实现组件缓存，组件切换时，不会对当前组件进行卸载

#### Vue.extend

const app = createApp(App)

app.use()

## 自定义指令

## diff算法

根节点是否相同：