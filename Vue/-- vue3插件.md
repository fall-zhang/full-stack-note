## vue-class-component

`vue-class-component` 官方出品，提供了Vue 、Component 等

## vue-property-decorator

`vue-property-decorator` 是社区出品，依赖 `vue-class-component` ，拓展出更多操作符。

### 基本使用

在开发时进行引入就行

```html
<script lang="ts">
  import {Vue, Component} from 'vue-property-decorator';
  @Component({})
  export default class "组件名" extends Vue{
    ValA: string = "hello world";
    ValB: number = 1;
  }
</script>
```

该文件等同于下面的文件

```html
<script lang="es6">
    import Vue from 'vue';
    export default {
        data(){
            return {
                ValA: 'hello world',
                ValB: 1
            }
        }
    }
</script>
```

总结：对于变量的定义，只需要按照 `ts` 中变量的命名方法即可

如果有 `computed` ，可以使用 getter 进行代替

原本`Vue`中的`computed`里的每个计算属性都变成了在前缀添加`get`的函数.

```html
<script lang="ts">
    import {Vue, Component} from 'vue-property-decorator';
    @Component({})
    export default class "组件名" extends Vue{
        get ValA(){
            return 1;
        }
    }
</script>
```

```html
<script lang="es6">
    import Vue from 'vue';
    export default {
        computed: {
            ValA() {
                return 1;
            }
        }
    }
</script>
```

### @Emit

在 `vue` 中，事件的监听和触发原本是通过 `$emit`、`$on` 在 `vue-property-decorator` 中，需要使用 `@Emit` 属性。

```html
<script lang="ts">
  import {Vue, Component, Emit} from 'vue-property-decorator';
  @Component({})
  export default class "组件名" extends Vue{
    mounted(){
      // $on 的作用是，绑定时间名称，和方法
      this.$on('emit-todo', function(n) {
        console.log(n)
      })
      this.emitTodo('world');
    }
    @Emit()
    emitTodo(n: string){
      console.log('hello'); // 先执行此处的内容，然后，再回调执行 emit-todo
    }
  }
</script>
```

触发 `@Emit` 后，会先执行在 `emit-todo` 后，执行 `emit-todo`

```html
<script lang="es6">
  import Vue from 'vue';
  export default {
    mounted(){
      this.$on('emit-todo', function(n) {
        console.log(n)
      })
      this.emitTodo('world');
    },
    methods: {
      emitTodo(n){
        console.log('hello');
        this.$emit('emit-todo', n);
      }
    }
  }
</script>
```

总结：在 `Vue` 中我们是使用 `$emit` 触发事件,使用 `vue-property-decorator` 时,可以借助 `@Emit` 装饰器来实现。`@Emit`修饰的函数所接受的参数会在运行之后触发事件的时候传递过去。
 `@Emit`触发事件有两种写法

- `@Emit() `不传参数,那么它触发的事件名就是它所修饰的函数名。

- `@Emit(name: string)`，里面传递一个字符串,该字符串为要触发的事件名.

### @Watch

一看就知道是用做监听的，

```js
// vue2 的书写格式
export default{
  watch: {
    'child': this.onChangeValue, // 监听的数据:执行的方法
    // 这种写法默认 `immediate`和`deep`为`false`
    'person': {
      handler: 'onChangeValue',
      immediate: true,
      deep: true
    }
  },
  methods: {
    onChangeValue(newVal, oldVal){ // 监听事件，自带传入两个值，第一个是更改之后的新字符串，另一个自己想
      // todo sth...
    }
  }
}
```

```js
// vue3 的书写格式
import {Vue, Component, Watch} from 'vue-property-decorator';
@Watch('child')
onChangeValue(newVal: string, oldVal: string){
    // todo...
}
@Watch('person', {immediate: true, deep: true})
onChangeValue(newVal: Person, oldVal: Person){
    // todo...
}
```

### @prop

学过vue2的都知道是用来向子传值的

```js
// 比如说子组件接收父组件的值
export default {
  props: {
    propA: {
      type: Number
    },
    propB: {
      default: 'default value'
    },
    propC: {
      type: [String, Boolean]
    },
  }
}
// vue3 中，变更后是这个样子的
import {Vue, Component, Prop} from 'vue-property-decorator';
@Component({})
export default class "组件名" extends Vue{
  @Prop(Number) propA!: number;// !是 typescript 中的内容，表示可选值
  @Prop({default: 'default value'}) propB!: string;
  @propC([String, Boolean]) propC: string | boolean;
}
```

