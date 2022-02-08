>Create by **fall** on 2021年10月26日19:15:51
>Recently revised in 2021年10月31日18:09:39

## 文件结构

```vue
<template>
  // Vue2中，template标签中只能有一个根元素，在Vue3中没有此限制
</template>
<script setup>
  // ...
</script>
<style lang="scss" scoped>
  // 支持CSS变量注入v-bind(color)
</style>
```

## data声明

```vue
<script setup>
	// 在 script setup里面声明的所有数据都是可以在 template 中使用的
  import { reactive, ref } from 'vue'
  // ref声明响应式数据，用于声明基本数据类型
  const name = ref('Jerry')
  // 修改
  name.value = 'Tom'

  // reactive声明响应式数据，用于声明引用数据类型
  const state = reactive({
    name: 'Jerry',
    sex: '男'
  })
  // 修改
  state.name = 'Tom'
</script>
```

## method

```vue
<template>
  // 调用方法
  <button @click='changeName'>按钮</button>  
</template>

<script setup>
  import { reactive } from 'vue'

  const state = reactive({
    name: 'Jery'
  })

  // 声明method方法
  const changeName = () => {
    state.name = 'Tom'
  }  
</script>
```

## computed

```javascript
<script setup>
  import { computed, ref } from 'vue'
  const count = ref(1)
  // 通过computed获得doubleCount
  const doubleCount = computed(() => {
    return count.value * 2
  })
</script>
```

## watch

```javascript
<script setup>
  import { watch, reactive } from 'vue'
  const state = reactive({
    count: 1
  })
  // 声明方法
  const changeCount = () => {
    state.count = state.count * 2
  }
  // 监听count
  watch(
    () => state.count,
    (newVal, oldVal) => {
      console.log(state.count)
      console.log(`watch监听变化前的数据：${oldVal}`)
      console.log(`watch监听变化后的数据：${newVal}`)
    },{
      immediate: true, // 立即执行
      deep: true // 深度监听
    }
  )
</script>
```

侦听ref中的数据

```js
// 省略引入
const num = ref()
setTimeout(()=>{num.value++},1000)
watch(num,(newVal,oldVal)=>{
  console.log(newVal+"<新的值|旧的值>"+oldVal)
})
```

侦听多个数据

```js
// 省略引入
watch([()=>data1,()=>data2],()=>{
  
})
```

## watchEffect

在组件初始化时， 会先执行一次来收集依赖， 然后当收集到的依赖中数据发生变化时， 就会再次执行回调函数。

意思是，只要读取了任何响应式数据，都会触发 Proxy 的 getter 代理机制，从而调用 `watchEffect` 方法内的事件，执行一次，但是对 `watchEffect` 内进行更改时，不会触发

```vue
<script setup>
  import { watchEffect,ref, reactive } from 'vue'
  const age = ref(999)
  const state = reactive({
    count: 1,
    name:'liu'
  })
  // 声明方法
  setTimeout(()=>{
    state.count++
  },1000)
  setTimeout(()=>{
    age.value++
  },5000)
  // 监听count
 watchEffect(()=>{
   console.log(state)
   console.log(age)
 })
</script>
```

## props父传子

### 子组件

```vue
<template>
  <span>{{props.name}}</span>
  // 可省略【props.】
  <span>{{name}}</span>
</template>

<script setup>
  // import { defineProps } from 'vue'
  // defineProps在<script setup>中自动可用，无需导入
  // 需在.eslintrc.js文件中【globals】下配置【defineProps: true】
  // 声明 props
  const props = defineProps({
    name: {
      type: String,
      default: ''
    }
  })  
</script>
```

### 父组件

```javascript
<template>
  <child name='Jerry'/>  
</template>

<script setup>
  // 引入子组件
  import child from './child.vue'
</script>
```

## emit子传父

### 子组件

```vue
<template>
  <span>{{props.name}}</span>
  // 可省略【props.】
  <span>{{name}}</span>
  <button @click='changeName'>更名</button>
</template>
<script setup>
  // import { defineEmits, defineProps } from 'vue'
  // defineEmits和defineProps在<script setup>中自动可用，无需导入
  // 需在.eslintrc.js文件中【globals】下配置【defineEmits: true】、【defineProps: true】
  // 声明props
  const props = defineProps({
    name: {
      type: String,
      default: ''
    }
  }) 
  // 声明事件
  const emit = defineEmits(['updateName'])
  
  const changeName = () => {
    // 执行
    emit('updateName', 'Tom')
  }
</script>

```

