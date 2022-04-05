```tsx
import cn from "classnames"
import React from 'react'
import "./style/index.less"
import {Icon,IIconProps} from "zent" // 理解为自定义的模块即可，zent 是啥不重要
interface IProps {
  title:string
  iconType?:IIconProps["type"]
  isShowIcon?:boolean
  iconClassName?:string
  titileClassName?:string
}
export const ContentTitle:React.FC<IProps>=(props)=>{
  const {title,iconType= 'liuchuan',isShowIcon=false,iconClassName,titleClassName,...popProps}= props
  return(
  <div className={cn("content-title",titleClassName)}>
    {title}
    {isShowIcon && <Icon className={cn("content-title__icon",iconClassName)} {...popProps} type={iconType} />}
    </div>
  )
}
```