总结： `@Prop` 接受一个参数可以是类型变量或者对象或者数组。`@Prop` 接受的类型比如 `Number` 是 `JavaScript` 的类型,之后定义的属性类型则是 `TypeScript` 的类型。

### Mixins

真正开发过程中，经常用到混合

#### 第一种混合方法

这个混合方法由 `vue-class-component`

首先，需要定义一个要混合的类

```typescript
// 创建mixins.ts 用来定义要混合的类
import Vue from 'vue';
import  Component  from 'vue-class-component';
@Component  // 一定要用 Component 修饰
export default class myMixins extends Vue {
    value: string = "Hello"
}
// 然后引入这个类
import  Component  {mixins}  from 'vue-class-component';
import myMixins from 'mixins.ts';
@Component			// 直接extends myMinxins 也可以正常运行
export class myComponent extends mixins(myMixins) {
      created(){
          console.log(this.value) // => Hello
    }
}
```

#### 第二种混合方法

```js
// mixins.ts
import { Vue, Component } from 'vue-property-decorator';
declare module 'vue/types/vue' {
    interface Vue {
        value: string;
    }
}
@Component
export default class myMixins extends Vue {
    value: string = 'Hello'
}
```

```js
import { Vue, Component, Prop } from 'vue-property-decorator';
import myMixins from '@static/js/mixins';
@Component({
    mixins: [myMixins]
})
export default class myComponent extends Vue{
    created(){
        console.log(this.value) // => Hello
    }
}
```

总结：两种方式不同的是在定义 `mixins` 时如果没有定义 `vue/type/vue` 模块, 那么在混入的时候就要 `继承` 该 `mixins`； 如果定义 `vue/type/vue` 模块,在混入时可以在 `@Component` 中 `mixins` 直接混入。

### @Model

`Vue`组件提供`model`: `{prop?: string, event?: string}`让我们可以定制`prop`和`event`.
 默认情况下，一个组件上的`v-model` 会把 `value`用作 `prop`且把 `input`用作 `event`，但是一些输入类型比如单选框和复选框按钮可能想使用 `value prop`来达到不同的目的。使用`model`选项可以回避这些情况产生的冲突。

- 下面是`Vue`官网的例子

```xml
<my-checkbox v-model="foo" value="some value"></my-checkbox>
```

```js
Vue.component('my-checkbox', {
  model: {
    prop: 'checked',
    event: 'change'
  },
  props: {
    // this allows using the `value` prop for a different purpose
    value: String,
    // use `checked` as the prop which take the place of `value`
    checked: {
      type: Number,
      default: 0
    }
  },
  // ...
})
```

相当于

```csharp
<my-checkbox
  :checked="foo"
  @change="val => { foo = val }"
  value="some value">
</my-checkbox>
```

即`foo`双向绑定的是组件的`checke`, 触发双向绑定数值的事件是`change`

使用`vue-property-decorator`提供的`@Model`改造上面的例子.

```js
import { Vue, Component, Model} from 'vue-property-decorator';

@Component
export class myCheck extends Vue{
   @Model ('change', {type: Boolean})  checked!: boolean;
}
```

- 总结, `@Model()`接收两个参数, 第一个是`event`值, 第二个是`prop`的类型说明, 与`@Prop`类似, 这里的类型要用`JS`的. 后面在接着是`prop`和在`TS`下的类型说明.

### 官方文档

- [`@Prop`](https://github.com/kaorun343/vue-property-decorator#Prop)
- [`@PropSync`](https://github.com/kaorun343/vue-property-decorator#PropSync)
- [`@Model`](https://github.com/kaorun343/vue-property-decorator#Model)
- [`@ModelSync`](https://github.com/kaorun343/vue-property-decorator#ModelSync)
- [`@Watch`](https://github.com/kaorun343/vue-property-decorator#Watch)
- [`@Provide`](https://github.com/kaorun343/vue-property-decorator#Provide)
- [`@Inject`](https://github.com/kaorun343/vue-property-decorator#Provide)
- [`@ProvideReactive`](https://github.com/kaorun343/vue-property-decorator#ProvideReactive)
- [`@InjectReactive`](https://github.com/kaorun343/vue-property-decorator#ProvideReactive)
- [`@Emit`](https://github.com/kaorun343/vue-property-decorator#Emit)
- [`@Ref`](https://github.com/kaorun343/vue-property-decorator#Ref)
- [`@VModel`](https://github.com/kaorun343/vue-property-decorator#VModel)
- `@Component` (**provided by** [vue-class-component](https://github.com/vuejs/vue-class-component))
- `Mixins` (the helper function named `mixins` **provided by** [vue-class-component](https://github.com/vuejs/vue-class-component))