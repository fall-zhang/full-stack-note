## 安装

```
npx create-react-app my-app --template typescript
```

React + TS 实现 Form

```ts
// service.ts
// 必要的 TS 声明，以及模拟后端接口
export enum Sex{
  female,
  male
}
export interface UserInfo{
  name:string
  sex:Sex
}
export const fetchUserInfo = (userId: string): Promise<UserInfo> =>
new Promise((rev) => {
  setTimeout(() => rev({ name: "Zhang san", sex: Sex.male }), 500);
});
export const updateUserInfo = (params:UserInfo):Promise<boolean> => Promise.resolve(true)
export const fetchUserList= ():Promise<UserInfo[]> => new Promise(resolve=>{
  setTimeout(()=>{
    resolve([
      {name:'就非得',sex:Sex.male},
      {name:'大幅',sex:Sex.female},
      {name:'不错',sex:Sex.female},
      {name:'切勿',sex:Sex.male},
    ])
  },220)
})
```



```tsx
// Form.tsx
import React,{useState,useEffect} from 'react'
import {Sex,fetchUserInfo,updateUserInfo} from '../services'

const Form =() => {
  const  [name,setName] = useState('')
  const [sex,setSex] = useState(Sex.male)
  useEffect(()=>{
    fetchUserInfo('id-xxx').then((res)=>{
      setName(res.name)
      setSex(res.sex)
    })
  },[])
  const handleSubmit = ()=>{
    const params = {name,sex}
    
  }
  return(
  	<div>
      <p>
      	<span>name</span>
        <input type="text" value={name} onChange={(e)=>{setName(e.target.value)}}></input>
      </p>
      <p>
      	<span>gender</span>
      	<input type='radio' checked={sex === Sex.male} onClick={()=>setSex(Sex.male)}/>Male
      	<input type='radio' checked={sex === Sex.female} onClick={()=>setSex(Sex.female)}/>Female
      </p>
      <p>
      	<button onClick={handleSubmit}>Submit</button>
      </p>
    </div>
  )
}
export default Form
```

