## 数据类型

### 基础类型

```ts
// 布尔类型
let flag:boolean = false
```

和 JS 相同，TS 里面所有数字都是浮点数，都是 number

```ts
// 数字类型
let a1:number = 10 //十进制
let a2:number = 0b1010 //二进制
let a3:number = 0o12 // 八进制
let a4:number = 0xa // 十六进制
// 字符串类型
let str:string = '卷起千堆雪'
```

undefined & null 

undefined 和 null可以作为其他数据类型的子类型（其他类型的子集），可以把该类型赋值给其他类型。

```ts
let notNum:undefined = undefined
let num1:number = null
let num2:number = undefined
```

**数组类型**

```ts
let arr1:number[] =[10,20,30,40] 
let arr2:Array<number> = [100,200,300]
```

**元组**

元组类型允许表示一个已知元素数量和类型的数组，`各元素的类型不必相同`。 比如，你可以定义一对值分别为 `string` 和 `number` 类型的元组。

```ts
let arr3:[string,number,boolean,] = ['55',233,true]
// 数组中每一个相应的类型都只能使用对应的方法
console.log(arr3[0].substring(1)) // OK
console.log(arr3[1].substring(1)) // Error, 'number' 不存在 'substring' 方法
```

**枚举类型**

枚举类型中，每一个数据都可以叫做元素,

可以为每一个元素进行编号，枚举中的数据值可以为中文，但是不推荐

```ts
enum Color{
  cyan=10,
  magenta,
  yellow
}
let color:Color = Color.red
console.log(Color.cyan+"---"+Color)
```

**any 类型**

个数不确定，或者类型不确定都可以使用 any 进行定义

```ts
// 任意数据类型
let num1:any = '遇贵人先立业，遇佳人先成家，遇富婆成家立业'
let arr:any[]= [11,35,'年少不知软饭香，错把青春到插秧']
```

**void 类型**

没有任何类型，在方法后面使用，意味着该函数没有返回值

```ts
function show():void{
  console.log('富婆把我心儿碎，予我别墅和崩溃')
}
```

**object 类型**

表示除了 number, string, boolean 之外的数据类型

```ts
function getObj(obj:object):object{
  console.log(obj)
	return {
    name:'菲菲小公主',
    age:62
  }
}
console.log(getObj({
  giao:"giao"
}))
```

**联合类型**

取值时可以为多种类型中的一种类型，方法必须同时满足两个类型

```ts
function toString2(x: number | string) : string {
  return x.toString()
}
```

### 接口

用接口来表明定义**对象**的类型，必须按照所有已定义的类型进行存储，且不能有任何多余。

在实现接口时，使用 `interface` 进行定义对象的类型。

- 可以使用 `readonly` 限制接口，只读 
- 也可以使用 `?` 进行更改接口的值，使接口可以传值也可以不传。

```ts
interface OnePerson{
    readonly name:string
    age:number
    hobby:string
    salary?:number
  }
  let tutou:OnePerson = {
    name:'琦玉',
    age:33,
    hobby:"兴趣使然的英雄"
  }
  tutou.age = 66
  console.log(tutou)
```

#### **函数类型**

```ts
interface Hero{
    (name:string,heroName:string):boolean
  }
  const tutou = function(name:string,heroName:string):boolean{
    // search 作用：返回符合元素的下标，如果为 -1 说明字符串中不存在该数值
    return name.search(heroName) > -1
  }
  console.log(tutou("秃头披风侠","秃头"))
```

#### **类类型**

一个类的类型可以通过接口完成约束，并且一个类可以被多个接口进行约束。

接口和接口之间可以继承，类和接口之间称为实现

每一个方法必须都要可以使用

```ts
// 定义一个接口
interface OneHero{
  hero()
}
// 此时接口可以看做 Person 类的一个约束
class Person implements OneHero{
  hero(){
    console.log('只有内心强大的人，才有资格做英雄')
  }
}
let jodge = new Person
jodge.hero()
```

#### 多个接口修饰

一个类，同时被多个接口进行修饰

