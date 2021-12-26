> Create by **fall** on 2021-12-26
> Recently revised in 2021-12-26

使用Hooks 的原因

- 复用一个有效的组件太麻烦了
- 生命周期逻辑混乱
- `this` 的指向问题

useState

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



useEffect

> 将所有的副作用整合到一个函数中，如果出现了数据的转变，或者是生命周期的变化，就会执行该钩子，当然也支持定义多个 钩子

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

自定义 Effect Hooks

```jsx
import {useState,useEffect} from 'react'
function userStatusWatch(props){
  const [isOnline,setIsOnline] = useState(null)
	function handleStatusChange(status){
    setIsOnline(status.isOnline)
  }
  useEffect(()=>{
    ChatAPI.subscribeToFriendStatus(props,handleStatusChange)
  	return()=>{
      ChatAPI.subcribeToFriendStatus(props,handleStatusChange)
    }
  })
  return isOnline
}
function StatusWatch(props){
  const isOnline = useStatusWatch(props.friend.id)
  if(isOnline === null){
    return 'loading...'
  }
  return isOnline ? 'online' : 'offline'
}
```



































