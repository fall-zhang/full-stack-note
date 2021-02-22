## JS方法1

### 1.查询文章单词个数

```javascript
function count(str){
    var n = 1;
    for(var i = 0;i<str.length-1;i++){
        if(notalp(str[i]) > notalp(str[i+1])){
            n++;
        }
    }
    return n
}
function notalp(alp){
    if((alp >= "a" && alp <= "z")||(alp>="A" && alp<="Z")){
        // alert("测试")
        return 1;
    }
    else{
        return 0;
    }
}
```

### 2.查询文章中某个单词出现个数

```javascript
function alpTimes(supStr,subStr){
     var arr = supStr.split(subStr)
     return arr.length-1
 }
 alert(alpTimes("can i can a can like a canner to can a can","can"))
```

### 3.添加逆序字符串

```javascript
function addReverseStr(str){
    var arr = str.split(" ")
    arr.reverse()
    arr = arr.join(" ")
    return str.concat(arr)
    }
alert(addReverseStr("how old are you")) 
```

### 4.随机生成验证码工具（随机码）

```javascript
function randomTest(num){
    var arr = []
    for(i= 0;i<num;i++){
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

### 5.转化大小写

``` javascript
function trans(str){
            var newstr = str.split("");
            for(var i = 1;i < newstr.length;i++){
                if(newstr[i]>="A" && newstr[i]<="Z"){
                    newstr[i] =newstr[i].toLowerCase();
                    newstr.splice(i,0," ");
                }
            }
            alert(newstr)
            return newstr.join("")
        }
        alert(trans("MostStrongMan"))
```

### 6.字母检查工具

```javascript
function check(str){
    if ((str>='a'&&str<='z')||(str>='A'&&str<='Z'))
        return true
}
```

### 7.输出两个日期之间的间隔时间

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

###　８.输出n天后的日期

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
###    9. 一定区间内动态调整
```javascript
a内放置一个要判断的数，judge内部放置判断条件的真假，并且每隔一定数值进行真假转换
function(a,judge){
    if (a%5 == 0){
        judge =!judge
    }
}
```
### 10. 在标签里面添加新的标签

```javascript
var oDiv = document.getElementById("oDiv");
// alert(oDiv);
var Btn = document.getElementById("btn");
Btn.onclick = function(){
	var oP = document.createElement("h1");//选择添加的节点类型
    oDiv.appendChild(oP);//在oDiv内部添加一个子节点
    
    var oText = document.createTextNode("<a>咯咯咯</a>")
    oDiv.appendChild(oText);//在oDiv内部末尾添加一段纯文本
}
```




## 兼容性解决方案

```javascript
//兼容IE8 不支持 node.getElementsByClassName
function elementsByClassName(node,classStr){
    var nodes = node.getElementsByTagName("*");
    var arry =[];
    for (var i = 0 ;i<nodes.length;i++){
        if(nodes[i].className === classStr){
            arry.push(nodes[i])
        }
    }
    return arry;
}

//解决浏览器的外联样式属性选择问题
function getStyle(node,cssStyle){
	return node.currentStyle ? node.currentStyle['height'] : getComputedStyle(oDiv["height"])
}
```

## JS实例

### 鼠标在可视区域内拖拽元素

css

```
*{margin: 0;padding: 0;}
        #box1{height: 200px;width: 200px;background-color: aqua;position: absolute;top: 50px;left: 400px;}   
```

javascript

```javascript
var boxL = null;//容器鼠标点击位置距离容器左上角的位置
var boxT = null;
var defe = false;
var realL = null;// 盒子左距离document的左距离
var realT = null;
window.onload = function(){
    var oDiv = document.getElementById('box1');
	/* 拖动方块 */
    function dragInLimit(node){
         node.onmousedown = function(ev){
             defe = true;
             boxL = ev.clientX - node.offsetLeft;
             boxT = ev.clientY - node.offsetTop;
             document.onmousemove = function(ev){
                 if(defe){
                     realL = ev.clientX - boxL;
                     realT = ev.clientY - boxT;
                     if(realL<=0){
                         realL = 0;
                     };
                     if(realT<=0){
                         realT = 0;
                     };
                     if(node.offsetWidth+realL >=document.documentElement.clientWidth){
                          realL = document.documentElement.clientWidth -node.offsetHeight;
                     };
                     if(node.offsetHeight+realT >=document.documentElement.clientHeight){
                          realT = document.documentElement.clientHeight -node.offsetHeight;
                     }
                     node.style.top = (realT) +'px';
                     node.style.left = (realL) + 'px';
                 }
             }
     }
      document.onmouseup = function(){
           defe = false;
     }
}
```

html

```html
<div id="box1"></div>
```

### 跟随鼠标移动效果

css

```
div{
    height: 16px;
    width: 16px;
    border-radius: 8px;
    background-color: blueviolet;
    position: absolute;
    display: none;
}
```

js

```
window.onload = function(){
    var oDiv = document.getElementsByTagName('div');
    document.onmousemove = function(ev){
        oDiv[0].style.top = ev.clientY + 16 +'px';
        oDiv[0].style.left = ev.clientX + 16 +'px';
        
        for(var i=oDiv.length-1; i > 0;i--){
            oDiv[i].style.display = 'block';
            oDiv[i].style.top = oDiv[i-1].style.top;
            oDiv[i].style.left = oDiv[i-1].style.left;
        }
        
    }
}
```

html

```html
	<div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
```

### 生成表格

css

```css
table{border: black 1px solid;
    border-collapse: collapse;
}
table tr > td{border: solid blue 1px;width: 60px;height: 22px;}
.col1{background-color: blueviolet;}
.col0{background-color: salmon;}
```

js

```javascript
window.onload = function(){
    var tab = document.getElementById('f-table');
    var rowNum = document.getElementById('rows');
    var colNum = document.getElementById('columns');
    var sub = document.getElementById('submit');
    //如何获取到输入的值
    sub.onclick = function(){
        var rowNums = rowNum.value;//行数
        var colNums = colNum.value;//列数
        if(colNums>0 && rowNums > 0){
            for(var i = 0 ;i<rowNums; i++){
                var nRow = document.createElement('tr');//创建行
                nRow.className = 'col'+ i%2;
                for(var j = 0;j<colNums;j++){
                    var nCol = document.createElement('td');//创建列
                    nCol.innerText ='ss';
                    //如何将生成的列插入到生成的行中间
                    nRow.appendChild(nCol);
                }
                document.createElement('button');
                ; 
                var deleted = document.createElement('td');
                deleted.innerHTML = '<button>删结点</button>';
                nRow.appendChild(deleted)
                tab.appendChild(nRow);
            }
        }
    }
    tab.onclick = function(ev){
        var target = ev.target;
        if(target.nodeName.toLowerCase() == 'button'){
            alert('1');
            tab.removeChild(target.parentNode.parentNode)
        }
    }
}
```

html

```html
	<div>
        请输入生成列表的行数、列数
    </div>
    <input type="number" id="rows">
    <input type="number" id="columns">
    <button id="submit">
        提交
    </button>
    <div id="table_p">
        <table name='cattable' id="f-table">
        </table>
    </div>
```

