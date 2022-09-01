>Create by fall on:2022-03-10
>Recently revised in:2022-03-10



## scoped 

给 HTML 的一个节点添加不重复的 data 属性，保证它的唯一 [data-v-2311c06a]

在 CSS 语句的末尾，也添加该 data 属性，保证该 CSS 只作用在该作用域内



```css
:deep(.class)  {} /*  vue 3 的写法 */
/deep/ .class {} /*  vue 2 的写法 */
/* 其它古老的写法，主要是 vue 不推荐了 */ 
.content >>> .button{}
.content ::v-deep .button{}
```

## vue动画

Vue 的动画，说起来很简单，用 transform 套住 vue-router 就可以实现，不同的name绑定不同的动画。

一共有六个动画的类名，按照动画从开始到结束分别为：

- `v-enter`：表示进入时的位置。
- `v-enter-active`：表示进入，从位置移动后的动画
- `v-enter-to`：表示进入，并且进入的动画执行结束后。
- `v-leave`：离开开始时的状态
- `v-leave-active`：表示动画开始执行离开，到离开的过程
- `v-leave-to`：表示动画结束的位置

<img src="https://staging-cn.vuejs.org/assets/transition-classes.f0f7b3c9.png">

> 如果两个动画同时执行，比如说切换界面，既是一个页面的出现动画，也是另一个界面的消失动画。此时需要考虑如何实现不同动画的实现。

```vue
// 如果 name 中没有值，那么v就是所有动画的默认 name
// 如果加上了 name 就在原有的基础上添加 name 的值而已
<template>
	<transition name="page-change">
  	<router-view ></router-view>
  </transition>
</template>
<style>
  .page-change-enter-active {
    animation: change-page .5s;
  }
  .page-change-leave-active {
    animation: change-page .5s reverse;
  }
  @keyframes change-page-in {
    0% {
      transform: translate(100%,-100%);
    }
    100% {
      transform: translate(0,-100%);
    }
  }
</style>
```