```typescript
interface OneHero{
  hero() // OneHero 限制必须拥有 hero 方法
}
interface TheHero{
  action() // TheHero 限制必须拥有 action 方法
}
class Person implements OneHero,TheHero {
  hero(){
    console.log("一颗执着的心")
  }
  action(){
    console.log("坚定不移的行动")
  }
}
let jodge = new Person
jodge.hero()
jodge.action()
```

### 类

#### **类的基本使用**

```ts
class SelfIntrduce {
  name: string
  age: number
  hobby: string
  constructor(
  name: string = '小甜甜',
   age: number = 19,
   hobby: string = 'both'
  ) {
    this.name = name
    this.age = age
    this.hobby = hobby
  }
  introduce() {
    console.log(
      `大家好，俺是${this.name},今年俺${this.age},俺喜欢${this.hobby}`
    )
  }
}
let liu = new SelfIntrduce('狗子', 3, '嘿嘿')
liu.introduce()
```

#### **类的继承**

如果 a 继承了 A 类的内容，a 称为子类，A 称为基类

子类也叫派生类，基类也叫父类

```ts
class Hero {
  // 类的属性
  name:string
  heroName:string
  activeTime:number
  // 类的构造方法
  constructor(name:string= '小汉堡',heroName:string = '铁血汉堡',activeTime:number = 2){
    this.name = name
    this.heroName = heroName
    this.activeTime = activeTime
  }
  // 类的实例方法
  heroInfo(str:string){
    console.log(`我是一名兴趣使然的英雄，我叫${this.name},我的英雄名是${this.heroName},我已经活跃了${this.activeTime}年`)
    console.log('一句话描述自己：'+str)
  }
}
// 继承类的方法
class SuperHero extends Hero{
  constructor(name:string,heroName:string,activeTime:number){
    super(name,heroName,activeTime)
  }
  // 这里可以调用父亲的
  sayHi(){
    super.heroInfo('我懒得描述')
  }
}
let he = new Hero()
he.heroInfo('汉堡，我只服自己')
let jienuosi = new SuperHero('杰诺斯',"魔鬼改造人",4)
jienuosi.sayHi()
jienuosi.heroInfo("rest in peace my enermy")
```

#### **类的多态**

```ts
class Hero {
    name:string
    constructor(name:string='汉堡'){
      this.name = name
    }
    jump(height:number=2){
      console.log(`这个英雄能跳${height}m 高`)
    }
  }
  class SurperHero extends Hero{
    jump(height:number=100){
      console.log(`这个英雄能跳${height}m 高`)
    }
  }
  class OtherHero extends Hero{
    jump(height:number=18){
      console.log(`这个英雄能跳${height}m 高`)
    }
  }
  // let jienuos:SurperHero =new SurperHero
  // let bickHero:OtherHero =new OtherHero
  let jienuos:Hero =new SurperHero // Hero 的子类，都可以用 Hero 进行约束，但是调用的时候是调用的子类方法
  let bickHero:Hero =new OtherHero
  jienuos.jump()
  bickHero.jump()
  function showThem(hero:Hero){
    hero.jump()
  }
  showThem(jienuos)
```

#### **类的修饰符**

类的修饰符，描述类的成员，构造函数，方法的可访问属性

- private 私有修饰符，智能在内部进行访问
- public 默认修饰符，意思是公共修饰符，外部构造方法和成员都可以访问
- protected 保护修饰符，能在子类构造方法中访问，外部无法访问
- readonly 只读修饰符，修饰之后，只能进行读取，不能更改属性名（类的方法内，也是无法修改属性值），构造函数时，可以对属性成员进行修改
- static 声明静态类，智能通过类名进行调用
- abstract 抽象类，一般抽象类作为父类，子类必须实现抽象类中的抽象属性和方法

构造函数时，只要使用修饰符进行修饰，就可以不用添加类的属性