### 父组件

```vue
<template>
  <child :name='state.name' @updateName='updateName'/>  
</template>
<script setup>
  import { reactive } from 'vue'
  import child from './child.vue'
  const state = reactive({
    name: 'Jerry'
  })
  
  // 接收子组件触发的方法
  const updateName = (name) => {
    state.name = name
  }
</script>
```

## v-model

v-model 可以绑定多个值，并且如果不写 `v-model:` 中 `:` 后面的值，默认绑定的为 `modelValue`

### 子组件

```vue
<template>
  <span @click="changeInfo">我叫{{ modelValue }}，今年{{ age }}岁</span>
</template>
<script setup>
  // import { defineEmits, defineProps } from 'vue'
  // defineEmits和defineProps在<script setup>中自动可用，无需导入
  // 需在.eslintrc.js文件中【globals】下配置【defineEmits: true】、【defineProps: true】
  defineProps({
    modelValue: String,
    age: Number
  })
  const emit = defineEmits(['update:modelValue', 'update:age'])
  const changeInfo = () => {
    // 触发父组件值更新
    emit('update:modelValue', 'Tom')
    emit('update:age', 30)
  }
</script>
```

### 父组件

```vue
<template>
  // v-model:modelValue简写为v-model
  // 可绑定多个v-model
  <child
    v-model="state.name"
    v-model:age="state.age"
  />
</template>

<script setup>
  import { reactive } from 'vue'
  // 引入子组件
  import child from './child.vue'

  const state = reactive({
    name: 'Jerry',
    age: 20
  })
</script>
```

## nextTick

A utility for waiting for the next DOM update flush.

等待下一个 DOM 更新完成的工具

```js
// type
function nextTick(callback?:()=>void):Promise<void>
```



```vue
<script setup>
  import { nextTick } from 'vue'
  nextTick(() => {
    // ...
  })
</script>
```

## ref和defineExpose

将方法、变量暴露给父组件使用，父组件才可通过 ref API拿到子组件暴露的数据

- 在标准组件写法里，子组件的数据都是默认隐式暴露给父组件的，但在 script-setup 模式下，所有数据只是默认 return 给 template 使用，不会暴露到组件外，所以父组件是无法直接通过挂载 ref 变量获取子组件的数据。
- 如果要调用子组件的数据，需要先在子组件显示的暴露出来，才能够正确的拿到，这个操作，就是由 defineExpose 来完成。

### 子组件

```vue
<template>
  <span>{{state.name}}</span>
</template>
<script setup>
  import { defineExpose, reactive, toRefs } from 'vue'
  // 声明state
  const state = reactive({
    name: 'Jerry'
  }) 
  // 声明方法
  const changeName = () => {
    // 执行
    state.name = 'Tom'
  }
  // 将方法、变量暴露给父组件使用，父组件才可通过 ref API拿到子组件暴露的数据
  defineExpose({
    // 解构state
    ...toRefs(state),
    changeName
  })
</script>
```

### 父组件

```vue
<template>
  <child ref='childRef'/>  
</template>

<script setup>
  import { ref, nextTick } from 'vue'
  // 引入子组件
  import child from './child.vue'
  // 子组件ref
  const childRef = ref('childRef')
  // nextTick
  nextTick(() => {
    // 获取子组件 name
    console.log(childRef.value.name)
    // 执行子组件方法
    childRef.value.changeName()
  })
</script>
```

## 十一、路由useRoute和useRouter

```vue
<script setup>
  import { useRoute, useRouter } from 'vue-router'
	
  // 必须先声明调用
  const route = useRoute()
  const router = useRouter()
	
  // 路由信息
  console.log(route.query)

  // 路由跳转
  router.push('/newPage')
</script>
```

## 十二、路由导航守卫

