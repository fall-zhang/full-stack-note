>Create by **fall** on 2022-04-05
>Recently revised in 2022-04-05

## 安装

- 使用 `create-react-app` 添加模板

```bash
npx create-react-app my-app --template typescript
```

## 使用

`React.FC` 是 TypeScript 中的一个泛型，FC 是 Function Component 的缩写，也可以写为 `React.FunctionComponent`

```tsx
// 泛型中包含了 PropsWithChildren 的泛型，所以不需要定义 children，如果要添加其他属性，需要添加类型注释，比如这里的 message
const MyComponent:React.FC<{message:string}> = ({message})=>{
  return (
    <div>{message}</div>
  )
}
```

### Hooks

useState

```tsx
import {useState} from 'react'
const [val,setVal] = useState(22)
// 没有初始值，或者是 null
type AppProps = {message:string}
const App = ()=>{
  const [data] = useState<AppProps |null>(null)
  return <div>{data?.message}</div>
}
```

useEffect

```tsx
import {useEffect} from 'react'
function DealyedEffect(props:{timerMs:number}){
  const {timerMs} = props
  useEffect(()=>{
    const timer = setTimeout(()=>{
      console.log('yep')
    },timerMs)
    return ()=>clearTimeout(timer)
  },[timerMs])
  return null
}
useEffect(()=>{
  (async ()=>{
    const {data} = await ajax(params)
  })()
},[params])
useEffect(()=>{
  ajax(params).then(res=>{
    // todo
  })
})
```

useRef

```tsx
function TextInputWithFocusButton(){
  const inputEl = React.useRef<HTMLInputElement>(null)
  const onButtonClick = ()=>{
    if(inputEl && inputEl.current){
      input.current.focus()
    }
    inputEl.current?.focus()
  }
  return (
    <div>
      <input ref={inputEl} type='text' />
      <button onClick={onButtonClick}>Focus on Input</button>
    </div>
  )
}
```

useReducer









## Hello World

```tsx
// src/components/Hello.tsx
import * as React from 'react'
export interface Props{
  name:string
  enthusiasmLevel?:number
}
function Hello({name,enthusiasmLevel=1}:Props){
  if(enthusiasmLevel <=0){
    throw new Error('you should have a talk with your friends')
  }
  return (
  <div className="hello">
    <div className="greeting">
      Hello{name+getExclamationMarks(enthusiasmLevel)}
      </div>
    </div>
  )
}
function getExclamationMarks(numChars:number){
  return Array(numChars + 1).join('!')
}
```

响应消





