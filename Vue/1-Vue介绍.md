> Create by fall on:2022-03-13
> Recently revised in:2022-06-11

# Vue

渐进式 `javascript` 框架。

> 声明式渲染-->组建系统-->客户端路由-->集中式状态管理->项目构建
>
> 集中式状态管理：方便管理业务数据，`vue`中有一个单独模块`VueX`专门处理此类业务

## 特点

客户端路由：实现局部更新，历史回退功能

- 易用、熟悉后开发很快
- 灵活 在库和一套完整框架之间自由伸缩
- 高效：超快虚拟 DOM，20kb 运行大小

**数据的响应式**

- 响应式布局和数据响应式
  - h5中的响应式布局指的是页面尺寸随着屏幕大小进行改变
  - 数据响应式指数据的变化导致页面内容的变化
- 数据绑定
  - 将数据填充到标签中
- v-once 只编译一次
  - 显示内容之后不具有响应式的功能

数据监听：从view（视图）到 model（模型）

数据绑定：从model（模型）到 view（视图）

## 使用

实例参数

- el：元素的挂载位置（CSS选择器或者DOM元素）
- data：数据对象（值是一个对象）

插值表达式

- 将html填充到HTML标签之中
- 插值表达式支持基本的计算操作

编译过程

- `vue`语法->原生语法

```html
<div class="app"></div>
<script src="vue.js"></script> <!-- 此处引入 vue.js-->
<script>
var app = new Vue({
  el:'.app',
  data:{},
  methods:{}
})
</script>
```

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

实现组件缓存，组件切换时，不会对当前组件进行卸载。

使用场景是嵌套 `router-view`

```vue
<keep-alive>
  <router-view></router-view>
</keep-alive>
```

`keep-alive` 标签总共可以传递三个参数，`include`、`exclude` 分别表示，匹配成功的内容会不会被缓存，`max` 表示限制缓存的最大个数，默认为 10 个。  

被 `keep-alive` 包含的组件/路由中，会多出两个生命周期的钩子：`activated` 与 `deactivated`。`activated` 会在组件第一次渲染时调用，之后如果激活了，也会去调用。

`$route.meta.keepAlive` 可以用来判断当前路由是否被缓存，可以利用这点添加骨架屏，以保证用户的体验

## 模块的导入导出

导入以使用模块，导出模块，可以提供给其他模块使用

**导入模块**

导入常量，函数，文件，模块等，方便进行使用

`import Name from './path/file'`

**导出模块**

export 和 export default 都可以用于导出常量、函数、文件、模块等。

export 和 export default 的区别

使用 export 导出的内容都必须使用大括号进行引用

```js
// module.js
export const fake = '虚伪的人' 
// main.js
import {fake}
```



> 



## 指令

| 指令名称    | 指令功能                                 | 简写 |
| ----------- | ---------------------------------------- | ---- |
| **v-cloak** | 先通过隐藏样式在内存时的值，读取后显示   | 无   |
| **v-text**  | 填充纯文本，用该方法填充不会闪动         | 无   |
| **v-html**  | 作用：填充HTML片段                       | 无   |
| **v-pre**   | 填充原始信息，显示原始信息，跳过编译过程 | 无   |
| **v-on:**   | 添加事件(点击事件，移动时间)             | @    |
| **v-band:** | 绑定后面的属性值                         | :    |
| **v-if**    | 判断是否渲染                             | 无   |
| **v-show**  | 判断是否展示                             | 无   |
| **v-for**   | 遍历属性                                 | 无   |

##　样式绑定

1. class样式处理

- 传入数组

```vue
<div :class="['activeClass',errorClass]" >看看里面有什么</div>
// 可以在data中更改errorClass里面的值
```

-  传入对象

```vue
<div :class="{active:activeJudge,errorClass:true}" >看看里面有什么</div>
// 只可以设置真假
```

2. 绑定样式的细节

- 对象绑定和数组绑定可以同时使用
- 数组绑定和对象绑定可以结合使用
- 默认的CSS样式也会生效

```vue
// 简化操作
<div :class="activeClass">看看里面有什么</div>
new Vue({data:{
	  activeClass:["bg-active","font-active"]
}})
```

## 循环遍历的使用

**遍历数组**

```vue
<div v-show="got" v-for="item in list">{{item}}</div>
// 将对象传入数组，输出对应的对象的值
<div v-show="got" v-for="item in list">{{item.age +"-------"+item.name}}</div>
```

**遍历对象**(键值对)

```vue
// 可以同时输出对象的键和对象的值
// value:值    key:键    index: 索引
<div v-show="got" v-for="(value,key,index) in object">{{v+"-------"+k+"-------"+i}}</div>
```

> 算法的优化，务必在标签内部书写 `v-bind:key="item.id"`优化，系统进行数据查找时不会盲目，也可以简写为`:key="item.id"`

## 绑定表单控件

> 绑定表单事件

```html
<div class="resume">
    <div class="hobby">
        <span>个人爱好：</span>
        <input type="checkbox" id="wo" value="1" v-model="hobby">女人
        <input type="checkbox" id="woman" value="2" v-model="hobby">女人♀
        <input type="checkbox" id="girl" value="3" v-model="hobby"> girl
    </div>
</div>
<script>
var vm = new Vue({
      el:".resume",
      data:{
        hobby:[3,1],//里面存放无序数组，绑定对应id的数据
      },
    })
</script>
```

## 自定义指令

> 因为内置指令不足以满足全部需求，所以出现自定义指令

```js
<input type="text" v-focus>
Vue.directive("focus"{
	inserted:function(el){
    el.focus();
}
})
//第二个参数
<input type="text" v-focus>
Vue.directive("focus"{
	inserted:function(el,binding){
    console.log(binding)
    el.style.backgroundColor = binding.value;
}
})
```

## 计算属性

> 可以通过计算属性对于函数进行计算
>
> 由于有缓存机制，无论调用多少次，只会打印一次
>
> 牺牲内存，节省性能

```js
var vm = new Vue({
    computed:{
         reverse:function(){
             console.log()
             return this.msg.split("").reverse().join('')
         }
     }    
}) 
```

## 侦听器

- 采用侦听器监听用户名的变化
- 调用后台接口进行验证
- 根据验证的结果调整提示信息

```js
watch:{
  firstName:function(val){
    this.fullName = val+" "+ this.lastName;
  }
}
```

