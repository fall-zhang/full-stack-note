## Boolean

由布尔对象存放的值或者要转换成布尔值的值

**返回值** 当作为一个构造函数 ( 带有运算符 new ) 调用时，Boolean() 将把它的参数转换成一个布尔值，并且返回一个包含该值的Boolean对象。如果作为一个函数(不带有运算符new)调用的，Boolean()只将它的参数转换成一个原始的布尔值，并且返回这个值。

false以及0、NaN、null、空字符串""和undefined都将转换成false。

字符串"false"以及其他的对象和数组都会被转换成true。

## Number类型数据

极大极小的值，可以用 e 来表示。

如果计算的数值超过JavaScript计算的数值范围，会被自动转换为infinity 值（有正负之分），infinity值不能参与下一次计算。

确定一个数是不是有穷的，可以使用 `isFinite()` 函数。

### NaN

用来表示一个本来要返回数值的操作数未返回数值的情况 避免抛出错误。

特点：

- 任何涉及NaN操作(NaN/10)都会返回NaN
- NaN 和任何值都不相等，包括本身(alert(NaN == NaN))

### 检测是否为NaN

`isNaN()` 接受一个参数，检测是否为NaN

### 保留指定位数的小数

将 `num.tofixed(2)` 保留两位有效数字，返回值的类型为 string 

`parseInt(num)`  对数据取整

### 数据类型转换

- `Number(str)`  将字符型数据，转化为数字

- 数组和多个数字之间的转化可以通过`...arr` 或者`...6,35,27` 实现

## String类型数据

所有的接口都只能返回新的字符串，无法修改原字符串

### 大小写转换

- `str.toUpperCase()`
- `str.toLowerCase()`

### 截取字符

- **获取单个字符**
  - `str.charAt(i)`  得到第 `i` 个字符下标
  - `str.charCodeAt(i)`  第 `i` 个字符的编码
-  **截取多个字符**
  - `str.slice(start,end)`  截取 `[start,end)` 间的数据，支持负数，此时为从后向前截取，不传`end` 则向后截取所有字符。
  - `str.substring(start,end)` 截取 `[start,end) `间的数据,不支持负数
  - `str.substr(start,i)` 从 start 开始截取 `i` 个数据

### 查找关键词出现位置

`str.indexOf('key',start)` 

从 `start` 开始查找关键词 `key` ，查找失败返回 `-1` ；`start` 可以省略

```js
var str = '从前有一座山，山上有座庙'
console.log(str.indexOf('有',4)) // 基本用法
// 查找最后一个"有"
for (let i = str.length; i > 0; i--) {
  if (str.indexOf('山', i) != -1){
    console.log(str.indexOf('山', i))
    break
  } 
}
```

> 优点：可以指定开始位置
>
> 缺点：不支持正则，只能查找一个关键字
>
> 查找最后一个关键字的 `str.lastIndexOf('keyword')`

### 判断关键字是否符合

`str.search(/正则/)` 

返回关键词位置，找不到返回 `-1` (此方法不支持正则关键字`g`)

### 获取所有符合内容

`str.match(/正则/g)`

找不到则返回 `null` ，找到返回包含所有关键词的数组

### 获取下标和内容

`regexp.exec(str)`

### 字符串分割

`str.split('str')` 

以 `str` 为分隔条件，将字符串分割，如果内容为空，则全部分割。返回值是一个数组

`str.split(/正则/)`

## Null & Undefined

### null

表示一个空指针，也是使用 `typeof()` 操作符检测 null 会返回 object 的原因

定义一个变量在将来用于保存对象，那么最好将变量初始化为 null 

## Math对象上的方法

| 方法            | 作用                                 |
| --------------- | ------------------------------------ |
| `Math.abs()`    | 返回取绝对值                         |
| `Math.max()`    | 返回最大的参数，传入逗号分割的多个值 |
| `Math.min()`    | 返回最小的参数，传入逗号分割的多个值 |
| `Math.round()`  | 舍入到最接近的整数                   |
| `Math.ceil()`   | 返回向上取整的值                     |
| `Math.floor()`  | 返回向下取整的值                     |
| `Math.random()` | 返回值为随机数，无需传入值           |

# Object类型

## 数组

为内存中多个连续的值存储多个数据的存储控件