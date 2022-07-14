> Create by **fall** on:2022-05-30
> Recently revised in:2022-07-13

## ECharts

使用：

```js
import * as echarts from 'echarts';
// 获取需要进行渲染图表的
let chartDOM = document.getElementById('main');
// 初始化
let myChart = echarts.init(chartDom,null,{renderer:'svg'}); // renderer 表示使用什么渲染器，默认为 canvas
// 如果想用 canvas，直接 let myChart = echarts.init(chartDom); 即可
// 设置渲染的内容
let options = {
  title: { // title，用来设置标题
    text: '图 2-10',
  }, 
  xAxis: { // 用来设置 x 轴的内容
    type: 'category', // category 用来标识类别
    data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
  }, 
  yAxis: {// 用来设置 y 轴的内容
    type: 'value', // 标识 value 是值
    name:'', // 坐标轴的名称，x 轴同
    axisTick:{}, // 坐标轴刻度，x 轴同
    axisLabel:{}, // 坐标轴刻度，x 轴同
  },
  toolTip:{}, // 点击数据后显示的提示
  timeLine:{}, // 时间线，根据表格的时间索引，创建不同的表格
  toolBox:{}, // 一些说明工具
  legend:{}, // 图表的说明文字（指明那个颜色是哪个数据）
  series: [{ //一连串的数据
    data: [120, 200, 150, 80, 70, 110, 130], // 数据
    type: 'bar', // 数据展现方式，bar 是柱状图，
  }]
};
options && myChart.setOption(options); // 存在 options 的时候，进行设置
```

> 渲染器的区别：svg 渲染后的内容是矢量图，放大后不会模糊，对于移动端性能更好，适合少量数据渲染。
>
> canvas 适合数据量大，某些特殊的渲染依然需要依赖 Canvas：如[炫光尾迹特效](https://echarts.apache.org/option.html#series-lines.effect)、[带有混合效果的热力图](https://echarts.apache.org//examples/editor.html?c=heatmap-bmap)等。

## 详细参数

### title

标题相关的内容

```js
const title = {
  show:true, // 是否显示标题内容
  text:'标题', // 标题的内容
  link:'链接', // 表示标题可以点击，通向哪里
  target:'blank', // 表示如何打开链接 target, self
  subtext:'小标题', // 小标题，同样也有 sublink
  textAlign:'left', // 标题的对齐方式
  padding:5, // 顾名思义
  itemGap:10, // 主副标题之间的间距
  // left, right, top, bottom 分别代表上下左右的距离，为 number
  backgroundColor:'transparent', // 背景颜色，默认为透明
  // 也可以通过 borderWidth 和 borderRadius 控制边框，边框可以为 number 也可以为 Array[number]
}
```

### grid

控制直角坐标系内绘图区域，就是绘制数据的地方

```js
const grid = {
  show:false, // 是否显示直角坐标系网格。
  // left, right, top, bottom 表示上下左右的距离
  containLabel:true, // grid 区域是否包含刻度线
  // width, height 控制高度和宽度
  backgroundColor:'transparent', // 控制背景
  tooltip:{}// 可以设置 tooltip
}
```

### legend

```js
const legend = {
  type:'plain', // 默认就是 plain，scroll 表示可以滚动
}
```



### yAxis 和 xAxis

- yAxis：控制 y 坐标轴
- xAxis：控制 x 坐标轴

```js
const xAxis = {
  show:true, // 是否显示该轴
  position:'bottom', // 默认在 bottom 底部，可选为 top，在 grid 上方
  offset:0, // X 轴相对于默认位置的偏移，在相同的 position 上有多个 X 轴的时候有用。
  type:'value', // value 为数值轴，category 为分类，time 为时间轴，log 对数轴。
  name:'坐标名',
  nameLocation:'end', // 名称在哪里显示
}
```





## 柱状图

## 散点图

## 折线图