```javascript
<script setup>
  import { onBeforeRouteLeave, onBeforeRouteUpdate } from 'vue-router'
	
  // 添加一个导航守卫，在当前组件将要离开时触发。
  onBeforeRouteLeave((to, from, next) => {
    next()
  })

  // 添加一个导航守卫，在当前组件更新时触发。
  // 在当前路由改变，但是该组件被复用时调用。
  onBeforeRouteUpdate((to, from, next) => {
    next()
  })
</script>
复制代码
```

## 十三、store

*Vue3 中的Vuex不再提供辅助函数写法

```vue
<script setup>
  import { useStore } from 'vuex'
  import { key } from '../store/index'
  // 必须先声明调用
  const store = useStore(key)
  // 获取Vuex的state
  store.state.xxx
  // 触发mutations的方法
  store.commit('fnName')
  // 触发actions的方法
  store.dispatch('fnName')
  // 获取Getters
  store.getters.xxx
</script>
```

## 十四、生命周期

通过在生命周期钩子前面加上 “on” 来访问组件的生命周期钩子。

下表包含如何在 Option API 和 setup() 内部调用生命周期钩子

| **Option API**  | **setup中**       |
| --------------- | ----------------- |
| beforeCreate    | 不需要            |
| created         | 不需要            |
| beforeMount     | onBeforeMount     |
| mounted         | onMounted         |
| beforeUpdate    | onBeforeUpdate    |
| updated         | onUpdated         |
| beforeUnmount   | onBeforeUnmount   |
| unmounted       | onUnmounted       |
| errorCaptured   | onErrorCaptured   |
| renderTracked   | onRenderTracked   |
| renderTriggered | onRenderTriggered |
| activated       | onActivated       |
| deactivated     | onDeactivated     |

## 十五、CSS变量注入

```javascript
<template>
  <span>Jerry</span>  
</template>

<script setup>
  import { reactive } from 'vue'

  const state = reactive({
    color: 'red'
  })
</script>
  
<style scoped>
  span {
    // 使用v-bind绑定state中的变量
    color: v-bind('state.red');
  }  
</style>
复制代码
```

## 十六、原型绑定与组件内使用

### main.js

```javascript
import { createApp } from 'vue'
import App from './App.vue'
const app = createApp(App)

// 获取原型
const prototype = app.config.globalProperties

// 绑定参数
prototype.name = 'Jerry'
复制代码
```

### 组件内使用

```javascript
<script setup>
  import { getCurrentInstance } from 'vue'

  // 获取原型
  const { proxy } = getCurrentInstance()
  
  // 输出
  console.log(proxy.name)
</script>
复制代码
```

## 十七、对 await 的支持

不必再配合 async 就可以直接使用 await 了，这种情况下，组件的 setup 会自动变成 async setup 。

```javascript
<script setup>
  const post = await fetch('/api').then(() => {})
</script>
复制代码
```

## 十八、定义组件的name

用单独的`<script>`块来定义

```javascript
<script>
  export default {
    name: 'ComponentName',
  }
</script>
复制代码
```

## 十九、provide和inject

### 父组件

```javascript
<template>
  <child/>
</template>

<script setup>
  import { provide } from 'vue'
  import { ref, watch } from 'vue'
  // 引入子组件
  import child from './child.vue'

  let name = ref('Jerry')
  // 声明provide
  provide('provideState', {
    name,
    changeName: () => {
      name.value = 'Tom'
    }
  })

  // 监听name改变
  watch(name, () => {
    console.log(`name变成了${name}`)
    setTimeout(() => {
      console.log(name.value) // Tom
    }, 1000)
  })
</script>
复制代码
```

### 子组件

```javascript
<script setup>
  import { inject } from 'vue'
	// 注入
  const provideState = inject('provideState')
  
  // 子组件触发name改变
  provideState.changeName()
</script>
复制代码
```

## 使用echarts

```javascript
// 安装
cnpm i echarts --save

// 组件内引入
import * as echarts from 'echarts'
```



## 参考文章

| 作者      | 链接                                       |
| --------- | ------------------------------------------ |
| Jerry丶Hu | https://juejin.cn/post/7006108454028836895 |
| SandySY   | https://juejin.cn/post/6940454764421316644 |
|           |                                            |
|           |                                            |
|           |                                            |

 

