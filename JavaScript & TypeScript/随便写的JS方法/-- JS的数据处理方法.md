## JS方法

### 查询文章单词总数

```javascript
// 检测该数据是否为 字母 
function notalp(alp){
    if((alp >= "a" && alp <= "z")||(alp>="A" && alp<="Z")){
        return 1;
    }
    else{
        return 0;
    }
}
function count(str){
    var total = 1; // 默认第一个单词就是字母
    for(var i = 0;i<str.length-1;i++){
      // 当前者为字母，后者不是字母，则单词结束，加一
        if(notalp(str[i]) > notalp(str[i+1])){
            total ++;
        }
    }
    return total
}
```

### 查询文章中某个单词出现个数

```javascript
function alpTimes(supStr,subStr){
     var arr = supStr.split(subStr)
     return arr.length-1
 }
 alert(alpTimes("can i can a can like a canner to can a can","can"))
```

### 添加逆序字符串

```javascript
function addReverseStr(str){
    var arr = str.split(" ")
    arr.reverse()
    arr = arr.join(" ")
    return str.concat(arr)
    }
alert(addReverseStr("how old are you")) 
```

### 随机生成（随机码）

```javascript
function randomTest(num){
    var arr = []
    for(let i= 0;i<num;i++){
        var n = parseInt(Math.random()*62)
        if(n>=0&&n<=9)
            arr.push(n)
        else if(n>=10&&n<36){
            arr.push(String.fromCharCode(87+n))//小写
        }
        else if(n>=36&&n<62){
            arr.push(String.fromCharCode(29+n))//大写
        }
        else(
            alert("该方法无法输出部分不合法数据")
        )
    } 
    return arr.join("")
}
```

### 大写字母加空格

``` javascript
// 该方法可以将 AutoFix 更改为 auto fix
function trans(str){
  var newstr = str.split("");
  for(var i = 1;i < newstr.length;i++){
      if(newstr[i]>="A" && newstr[i]<="Z"){
          newstr[i] =newstr[i].toLowerCase();
          newstr.splice(i,0," ");
      }
  }
  // alert(newstr)
  return newstr.join("")
}
console.log(trans("MostStrongMan"))
```

### 字母检查工具

```javascript
// 用来检测该字符串是否为字母
function check(str){
    if ((str>='a'&&str<='z')||(str>='A'&&str<='Z'))
        return true
}
```

### 输出两个日期之间的间隔时间

```javascript
var d1= '2014/3/13'
var d2= '2019-4-8'
alert(minuesDate(d1,d2))
function minuesDate(date1,date2){
    var day1 = new Date(date1)
    var day2 = new Date(date2)
    var time1 = day1.getTime()
    var time2 = day2.getTime()
    var time = Math.abs(time1-time2)
    return parseInt(time/1000/3600/24)
}
```

###　输出n天后的日期

```javascript
var after = 20
console.log (afterDay(after))
function afterDay(n){
var date = new Date
var d = date.getDate();
date.setDate(d+n)
return date
}
```
###    一定区间内动态调整
```javascript
// a 内放置一个要判断的数，judge 内部放置判断条件的真假，并且每隔一定数值进行真假转换
function $$(a,judge){
    if (a%5 == 0){
        judge =!judge
    }
}
```

### 删除数组中的对应的值

```js
function deleteArryItem(arr, deleteItem) {
  var eventArr = []
  arr.forEach((item, index) => {
    if (item == deleteItem) {
      var str = []
      var str1 = arr.slice(0, index)
      var str2 = arr.slice(index + 1, arr.length)
      str = str.concat(str1, str2)
      eventArr = str
    }
  });
  return eventArr
}
var ss = [1, 2, 3, 4, 5, 6]
var ss = deleteArryItem(ss, 3)
```

