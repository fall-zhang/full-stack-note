

### 跨域是什么，你是怎么解决跨域问题的

### 如何实现对象的深拷贝

> Create by **fall** on 2021-10-18
> Recently revised in 2021-10-18 13:52:00

## 简单

### undefined 和 null 的区别是什么？

- undefined 是此处应该有一个值，但是没定义。
- null 是不应该有值

```js
var a;
i // undefined
function b(x){console.log(x)}
b() // undefined
var  c = new Object();
c.p // undefined
var d = f();
d // undefined
```

判断一个值是否存在的话，使用的是 a === undefined 而不是，a==null，后者只能判断是否为 null

### 什么是事件代理（事件委托） 有什么好处

事件委托的原理：不给每个子节点单独设置事件监听器，而是设置在其父节点上，然后利用冒泡原理设置每个子节点，即`event.target`。

**优点：**

- **减少内存消耗和对 DOM 操作，提高性能**。因为需要不断的操作 DOM，持续操作 DOM 会引起浏览器重绘和回流的可能也就越多，页面交互的事件也就变的越长。在 JavaScript 中，添加到页面上的事件处理程序数量将直接关系到页面的整体运行性能。每一个事件处理函数，都是一个对象，多一个事件处理函数，**内存**中就会被多占用一部分空间。如果要用事件委托，就会将所有的操作放到 js 程序里面，只对它的父级进行操作，与 DOM 的操作就只需要交互一次，这样就能大大的减少与 DOM 的交互次数，提高性能。
- 动态绑定事件 因为事件绑定在父级元素 所以新增的元素也能触发同样的事件

### addEventListener 默认是捕获还是冒泡

默认是**冒泡**

addEventListener**第三个参数**默认为 false 代表执行事件冒泡行为。

当为 true 时执行事件捕获行为。

### apply call bind 区别

- 三者都可以改变函数的 this 对象指向。
- 三者第一个参数都是 this 要指向的对象，如果如果没有这个参数或参数为 undefined 或 null，则默认指向全局 window。
- 三者都可以传参，但是 **apply 是数组**，而 **call 是参数列表**，且 apply 和 call 是一次性传入参数，而 **bind 可以分为多次传入**。
- bind 是返回**绑定 this 之后的函数**，便于稍后调用；apply 、call 则是**立即执行** 。
- bind()会返回一个新的函数，如果这个返回的新的函数作为**构造函数**创建一个新的对象，那么此时 this **不再指向**传入给 bind 的第一个参数，而是指向用 new 创建的实例

```js
function add(a,b){
  console.log(this) // '10+20'
  console.log(a) // 10
  console.log(b) // 33
  return a+b
}
const reAdd = add.bind('10+20',10).bind(22,33)
const result = reAdd()
result // 43
```

> 注意！很多同学可能会忽略 bind 绑定的函数作为构造函数进行 new 实例化的情况
>
> 如果这个返回的新的函数作为构造函数创建一个新的对象，那么此时 this 不再指向传入给 bind 的第一个参数，而是指向用 new 创建的实例

### 闭包的应用场景

比如常见的防抖节流

```js
// 防抖
function debounce(fn, delay = 300) {
  let timer; //闭包引用的外界变量
  return function () {
    const args = arguments;
    if (timer) {
      clearTimeout(timer);
    }
    timer = setTimeout(() => {
      fn.apply(this, args);
    }, delay);
  };
}
```

使用闭包可以在 JavaScript 中模拟块级作用域

```js
function outputNumbers(count) {
  (function () {
    for (var i = 0; i < count; i++) {
      alert(i);
    }
  })();
  alert(i); //导致一个错误！
}
```

闭包可以用于在对象中创建私有变量

```js
var aaa = (function () {
  var a = 1;
  function bbb() {
    a++;
    console.log(a);
  }
  function ccc() {
    a++;
    console.log(a);
  }
  return {
    b: bbb, //json结构
    c: ccc,
  };
})();
console.log(aaa.a); //undefined
aaa.b(); //2
aaa.c(); //3
```

### 事件循环

```js
setTimeout(function () {
  console.log("1");
}, 0);
async function async1() {
  console.log("2");
  const data = await async2();
  console.log("3");
  return data;
}
async function async2() {
  return new Promise((resolve) => {
    console.log("4");
    resolve("async2的结果");
  }).then((data) => {
    console.log("5");
    return data;
  });
}
async1().then((data) => {
  console.log("6");
  console.log(data);
});
new Promise(function (resolve) {
  console.log("7");
  //   resolve()
}).then(function () {
  console.log("8");
})
```

输出结果：2475361

> 注意！我在最后一个 **Promise** 埋了个坑 我没有调用 resolve 方法 这个是在面试美团的时候遇到了 当时自己没看清楚 以为都是一样的套路 最后面试官说不对 找了半天才发现是这个坑 哈哈