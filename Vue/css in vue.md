>Create by fall on:2022-03-10
>Recently revised in:2022-03-10



### 实现 scoped 

给 HTML 的一个节点添加不重复的 data 属性，保证它的唯一 [data-v-2311c06a]

在 CSS 语句的末尾，也添加该 data 属性，保证该 CSS 只作用在该作用域内



```css
:deep(.class)  {} /*  vue 3 的写法 */
/deep/ .class {} /*  vue 2 的写法 */
/* 其它古老的写法，主要是 vue 不推荐了 */ 
.content >>> .button{}
.content ::v-deep .button{}
```

