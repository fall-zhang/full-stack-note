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
// 泛型中包含了 PropsWithChildren 的泛型，所以不需要定义 children，如果要添加其他属性，需要添加类型注释
const MyComponent:React.FC<{message:string}> = ({message})=>{
  return (
    <div>{message}</div>
  )
}
```