```ts
class Hero {
  public heroName:string // 所有成员都有自己默认的修饰符 public 
  // private name:string // 用私有 private 进行限制后，只能在类本身使用
  readonly hobby:string 
  age:number
  constructor(name:string= '汉堡骑士'){
    this.name= name
  }
  jump(num1:number = 10){
    console.log(`我叫${this.heroName}是一个英雄`)
    console.log('一窜就是'+ num1 +'米这么高')
  }
}
let bickKnight = new Hero
bickKnight.heroName = '单车骑士'
bickKnight.jump(0.5)
console.log(bickKnight.hobby)
```

#### **存取器 ** 

setter & getter 存取器可以在用户使用存储功能，或者是调用查找功能时触发。

```ts
class Hero {
    name: string
    heroName: string
    constructor(name: string = '汉堡', heroName: string = '蜜汁') {
      this.name = name
      this.heroName = heroName
    }
    get fullName() {
      console.log('loading.....')
      return this.heroName + '_' + this.name 
    }
    set fullName(msg){
      let mm = msg.split("_")
      console.log(mm)
      this.name= mm[1]
      this.heroName= mm[0]
    }
  }
  let mememe = new Hero()
  console.log(mememe.fullName)
  mememe.fullName = ('秃头披风侠_琦玉')
  console.log(mememe.fullName)
  console.log(mememe.name)
```

#### **static 静态属性**

静态属性中自带 name 属性，所以不可以设置 name 为静态属性值，

使用 static 绑定构造方法和构造属性后，只能通过类名进行访问

```ts
class Hero {
  static heroName:string = '汉堡'
  static heroTag(){
    console.log('英雄就是在别人无法面对时挺身而出的人')
  }
}
// cc 此时为实例对象，不能调用静态方法
let cc = new Hero
// console.log(cc.heroName)
// 无法输出 cc.heroName
console.log(Hero.heroName)
Hero.heroName = '秃头披风侠'
console.log(Hero.heroName)
Hero.heroTag()
```

#### **abstract 抽象类**

```ts
 abstract class Hero {
    // 抽象类 : 抽象类的目的是为了子类进行服务的
    // 抽象类中很少使用抽象属性让子类进行呈现
    static jump(){
      console.log('冲冲冲吃好吃')
    }
    abstract eat() // abstract可以有抽象的类，但是不能有具体的实现
  }
  class SuperHero extends Hero{
    eat(){
      console.log('take it to your month')
    }
    static eat(){
      console.log('suck it')
    }
  }
  // let qiyu = new Hero() // 无法实例化抽象类
  Hero.jump()
  SuperHero.eat()
  let cc = new SuperHero()
  cc.eat()
```

### 函数

#### 函数的基本使用方法

```ts
// js的函数书写方法
  function add(x, y) {
    return x + y
  }
  let sum = function (x, y) {
    return x + y
  }
  let plus = (x: string, y) => {
    return x + y
  }
  // ts 的函数的书写方法
  let keke = (y: string): string => {
    console.log('咳咳' + y)
    return ''
  }
  keke('fuck')
```

#### 可选参数 默认参数 和剩余参数

```ts
function create(x:number = 22,y?:string):number{
  console.log(y)
  return x +3
}
console.log(create())
// 剩余参数存放在 ... 后面即可捕获剩余参数
function mountain(num:number,...arr:string[]){
    console.log('这是第'+num+"次输出")
    console.log(arr[0])
  }
  mountain(12,"阿尔卑斯",'珠穆朗玛','嵩山',"华山")
```

#### 函数的重载

函数经过重载后，只能传入对应的值，

```ts
function plusOrAdd(x:number,y:number) // 使函数可以传入两个 number 类型的数据
function plusOrAdd(x:string,y:string) // 使函数可以传入两个string类型的数据
function plusOrAdd(x,y):void{
  console.log(x+y)
}
plusOrAdd(10,12)
plusOrAdd("小天才","22")
// plusOrAdd('做坏事',22)
```

#### 函数的泛型

泛型意思是，可以等到需要传入值的时候，这时候再限定参数将所需要的类型传入，达到限制类型的目的

```ts
function anyType<C>(x:C,y:number):C[]{
  let arr = []
  for(let i =0 ;i<y;i++){
    arr.push(x)
    console.log('hite me')
  }
  return arr
}
console.log(anyType<number>(12,13))
```

