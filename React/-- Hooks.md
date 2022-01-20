> Create by **fall** on 2021-12-26
> Recently revised in 2022-01-20

使用 Hooks 的原因

- 复用一个有效的组件太麻烦了
- 生命周期逻辑混乱
- `this` 的指向问题

注意事项

- 只能在函数内部的最外层调用 Hook，不要在循环、条件判断或者子函数中调用
- 只能在 React 的函数组件中调用 Hook，不要在其他 JavaScript 函数中调用（例外：自定义 Hook）

三神柱：`useState` `useEffect` `useCallback`，这么一看，必须掌握的只有三个。还蛮简单的.jpg

## useState

 useState 总是替换变量而不是 class 组件中的 合并。

```jsx
import { useState } from 'react'
function MyComponent(){
  const [count,setCount]= useState(0)
  // useState 返回一个数组，第一项是设置的值，这里为 0
  // 第二个为 设置的函数，调用可以访问 setCount(count+1)
  return(
  	<div>
      <p>You already click {count} times</p>
      <button onClick={()=>setCount(count+1)}>Add</button>
    </div>
  )
}
```

特性

```jsx
import {useState} from 'react'
function Counter2(){
  let [number,setNumber] = useState(0);
  function alertNumber(){
    setTimeout(()=>{
      // 1 如果想设置 number 的值 
      // setNumber(number +1 ) // 这种方式设置值，只会使用点击时的值
      setNumber(number=>number+1) // 传递函数的方式，可以避免
      // alert 只能获取到点击按钮时的 number 值
      alert(number);
    },3000);
  }
  return (
    <>
    <p>{number}</p>
    <button onClick={()=>setNumber(number+1)}>+</button>
    <button onClick={()=>alertNumber()}>alertNumber</button>
    </>
  )
}
```

惰性初始化 state

```jsx
function Compp(props){
  console.log('render')
  function initState(){
    return {
      age:12,
      name:props
    }
  }
  const [file,setFile] = useState(initState)
  return(<>
    <h2>{file.age}</h2>
    <button onClick={()=>setFile({age:file.age+1,name:props})}>Plus</button>
    <button onClick={()=>setFile({age:file.age+1,name:props})}>Plus</button>
    </>)
}
```



## useEffect

数据获取、设置订阅以及手动更改 React 组件中的 DOM 都属于副作用。

> 将所有的副作用整合到一个函数中，如果出现了数据的转变，或者是生命周期的变化，就会执行该钩子，当然也支持定义多个钩子。

`useEffect` 会让 React 在完成对 DOM 的更改后，运行你的 useEffect 函数。由于副作用函数是在组件内声明的，所以可以访问到组件内部的 `props`、`state`。

React 会在每次渲染后调用副作用函数 —— 包括第一次渲染的时候。

```jsx
import {useState,useEffect} from 'react'
function Example(){
  cost [count,setCount]= useState(0)
  useEffect(()=>{
    // 更改当前文档的标题
    document.title = '别点了，都点' + count +'次了'
  },[count])// useEffect 第二个参数表明，只有 count 发生变化，才会执行
  return(
  <div>
    	<p>你点了 {count} 次了</p>
      <button onClick={()=>setCount(count+1)}>点啊</button>
    </div>)
}
```

> 有些代码无需进行清除，比如说网络请求和 DOM 绘制
>
> 有些代码需要进行清除，比如说监听 onMouseMove



## useCallback









## 自定义 Hooks

定义

```jsx
// useFriendStatus.js
import React,{useState,useEffect} from 'react'
function useFriendStatus(friendId){
  const [isOnline,setIsOnline] = useState(null)
  function handleStatusChange(status){
    setIsOnline(status.isOnline)
  }
  useEffect(()=>{
    ChatAPI.subscribeToFriendStatus(friendId,handleStatusChange)
    return()=>{
      ChatAPI.unsubscribeToFriendStatus(friendId,handleStatusChange)
    }
  })
  return isOnline
}
export default useFriendStatus
```

使用

```jsx
// FriendStatus.jsx
import React,{useState,useEffect} from 'react'
import useFriendStatus from 'useFriendStatus.js'
function FriendStatus(props){
  const isOnline = useFriendStatus(props.friend.id)
  if(isOnline === null){
    return 'loading...'
  }
  return isOnline ? 'online' : 'offline'
}
// FriendListItem.jsx
import React,{useState,useEffect} from 'react'
import useFriendStatus from 'useFriendStatus.js'
function FriendListItem(props){
  const isOnline = useFriendStatus(props.friend.id)
  if(isOnline === null){
    return 'loading...'
  }
  return (
  <div styl>
   	{props.friend.name}
  </div>
  )
}
```



### useMemo

一般情况下，只要父组件改变了，不管子组件是否依赖该状态，子组件也会重新渲染

- 类组件通过 `pureComponent`
- 函数组件通过 `React.memo`，将组件传递给 memo 之后，返回一个新的组件，如果接收到的属性不变，就不会重新渲染

### 

























```jsx
import React,{useState,useEffect} from 'react'
function Example(){
  const [count,setCount] = useState(0)
  useEffect(()=>{
    document.title = `you are ${count} years old`
  })
  return (
  <div>
  	<p>You clicked {count} times</p>
    <button onClick={()=>{setCount(count+1)}}>成长吧，少年</button>
  </div>
  )
}
```



