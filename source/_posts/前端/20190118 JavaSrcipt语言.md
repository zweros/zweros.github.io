---
title: 201901018 JavaSrcipt语言
date: 2019-1-18
categories: ['前端']
tags: [JavaScript]
---

# 1 JS 定义和特点

## 1.1 JS的作用

> HTML+CSS  实现静态的页面
>
> JS 实现动态效果，表单数据的校验,TAB的切换，背景图片的切换，JS小游戏开发

## 1.2 JS的定义

> JavaScript 一种直译式脚本语言，是一种动态类型、弱类型、基于原型的语言，内置支持类型。

​		



# 2  JS的声明和引入

## 2.1 JS的两种引入方式

- 方式一

```html
<!--JS 引入方式一 -->
<script>
    //网页弹框
    alert("Hello World");
</script>
```

- 方式二

```html
<!--JS 引入方式二 
type:指明引入的类型
src: 指明引入文件的路径
注意：方式二不可与方式一混用
-->
<script type="text/javascript" src="js/test.js" ></script>
```

注意：两种引入方式不可混用

# 3 Js 变量

## 3.1 变量的声明

> var 变量名=值

```html
<script>
    var  a= 1;
    var b= 1.12345678;
    var c= "123";
    var d = '1';
    var e = true;
    var f = new Date();

    var a = "1231";

    alert(a);


</script>
```



## 3.2 注意事项

> A、js变量名命名与Java标识符命名一致
>
> B、js中变量可以重复
>
> C、js中结尾的分号最好加上。



# 4 Js 中数据类型

> 基本数据类型:
>
> number 类型 (数字类型，不区别整型和浮点型)
>
> string 类型 (字符串类型，不区别单引号和双引号)
>
> boolean 类型(布尔类型)  true 1  false  0
>
> objet 类型(对象类型)
>
> 特殊数据类型:
>
> undefined（未定义类型，只声明变量，未赋值）
>
> Nan (不是一个数字) not a number 
>
> null(空对象)

- 测试数据类型

```js
alert(typeof(a));
```

- 三种特殊的数据类型

```js
var aa;
alert(typeof(aa)); //undefined
a="123adsf";
alert(Number(a)); //NaN
var bb=null; 
alert(bb); //object
```

# 5 运算符

> 算术运算符  + - * / % ++ --
>
> 逻辑运算符 & | ！ &&  || ^  <  >   <=  >=  !=
>
> 连接符  + 
>
> 特殊运算符  
>
> (==) 等值符(先比较类型，再比较内容，如果类型不一致，这时会统一强转number类型，再比较内容)
>
> (===) 等同符(先比较类型，再比较内容，如果类型不一致，直接返回 false )

- 连接符

```cs
var a = 1;
var b= 12.12;
var c ="11";
alert(a+b+c);
```



- 等值符

```js
alert(t==t1); //F
alert(t==t2); //T
alert(t==t3); //T			
alert(t1==t2); //F
alert(t1==t3); //F
```

- 等同符

```js
//等同符
alert(t===t1); //F
alert(t===t2); //F
alert(t===t3); //F
alert(t1===t2); //F
alert(t1===t3); //F
```

# 6  控制语句

> 条件语句
>
> if(){}
>
> if(){}else{}
>
> if(){}else if(){}else if(){} esle if(){} ... else{}
>
> 分支语句
>
> switch
>
> 循环语句
>
> while(){}
>
> do{}while()
>
> for(){}
>
> document.write()

- switch 语句 Test

```js
var = 1;
switch(a){
    case 0: 
        document.write(0);
        break;
    case 1:
        document.write(1);
        break;
    case 2:
        document.write(2);
        break;
    default:
        document.write("error")；
        break;
}
```

- 打印九九乘法表

```js
//打印九九乘法表
for(var a=1;a<=9;a++){
    for(var b=1;b<=a;b++){
        document.write(a+"*"+b+"="+a*b+"&nbsp;&nbsp;&nbsp;");
    }
    document.write("<br/ >");
}
```



# 7  函数

## 7.1 函数声明

- 方式一

```js
function 函数名() { 函数体}
```

- 方式二

```js
var 变量名 = function(参数名){函数体}
```

- 方式三(函数本身也是一个对象)

  ```js
  var 变量名 = new Function("语句");
  ```

- demo 

//方式一
function demo1(){
​    console.log("我是函数声明一哦");
}
//方式二
var demo2 = function(){
​    console.log("我是函数声明二哦");
}
//方式三
var demo3 = new Function("alert('我是函数声明3')");



## 7.2 函数的参数传递

> 在js中实参的个数和形参的个数可以不一致

```js
var demo4 = function(a,b,c){
    console.log(a+" "+b+" "+c+" ");
}
//调用函数
demo4(1,2,3);
//缺少参数的情况 报错 undefinde
demo4(1,2);
//增加参数的情况  
demo4(1,2,3,4);

```



## 7.3 函数的返回值

> 如果函数没有return语句，则返回值为 undefined 
>
> () : 函数执行符

```js
function demo5(a){
    console.log("这是控制台中"+a());
    return a;
}

var a =function(){
    console.log("这是函数 a 哦");
}

//调用函数
//demo5(4);
demo5(a); 
```



# 8  内置对象

## 8.1 日期对象

> 日期对象
>
> ​	getDate 本月的第几天
>
> ​	getDay  本星期的第几天
>
> ​	getMonth 返回的月份  0-11
>
> ​	getYear 返回的是1900年到现在年份的差值 2
>
> ​	getFullYear 返回的全年
>
> ​	toLocaleString 返回本地的时间	

```js
var date = new Date();
//获取当前的本月的第几天
console.log(date.getDate());
//获取当前的本星期的第几天
console.log(date.getDay());
//获取当前的从1900年到现在之间的年数
console.log(date.getYear());
//获取当前年
console.log(date.getFullYear());
//获取当前本地的时间
console.log(date.toLocaleString());
```

## 8.2 数学对象

> 数学对象
>
> ​	Math.random()  随机数
>
> ​	Math.floot()  向下取整
>
> ​	Math.ceil()  向上取整
>
> ​	Math.random()*9000+1000 产生四位数的验证码

```js
//获得 0-1 之间的随机数
document.write(Math.random()+"<br/>");
//获得四位数的随机数
var a = Math.random()*9000+1000;
document.write(a+"<br/>");
//向上取整
document.write(Math.ceil(a)+"<br/>");
document.write(Math.floor(a)+"<br/>");
```



## 8.3  String 对象

> chartAt    返回对应字符在所在字符串中的下标
>
> indexOf   返回下标对应的字符
>
> subStr     
>
> 若只有一个参数，则截取返回从该下标到字符串结束。
>
> 若有两个参数，第一个参数表示截取的开始位置，第二个参数表示截取的长度
>
> subString  有两个参数，第一个参数表示截取的开始位置，第二个参数表示截取的结束位置
>
> split 分割字符串

```js
/************** String *********/
var testStr = function(){
    var str1 = "szxy|xxgcxy|IOT";
    var str2 = new String("szxyxxgcxy");
    //chartAt 根据下标返回对应的下标的字符
    document.write(str2.charAt(3)+"<br />");
    //indexOf 根据字符返回对应字符的下标
    document.write(str2.indexOf('y')+"<br />");
    //substr(number) 截取从当前下标到字符串结束
    document.write(str2.substr(3)+"<br />");
    // subStr(number,number) 截取从当前下标开始并向后截取5个长度的字符串 
    document.write(str2.substr(3,5)+"<br/>");
    //subString(number,number) 截取两个下标之间的字符，注意：含头不含尾
    document.write(str2.substring(3,5)+"<br />")	;
    //split分割字符串
    document.write(str1.split('|')+"<br/>");
}

```





## 8.4  Global 

> 全局对象
>
> **eval() 表达式**   作用：把字符串转成可以执行的 JS 代码
>
> isNaN()            作用: 判断是否是一个 number 类型，若不是，则返回true，否则返回 false

```js
	/********* Global 全局对象  ******/
function testGlobal(){
    var a  = '1';
    var b = "var c = 1433223;";
    document.write(b+"<br/>");
    //eval() 表达式将 字符串转为 Js 代码执行
    eval(b);
    document.write(c);
}
```

## 8.5  Array 对象

### 8.5.1 数组声明

```js
/*******数组的声明 4种方式*******/
function demo1(){
    // 方式一
    var arr1 = new Array();
    // 方式二  给定数组的初始容量
    var arr2 = new Array(5);
    console.log("方式二 "+arr2);
    // 方式三 
    var arr3 = new Array("方式三",new String("123"),123,true);
    console.log("方式三 "+arr3);
    // 方式四
    var arr4 = ["方式四 ",new Date(),123,false];
    console.log("方式四 "+arr4);
}
```

### 8.5.2 数组初始化 

> 数组的下标可以不连续，如果没有给值，则为空

```js
/***********数组的初始化********/
function demo2(){
    var arr = []; //声明一个数组
    arr[0] = "你是李时珍的皮";
    arr[1] = 3555520;
    arr[2] = new String();
    arr[6] = "跳6";

    console.log(arr);
}
			
```

### 8.5.3 数组扩容

> 数组的扩容，通过调整数组的长度length

```js
/************数组扩容与缩小******/
function demo3(){
    var arr = [123,new String(),"Date",false];
    console.log(arr);
    console.log("数组扩容前"+arr.length);
    arr.length = 10;
    console.log("数组扩容后"+arr.length);
}

function demo4(){
    var arr = [123,new String(),"Date",false];
    console.log(arr);
    console.log("数组缩小前"+arr.length);
    arr.length = 2;
    console.log("数组缩小后 "+arr.length);
    console.log(arr);
}
```

### 8.5.4   遍历数组

> for 循环
>
> 增强 for 循环(与 Java 中的不同)

```js
/*********数组的遍历************/
function demo5(){
    var arr = ["sxzy",123,new Date(),false];
    console.log("数组遍历方式一: ");
    for(var i=0;i<arr.length;i++){
        console.log(arr[i]);
    }
    console.log("数组遍历方式二: ");
    for(var i in arr){
        console.log(i+"---->"+arr[i]);
    }
}			
```

### 8.5.5 数组方法

> push 向数组末尾添加一个或多个元素，并返回新的长度。
>
> pop 删除并返回数组的最后一个元素
>
> shift 删除数组首部的元素并返回该元素。
>
> unshift 向数组开头添加一个元素，并返回该元素的下标	
>
> splice 删除的含义，并返回删除的元素       参数: 开始删除的位置，删除的个数 
>
> splice 增加的含义  参数:开始增加的位置，0，增加的元素1，增加的元素2，。。。，增加的元素n

```js
/****************数组对象中的常用方法****/
function demo6(){
    var arr = ["szxy",123,new Date(),false];
    for(var a in arr){
        console.log(a+"---->"+arr[a]);
    }
    console.log("---------------");
    console.log(arr.push("元素1","元素2"));
    console.log("新的数组长度...");
    for(var a in arr){
        console.log(a+"---->	"+arr[a]);
    }
    console.log(arr.pop());
    //console.log(arr.shift());
    //console.log(arr.unshift("这是增加的元素2"));

    //splice 删除含义   第一个参数表示删除开始的位置    第二个参数表示删除元素的个数
    //console.log(arr.splice(0,2));
    //splice 添加含义  第二个参数表示增加元素的位置  第二个参数表示不删除元素 第三个参数表示添加的元素
    console.log(arr.splice(2,0,"2035","加油"));
    console.log("新的数组长度...");
    for(var a in arr){
        console.log(a+"---->	"+arr[a]);
    }

}
```

# 9  Event 事件  

## 9.1 Event 定义：

> 能够被 JavaScript 探测的行为

作用：通过事件来操控函数

## 9.2 Event 的触发

> onclick     单击
>
> ondblclick 双击
>
> onmouseover  鼠标放上
>
> onmouseout 鼠标离开
>
> onmosemove 鼠标移动
>
> onkeyup 键盘弹起
>
> onkeydomn   键盘按下,用于搜索提示
>
> onfocus  获得焦点
>
> onfocusout  onblur 失去焦点  
>
> onchange 内容改变，在失去焦点后		
>
> onload 页面加载完成后，触发

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>事件</title>
		<script>
			function demo1(){
				alert("单击事件");
			}
			
			function demo2(){
				alert("双击事件");
			}
			
			function demo3(){
				//alert("鼠标放上");
				//alert("鼠标移开");
				console.log("鼠标移动");
			}
			
			function demo4(){
				alert("键盘弹起...");
			}
			
			function demo5(){
				alert("键盘按下...");
			}
			
			function demo6(){
				alert("获得焦点");
				//alert("失去焦点");
			}
			
			function demo7(){
				alert("内容改变");
			}
			
			function demo(){
				console.log("页面加载完成");
			}
		</script>
	</head>
	<body onload="demo()">
		<!-- 单击事件 -->
		<input type="button" value="单击事件" onclick="demo1();demo2()"/>
        <br /><br /><br />
		
		<!-- 双击事件 -->
		<input type="button" value="双击事件" ondblclick="demo2()"/>
        <br /><br /><br />
		
		<!-- onmouseover:鼠标放上   onmouseout:鼠标移开  onmousemove:鼠标移动 -->
		<div style="width:400px; height:400px; background-color:indianred;" onmousemove="demo3()">
        </div><br /><br /><br />
			
		<!--- onkeyup: 键盘弹起 -->
		键盘弹起: &nbsp;<input type="text" name="name" onkeyup="demo4()"/>
        <br /><br /><br />
		
		<!---onkeydown: 键盘按下 -->
		键盘按下: &nbsp;<input type="text" name="keydown" onkeydown="demo5()" />
        <br /><br /><br />
		
		<!-- onfocus:获得焦点 onfocusout:失去焦点-->
		获得焦点: &nbsp;<input type="text" name="focus" onfocusout="demo6()" />
        <br /><br /><br />
		
		<!--内容改变 -->
		内容改变： &nbsp;<input type="text" name="change" onchange="demo7()"/>
        <br /><br /><br />
	</body>
</html>
```

- 注意：同一个事件可以添加多个函数，中间用`;`分号间隔。



# 10  BOM  DOM

> BOM： 浏览器对象
>
> DOM：文档对象对象
>
> BOM对象  包含 DOM对象

## 10.2 BOM 对象

### 10.2.1 三个弹框

> window.alert()
>
> window.confirm()    可以删除
>
> window.prompt()	可以输入内容

```js
	/*三种弹框*/
function demo1(){
    window.alert("确定弹框");
}

function demo2(){
    //是否确定取消弹框
    //若点击确定按钮返回 true，否则返回 false
    var flag = window.confirm("是否删除？");
    window.alert("confirm 方法的返回值： "+flag);
}

function demo3(){
    //提示输入弹框
    var name = window.prompt("请输入姓名:","例如:张三");
    window.alert(name);
}
```



### 10.2.2 定时器

> window.setTimeout()   一定时间后进行方法的调用
>
> window.setIntervarl()  每隔一定时间进行方法的调用
>
> window.clearInterval() 清除定时器

````js
/*****  定时器 ****/
function getTime(){
    var date = new Date();
    //获得本地时间
    var time = date.toLocaleString();
    //根据 id  获得 span 对象
    var  span = document.getElementById("span_1");
    span.innerHTML = time;

}
//定时器1   当 1s 后，执行 getTime 方法
//window.setTimeout("getTime()",1000);  
//定时器2  每隔 1s 后，执行getTime 方法
var val = window.setInterval("getTime()",1000);
//停止定时器
function stopTime(){
    window.clearInterval(val);
}
````



### 10.2.3  打开关闭网页

> window.open("URL")
>
> window.close()   关闭当前网页

```js
/*********开启关闭网页********/
function windowOpen(){
    //新建标签页打开 百度 网页
    var URL = "http://www.baidu.com";
    window.open(URL);
}

function windowclose(){
    //关闭当前页面
    window.close();
}
```

### 10.2.4 location 对象

> location.href   修改当前的 URL
>
> location.hostname  主机名
>
> location.port  端口号
>
> location.host  主机名+端口号
>
> reload() 重新加载页面

```JS
/******Location*******/
function testLocation(){
    //http://127.0.0.1:8020/04%20JavaScript/12%20Js%E4%B8%AD%E7%9A%84%20BOM%20%E5%AF%B9%E8%B1%A12.html
    //var href = window.location.href;
    window.location.href = "http://www.baidu.com";
    //127.0.0.1
    var hostname = window.location.hostname;
    //8020
    var port = window.location.port;
    //127.0.0.1:8020
    var host = window.location.host;
    //alert(href+"|"+hostname+"|"+port+"|"+host);
    //重新加载
    //window.location.reload(); //相等于 F5 刷新
}

```



### 10.2.5  history 

> history.length 返回浏览器历史列表中  URL 的数量
>
> history.forward() 前进
>
> histor.back()  后退
>
> history.go(number ) 控制前进和后退
>
> 正数表示前进，负数表示后退，0表示刷新

```js
/******history********/
function testHistory(){
    window.alert("长度为："+window.history.length);
}
function testHistory1(){
    window.history.forward();	
}
function testHistory2(){
    window.history.back();	
}
function testHistory3(){
    window.history.go(0);	
}

```



### 10.2.5  Screen 

> 获得当前屏幕的分辨率
>
> screen.width 
>
> screen.height

```js
/*******screen***********/
function testScreen(){
    var width = window.screen.width;
    var height = window.screen.height;
    window.alert("分辨率:"+width+"*"+height)
}

```



### 10.2.6  Navigathtor

> userAgent 返回客户端的 user-Agent 头部信息

```js
function testNavigathor(){
    //Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36
    var ua = window.navigator.userAgent;
    alert(ua);
}

```

## 10.3 DOM 对象

> 1. 查询元素(进行操作元素、或者元素的属性、文本)
> 2. 操作文本
> 3. 操作属性
> 4. 操作 CSS 样式
> 5. 操作元素



### 10.3.1 直接获得元素对象的方式

> getElementById()    
>
> getElementsByTagName()   
>
> getElementsByName

```js
/***********直接获得元素对象*****/
function demo1(){
// 通过 id 获得元素节点对象 
var name = window.document.getElementById("usr");
window.alert(name);
console.log(name);
}

function demo2(){
//获得 input 标签的所有元素对象
var input = window.document.getElementsByTagName("input");
window.alert(input);
console.log(input);
}

function demo3(){
//通过标签中 name 属性获得元素对象
var age = window.document.getElementsByName("age");
window.alert(age);
console.log(age);
}

```



### 10.3.2 间接获得元素对象的方式

> childNodes    获得子节 注意：空白文档也是一个子节点
>
> parentNode  获得父节点 
>
> nextSibling  获得下一个节点，包含空白文档	
>
> nextElementSibling 获得下一个节点，不包含空白文档 
>
> previousSibling 获得上一个节点，包含空白文档
>
> prreviousElementSibling 获得上一个节点，不包含空白文档

```js
/*******间接获得元素对象******/
function demo4(){
    var professional = window.document.getElementById("professional");
    //获得子节点对象,包含空白文档节点
    var childs = professional.childNodes;
    alert(childs.length)
    console.log(childs);
}

function demo5(){
    var p2 = document.getElementById("p2");
    //获得父节点元素对象
    var professional = p2.parentNode;
    alert(professional);
    console.log(professional);
}


function demo7(){
    var p2 = document.getElementById("p2");
    //获得兄弟节点的前一个  空白文档对象
    var op1 = p2.nextSibling;
    //获得兄弟节点的元素对象，不包含空白text对象
    var op1s = p2.nextElementSibling;
    console.log(op1);
    alert(op1);
    console.log(op1s);
}
```

### 10.3.3  操作属性

> 两种方式，一种通过属性值获取，哟中通过方法名获取
>
> 一般情况下，使用方式一居多。
>
> 注意

```js
function demo1(){
    //获得元素对象
    var name = document.getElementById("name");
    /***********方式一**********/
    //获得元素对象的属性
    var nameType = name.type;
    var nameId = name.id;
    //获得实时当前文本输入框的值
    var nameValue = name.value;

    //alert(nameType+"|"+nameId+"|"+nameValue);
    //操作元素对象的属性
    //name.type = "button";

    /*********方式二**********/
    var nameType2 = name.getAttribute("type");
    var nameId2 = name.getAttribute("id");
    //只能获得属性的默认值
    var nameValue2 = name.getAttribute("value");
    //操作元素对象的属性
    name.setAttribute("value","测试数据改变...");

    alert(nameType2+" | "+nameId2+" | "+nameValue2);

}
```

- 注意区分

  ```js
  //获得实时当前文本输入框的值
  var nameValue = name.value;
  //只能获得属性的默认值
  var nameValue2 = name.getAttribute("value");
  ```




### 10.3.4  操作样式

> 只能操作 CSS 行内样式
>
> 对于 background-color 格式的样式在 Js中需要采用驼峰命名法
>
> 通过增加class类来增加对应的css样式 注意: className 

```js
<script>
    function demo1(){
    //获得元素对象
    var div = document.getElementById("div1");
    //				var wth = div.style.width;
    //				var he = div.style.height;
    //				var backColor = div.style.backgroundColor;

    //				alert(wth+" | "+he+" | "+backColor);

    //操作 CSS 属性 注意：只能操作行内的 CSS  
    //修改的值需要使用双引号
    div.style.width = "300px";
    div.style.height = "300px";
    div.style.backgroundColor = "red";

    //增加 CSS 样式
    div.className = "div2";
}
    </script>
<style>
    .div2{
        border: 5px solid black;
    }
</style>
```

### 10.3.5 操作元素的内容

>   innerHTML  获得里面的HTML中的内容，且会识别 HTML 信息(使用内部标签)
>
>  innerText 获得里面的文本 ，不会识别 HTML 信息
>
> 注意：双标签有 innerHTML和 innerText，但是单标签获得都是用 value  属性
>
> 特殊标签：select 、textarea 使用 value获得元素的内容

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>操作文本和值</title>
		<script>
			function demo1(){
				//获得 div 元素对象
				var div = document.getElementById("div1");
				var divInnerHTML = div.innerHTML;
				var divInnerText = div.innerText;
				
				//获得元素标签下的所有内容包含子标签和文本内容
				console.log(divInnerHTML);
				//获得该元素标签下的文本内容，不包含其他子标签和空白文档
				console.log(divInnerText);
				
				//div.innerHTML += "<h1>可能我见了黄河才会死心吧</h1>"; //会识别 HTML 标签
				div.innerText+="<h1>可能我见了黄河才会死心吧</h1>";  //不会识别 HTML 标签
				
			}
			
			function demo2(){
				//获得 select 元素对象
				var sele = document.getElementById("select1");
				
				var inn = sele.innerText;
				var inn2 = sele.value;
				/******特殊情况*********/
				/***
				 * 	option 没 value 值，则选择option标签中文本内容
				 *   option 有 value 值，则选择 option标签中 value属性的值
				 * */
				console.log(inn); //获得空白
				console.log(inn2); //获得文本内容  
			}
		
			function demo3(){
				//获得 textarea 元素对象
				var textarea1 = document.getElementById("area");
				/***特殊情况  通过 value属性获取文本中内容*/
				var in1 = textarea1.value;
				
				console.log(in1);
			}
		</script>
	</head>
	<body>
		<div id="div1" style="border: 1px solid red; width:200px; height:200px	;">
			<span>可能我撞了南墙才会回头吧</span>
			
		</div>
		
		<p>
			<select name="country" id="select1">
				<option value="0">---请选择---</option>
				<option value="HeFei">合肥</option>
				<option value="Suzhou">宿州</option>
			</select>
		</p>
		
		<p>
			<textarea id="area">
				春天的天吹来夏天的雨！！！
			</textarea>
		</p>
		
		<p><input type="button"  value="测试元素" onclick="demo1()"/></p>
	</body>
</html>

```

### 10.3.6 操作节点

> createElement  创建新的节点对象
>
> appendChild	  在末尾插入子节点
>
> insertBefore  在指定标签之前插入节点
>
> removeChild 移除子标签
>
> remove     移除自身标签
>
> 删除节点先移除子节点，再移除本身。(对于表格而言)

````js
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>操作节点</title>			
		<script>
			function addNode(){
				
				//创建新节点
				var p = document.createElement("p");
				p.innerText="图片: ";
				var inp = document.createElement("input");
				inp.type = "file";
				/******注意 input标签汇总 file类型没有 value属性****/
//				inp.value = "上传";
				var inp2 = document.createElement("input");
				inp2.type="button";
				inp2.value="删除";
				p.onclick= function(){
					/***移除子标签****/
					p.removeChild(inp);
					p.removeChild(inp2);
					/***移除自身标签****/
					p.remove();
				}
				
				//增加新节点
				var fom = document.getElementById("fom");
				/******form标签中的子标签末尾添家 p 标签/
//				fom.appendChild(p);
//				p.appendChild(inp);
//				p.appendChild(inp2);
				
				var lastNode= document.getElementById("lastNode");
				/******在 lastNode元素对象之前加入p标签 ********/
				fom.insertBefore(p,lastNode);
				p.appendChild(inp);
				p.appendChild(inp2);
				
			}
		</script>
	</head>
	<body>
		<form action="#" method="get" id="fom">
			<p>
				图片: <input type="file"/>
				<input type="button"  value="增加" name="add" id="add" onclick="addNode()"/>
			</p>
			<p id="lastNode">
				<input type="submit" value="提交" />
			</p>
		</form>
	</body>
</html>

````

- 注意:添加新的节点都是相对于 form标签中

# 11DOM 编程案例01

> 制作一个表格，用于数据的填写，并可以增加新行或删除自身的行。

## 11.1 案例代码

````html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>DOM 案例</title>
		<style>/**添加表格的样式*/
			table{
				border: 1px solid red;
			/*	align-self: center;*/
			}
			tr{
				height:70px;
			}
			td{
				border: 1px solid red;
				width: 200px;
				text-align: center;
			}
		</style>
		<script>
			function addNode(){
				//创建新的节点
				var tr = document.createElement("tr");
				var td1 = document.createElement("td");
				/**onfocusout 失去焦点
				 * this 代表 td 标签的元素对象
				 * ***/
				td1.innerHTML = "<input type='text' size='7px' onfocusout='saveVal(this)'>";
				var td2 = document.createElement("td");
				td2.innerHTML = "<input type='text' size='7px' onfocusout='saveVal(this)'>"
				var td3 = document.createElement("td");
				td3.innerHTML = "<input type='button' value='添加' onclick='addNode()' >"+
								"<input type='button' value='删除' onclick='removeNode(this)'>";
				
				
				//获得 table标签 的元素对象
				var tab = document.getElementById("tab");//获得不到 table 标签对象，浏览器不报错...
				//添加新节点
				tab.appendChild(tr);
				tr.appendChild(td1);
				tr.appendChild(td2);
				tr.appendChild(td3);
							
			}
			/** thi 接受*/
			function saveVal(thi){
				//将 input 的value值传给 td 中
				var td = thi.parentNode;
				td.innerText = thi.value;
			}
			function removeNode(thi){
				
				var tr = thi.parentNode.parentNode;
				tr.remove();
			}
		</script>
	</head>
	<body>
		<table align="center" id="tab">
			<tr>
				<td>图书名称</td>
				<td>图书价格</td>
				<td>数量</td>
			</tr>
			<tr>
				<td>JavaWeb开发</td>
				<td>45.4</td>
				<td>
					<input type="button" value="增加" onclick="addNode()"/>&nbsp;
					<input type="button" value="删除" onclick="removeNode(this)"/>
				</td>
			</tr>
			<tr>
				<td>JavaWeb开发</td>
				<td>45.4</td>
				<td>
					<input type="button" value="增加" onclick="addNode()"/>&nbsp;
					<input type="button" value="删除" onclick="removeNode(this)"/>
				</td>
			</tr>
		</table>
	</body>
</html>

````

- 效果图 

![](http://www.zwer.xyz/picGo/GI0F.gif)

## 11.2 总结

1. `innerHTML `使用，可以识别 HTML语言，较于用元素对象操作节点的属性容易。
2. `this ` 指针的使用，用法与 Java 中相近，需注意是函数接受是的形参用 `thi`.
3. `input `标签中` size`属性是调整输入框大小尺寸的，不是用 `width` 和 `height` 属性



# 12 DOM 编程案例02

> 实现网页背景图片的手动更换和对话框的设计(只能点击是，当鼠标放在否按钮上，对话框的位置会发生改变)

## 12.1 案例代码

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>DOM 案列2</title>
		<style type="text/css">
			body{
				
				background-image: url("img/bjsky.jpg") ;
				background-repeat: no-repeat;
				/*background-size: 1725px;*/
				/* 设置当前 背景图片的 宽长尺寸*/
				background-size: 1725px 830px;
			}
			
			a{
				font-size: 50px;
				color: white;
			}
			
			#div_1{
				background-color:gray;
				width: 300px;
				height: 200px;
				
				text-align:center;
				padding-top: 30px;
			}
			
			#div_1 input{
				width: 50px;
				height: 30px;
			}
			
		</style>
		<script>
			var i = -1; //全局变量
			function changePic(){
				var arr = ["simple.jpg","mayun.jpg","sxt.jpg","zgc.jpg","bjsky.jpg"];
			
//				var body = document.getElementById("bd");
//				body.style.backgroundImage = "url('img/1.jpg')";
				//var i = -1; 
			
				if(i < arr.length-1){
					i++;
					//alert(i+"------------->"+arr[i]);
				}else{
					i = 0;
				}
				document.body.style.backgroundImage = "url(img/"+arr[i]+")";
				
			}
			
			// 随机改变 div区域 的位置
			function changePos(){
				
				var div = document.getElementById("div_1");
				
				div.style.marginTop = Math.random()*400+"px";
				div.style.marginLeft = Math.random()*1000+"px";
			}
			
			function changePhoto(){
					
				var body = document.getElementById("bd");
				body.style.backgroundImage = "url('img/1.jpg')";
				
				var div = document.getElementById("div_1");
				div.style.display = "none";
				
			}
		</script>
	</head>
	<body id="bd">
		<a href="javascript:changePic()">点击更换主题</a>
	
		<div id="div_1">
			<p>只要你乖就把你买条GAI</p>
			<input type="button" value="乖" onclick="changePhoto()"/>&nbsp; &nbsp; &nbsp; 
			<input type="button" value="不乖" onmouseover="changePos()" />
		</div>
	</body>
</html>

```

- 效果图

![](http://www.zwer.xyz/picGo/themetest.gif)



## 12 .2 总结

1. 背景图片设置和图片设置是两种不同的方式，不可混用。
2. 背景图片的大小通过 `background-size` 调整，而图片` img` 的大小通过 `width `、`height` 调整。
3. 要使用全局变量，需要把变量放在函数外声明初始化。



# 13 表单元素补充

> readyonly 和  disabled    
>
> 共同点:   可以看到数据，但是不可以操作数据
>
> 不同点:  readonly(只读) 里面的数据是可以提交到后台的 
>
> ​	      disabled(不可用)：数据无法提交到后台
>
> 控制表单提交： onsubmit="return checkName() "
>
> ​		             document.fom.submit()
>
> ​			    

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>表单校验</title>
		<script>
			function checkName(){
				
				var uname = document.getElementById("uname").value;
				var span_name = document.getElementById("span_name");
				
				if( uname == null || uname == ""){
					span_name.innerText = "× 账号名称不能为空";
					//return false;
				}else{
					span_name.innerText = "√账号名称合法";
					//document.fom.submit();
					var fom = document.getElementById("fom");
					console.log(fom);
					fom.submit();
					//return true;
				}
				
			}
		</script>
	</head>
	<body>
		<!--<form action="#" method="get"  onsubmit="return checkName()">-->
		<form action="#" method="get"  name="fom" id="fom">	
			<p>
				账号: <input type="text"  name="uname" id="uname"  value="ytj" />
				<span id="span_name"></span>
			</p>
			<p>
				密码: <input type="pasword" name="psw" id="psw" value="password" disabled/>
			</p>
			<p>
				<!--<input type="submit" value="提交"/>-->
				<input type="button" value="提交" onclick="checkName()"/>
			</p>
		</form>
	</body>
</html>

<!--
	readyonly： 数据不可修改，但是被表单提交
	disabled: 数据不可修改，并且不能被表单提交
	
	控制表单的提交方式 
	1. onsubmit="return checkName()"
	2. 改 input标签属性submit为button，使用 document.fom.submit();提交数据
	3. 与 方法 2类似，改用 id 获得 form 标签元素对象
	   var fom = document.getElementById("fom");
	   fom.submit();
-->

```

# 14 表单校验

## 14.1 正则表达式 

> 定义： 对于数据格式的规范性限制
>
> ^ : 开始
>
> `[0-9]  \d 数字    [a-z A-Z]`
>
> {2,4} :  段域 至少是 2 位，最多是4位
>
> {3}： 指定范围就是 3 位
>
> {2,,}: 至少是 2 位
>
> 任意
>
> $  结束
>
> \w    `[0-9] [a-z] [A-Z]`

## 14.2 源码

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>表单校验初步</title>
		<script>
			//四位随机数，用于验证码
			var randNum;
			/**********生成验证码******/
			function checkYzm(){
				var span_yzm = document.getElementById("span_yzm");
				randNum = Math.floor(Math.random()*9000+1000);
				span_yzm.innerText = randNum;
			}
	
			/*****检查用户名的合法性****/
			function checkName(){
				
				//校验用户名的正则表达式
				var reg = /^[\u4e00-\u9fa5]{3,6}$/;		
				return check("uname",reg);
				
			}
		
		/***检查密码的合法性********/
		function checkPsw(){
			
			//校验密码的正则表达式
			var reg = /\w{5,8}$/;
			return check("psd",reg);
			
		}
		
		/******检查邮箱的合法性******/	
		function checkEmail(){
			
			//校验邮箱的正则表达式
			var reg = /^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$/;
			return check("email",reg);
			
		}
		
		/*****检查手机号的合法性********/
		function checkMobileNum(){
			
			//校验手机号的正则表达式
			var reg= /^1[34578]\d{9}$/;
			return check("mobileNum",reg);
			
		}
		
		/*******检查用户输入合法性***************/
		function check(id,reg){
			var idName = document.getElementById(id);
			var val = idName.value;
			var alt = idName.alt;
			var span = document.getElementById("span_"+id);
//			console.log("span_"+id);
//			console.log(span)
			if(val == null || val == ""){
				span.innerText="×"+alt+"不能为空";
				span.style.color="red";
				return false;
			}else if(reg.test(val)){
				span.innerText="×"+alt+"合法";
				span.style.color="green";
				return true;
			}else{
				span.innerText="×"+alt+"不合法";
				span.style.color="red";
				return false;
			}
		}
		
		/********* 检查性别*******************/
		function checkSex(){
				return checkByName("sex");
		}
		
		/*******检查兴趣*******************/
		function checkHobby(){
			return checkByName("hobby");
		}
		
		/********通过 name属性 检查 *******/
		function  checkByName(nam){
			/*****注意这里是获取的变量 name 是数组类型**/
			var name = document.getElementsByName(nam);
			var span = document.getElementById("span_"+nam);
			
			for(var i=0;i<name.length;i++){
				if(name[i].checked){
					var alt = name[i].alt;
					span.innerHTML=alt+"被选中";
					return true;
				}
			}
			return false;	
		}
		
		/*****查询国籍是偶选择*******/
		function checkCountry(){
			
			// 选择国籍
			var country = document.getElementsByName("country");
			var span = document.getElementById("span_country");
			var val = country[0].value;
			if( val == 0){
				span.innerHTML="请选择国籍";
				span.style.color = "red";
				return false;
			}else{
				span.innerHTML = "国籍已选择";
				span.style.color = "green";
				return true;
			}	
		}
		
		/******检查用户输入的验证码是否正确*****/
		function checkYzmByUser(){
			
			var yzm = document.getElementById("yzm").value;
			var span = document.getElementById("span_checkYzm");
			if(yzm  == randNum){
				span.innerHTML="验证码正确";
				span.style.color = "green";
				return true;
			}else{
				span.innerHTML="验证码错误";
				span.style.color="red";
				return false;
			}
		}
		
		/********同意本公司协议*********/
		function checkAgree(){
			
			var check = document.getElementById("checkAree");
			console.log(check);
			console.log(check.checked)
			var submit = document.getElementById("checkSubmit");
			if(check.checked){
				submit.disabled = false;
			}
		}
		/******** 检查所有校验  *********/
		function checkAll(){
			
			var flag = 
			checkName()&&checkPsw()&&checkEmail()&&checkMobileNum()&&checkSex()&&checkCountry()&&checkYzmByUser();
			if(flag){
				return true;
			}else{
				return false;
			}
			
		}
		</script>
	</head>
	<body onload="checkYzm()">
		<table align="center">
			<form action="index2.html" method="get" onsubmit="return checkAll()">
				<tr>
					<td><input type="hidden" name="id" value="1001"/></td>
				</tr>
				<tr height="65px">
					<td align="center" width="100px"><p>用户名 </p></td>
					<td> 
						<input type="text" name="username"  id="uname" alt="用户名" onblur="checkName()"/>
						<span id="span_uname">用户名3到6位之间</span>
					</td>
				</tr>
				<tr>
					<td align="center"><p>密码</p></td>
					<td>
						<input type="password" name="password" id="psd" alt="密码" onblur="checkPsw()" />
						<span id="span_psd">密码的长度为6到18位</span>
					</td>
					
				</tr>
				<tr>
					<td align="center"><p>邮箱</p></td>
					<td>
						<input type="text" name="email"  id="email" alt="邮箱" onblur="checkEmail()"/>
						<span id="span_email"></span>
					</td>
					
				</tr>
				<tr>
					<td align="center"><p>手机号</p></td>
					<td>
						<input type="text" name="mobileNum" id="mobileNum" alt="手机号" onblur="checkMobileNum()"/>
						<span id="span_mobileNum"></span>
					</td>
				</tr>
				<tr align="center">
					<td><p>性别:<p></td>
					<td align="left">
						<!-- 注意：单选框必须 添加相同的 name 属性才能实现单选效果-->
						<!-- 默认选择 checke属性 -->
						男<input type="radio" name="sex" value="male"  alt="性别 " onclick="checkSex()" />
						女<input type="radio" name="sex" value="female" alt="性别"  onclck="checkSex()"/>
						<span id="span_sex"></span>
					</td>
				</tr>
				<tr align="center">
					<td><p>爱好:<p></td>
					<td align="left">
						篮球<input type="checkbox" name="hobby" alt="爱好" value="baketball" onclick="checkHobby()" />
						足球<input type="checkbox" name="hobby" alt="爱好" value="football" onclick="checkHobby()"/>
						乒乓球<input type="checkbox" name="hobby" alt="爱好" value="pingpangball" onclick="checkHobby()"/>
						<span id="span_hobby"></span>
					</td>
				</tr>
				<tr align="center"><!--下拉框-->
					<td><p>国家</p></td>
					<td align="left">
						<select name="country" onchange="checkCountry()">
							<!-- 默认选择 -->
							<option value="0">---请要求---</option>
							<option value="China">中国</option>
							<option value="South Korea">韩国</option>
							<option value="Japan">日本</option>
							<option value="American">美国</option>
						</select>
						<span id="span_country"></span>
					</td>
				</tr>
				<tr>
					<td align="center"><p>上传文件</p></td>
					<td><input type="file" name="file"/></td>
				</tr>
				<tr>	
					<td align="center">个人介绍</td>
					<td><!--多行文本框-->
						<textarea name="text" cols="30" rows="10">
							这里是默认文本的书写位置
						</textarea>
					</td>
				</tr>
				<tr align="center">
					<td><p>验证码</p></td>
					<td align="left">
						<input type="text" name="yzm" id="yzm" onblur="checkYzmByUser()"/>
						<span id="span_yzm"></span>
						<span id="span_checkYzm"></span>
					</td>
				</tr>
				<tr>
					<td align="center" colspan="2">
						 <input type="checkbox" id="checkAree" onclick="checkAgree()"/>用户 需同意本公司协议
						 <br/>
					</td>
				</tr>
				<tr align="center">
					<td colspan="2">
					<input type="submit" value="提交" disabled="none" id="checkSubmit"/> &nbsp;&nbsp;
					<input type="reset" value="重置"></td>
				</tr>
			</form>
		</table>
	</body>
</html>

```

## 14.3  总结

思路： 获取用户输入的数据，然后用正则表达式对数据进行校验。

注意：

1. id 的值获得前后名称要一致，不然不能获取到指定的元素对象
2. 通过 getElementsByName() 获取的变量是数组类型的



# 15  购物车案例

## 15.1  Js源码

```js

//获得所有选择框对象
var fav = document.getElementsByName("fav");
/************全选******/
//this 指针指向 事件触发的元素对象
function checkTest01(thi){
	
	var flag= thi.checked ;
	for(var i in fav){
		fav[i].checked = flag;
	}
	
}

/*****单选  ****/
//若单选全部被勾选，则全选也勾选
function checkTest02(){

	var flag = true;	
	for(var i=1;i<fav.length-1;i++){
		// 检查 单选框是否都勾选，若有没有被勾选的，则取消全选的勾选框
		if(!fav[i].checked){
			flag = false;
			break;
		}
	}
	
	//取消全选的勾选框
	fav[0].checked=flag;
	fav[fav.length-1].checked=flag;		
	
	
	
	//结算栏
	
	var summaryMoney = document.getElementById("span_summaryMoney"); //统计购物车总价
	var sumNumber = document.getElementById("span_sumNumber");
	var sum=0;	 //商品的总账单
	var sumNum=0;  	//商品的数目
	
	
	//判断单选框是否被选
	var num = 0;
	for(var i=1;i<fav.length-1;i++){
		if(fav[i].checked){
			num++;
			//获得父节点 ul
			var ul = fav[i].parentElement.parentElement;	
			//获得 li 元素对象的数组
			var li = ul.getElementsByTagName("li");
			//获得 单个商品的总价格加到总商品的价格中
			sum = sum+Number(li[6].innerText.split("￥")[1]);
			//结算栏的总价格
			summaryMoney.innerText = "￥"+Number(sum);
			//单个商品的总数量
			var spNum = li[5].getElementsByTagName("input");
			//结算栏的商品的总数量
			sumNum = sumNum+Number(spNum[1].value);
			sumNumber.innerText = sumNum;
			
		}
	}
	
	if( num == 0 ){
		sumNumber.innerText = 0;
		summaryMoney.innerText = "￥"+0;
	}
	
}

/*********数量按钮*******/
function checkTest03(thi,flag){
	//当前商品的数量
	var num=0;
	//获得当前商品的价格的对象
	var price = thi.parentElement.previousElementSibling;
	//获得当前商品的总价的对象
	var money = thi.parentElement.nextElementSibling;
	if(flag == 1){
		//获得上一个节点对象
		var pre = thi.previousElementSibling;
		num = Number(pre.value)+1;
		pre.value = num;
		
	}else{
		//获得下一个节点对象
		var nex = thi.nextElementSibling;
		if( nex.value > 0){
			num = Number(nex.value)-1;
			nex.value = num;
		}
	}
	money.innerText = "￥"+(Number(price.innerHTML.split("￥")[1]) * num);
	
}

/****** 删除商品 *******/
function checkTest04(thi){
	
	var div = thi.parentNode.parentNode.parentNode;
	console.log(div);
	div.remove();
	
}
```

## 15.2  HTML 代码

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title>京东购物车</title>
		<!-- 清除浏览器的页面布局-->
		<link rel="stylesheet" href="css/reset.css" />
		<!-- 京东购物车的 CSS 样式-->
		<link rel="stylesheet" href="css/jd.css" />
		<!-- icon -->
		<link rel="stylesheet" href="icon/iconfont.css" />
		
		<script type="text/javascript" src="js/jd.js" ></script>
	</head>
	<body>
		<!--导航开始-->
		<div  class="nav">
			<div class="warp">
				<ul class="nav_ul1">
					<li><a href="#"><i class="iconfont">&#xe69c</i>京东首页</a></li>
					<li><a href="#">配送到: 北京</a></li>
				</ul>
				<ul class="nav_ul2">
					<li><a href="#">洋洋的宝贝</a><span>|</span></li>
					<li><a href="#">我的订单</a><span>|</span></li>
					<li><a href="#">我的京东</a><span>|</span></li>
					<li><a href="#">京东会员</a><span>|</span></li>
					<li><a href="#">企业采购</a><span>|</span></li>
					<li><a href="#">京东手机</a><span>|</span></li>
					<li><a href="#">关注京东</a><span>|</span></li>
					<li><a href="#">客户服务</a><span>|</span></li>
					<li><a href="#">网站导航</a></li>
				</ul>
			</div>
		</div>
		<!--导航结束-->
		
		<!--搜索栏开始-->
		<div class="search">
			<!--用于中间对齐-->
			<div class="warp">
				
				<img src="img/logo.jpg" />
				<!-- 保持距离 -->
				<input type="text" name="text"/>
				<input type="button" value="搜索" />
				
			</div>
		</div>
		<!--搜索栏结束-->
		
		<!--标题栏开始-->
		<div class="title warp">
			<h1>全部商品</h1>
			
			<div class="title_div">
				<span>配送到</span>
				<select>
					<option>昌平区</option>
					<option>太兴区</option>
					<option>顺平区</option>
					<option>朝阳区</option>
				</select>
			</div>
		</div>
		<!--标题栏结束-->
		
		<!--提示栏开始-->
		<div class="tips warp">
			<ul>
				<li>
					<input type="checkbox"  name="fav"  onclick="checkTest01(this),checkTest02()"/>全选
				</li>
				<li>商品</li>
				<li>单价</li>
				<li>数量</li>
				<li>小计</li>
				<li>操作</li>
			</ul>
		</div>
		<!--提示栏结束-->
		
		<!--商品展示栏开始-->
		<div class="info warp">
			<ul>
				<li>
					<input type="checkbox" name="fav" onclick="checkTest02()" />
				</li>
				<li class="info_1">
					<img src="img/img1.jpg" />
				</li>
				<li class="info_2"><a>【京东超市】desha春秋季儿童休闲服</a></li>
				<li class="info_3"><a>颜色：灰色+粉红</a></li>
				<li class="info_4">￥182.5</li>
				<li class="info_5">
					<input type="button" value="-"onclick="checkTest03(this,0),checkTest02()"/>
					<input type="text" name="num" value="1"/>
					<input type="button" name="add" value="+" onclick="checkTest03(this,1),checkTest02()"/>
				</li>
				<li class="info_6">￥182.5</li>
				<li class="info_7"><a href="javascript:void(0)" onclick="checkTest04(this),checkTest02()">删除<br/>已到我的关注</a></li>
			</ul>
		</div>
		
		<div class="info warp">
			<ul>
				<li>
					<input type="checkbox" name="fav" onclick="checkTest02()" />
				</li>
				<li class="info_1">
					<img src="img/img2.jpg" />
				</li>
				<li class="info_2"><a>【京东超市】desha春秋季儿童休闲服</a></li>
				<li class="info_3"><a>颜色：灰色+粉红</a></li>
				<li class="info_4">￥182.5</li>
				<li class="info_5">
					<input type="button" value="-"onclick="checkTest03(this,0),checkTest02()"/>
					<input type="text" name="num" value="1"/>
					<input type="button" name="add" value="+" onclick="checkTest03(this,1),checkTest02()"/>
				</li>
				<li class="info_6">￥182.5</li>
				<li class="info_7"><a href="javascript:void(0)" onclick="checkTest04(this),checkTest02()">删除<br/>已到我的关注</a></li>
			</ul>
		</div>
		
		<div class="info warp">
			<ul>
				<li>
					<input type="checkbox" name="fav" onclick="checkTest02()" />
				</li>
				<li class="info_1">
					<img src="img/img3.jpg" />
				</li>
				<li class="info_2"><a>【京东超市】desha春秋季儿童休闲服</a></li>
				<li class="info_3"><a>颜色：灰色+粉红</a></li>
				<li class="info_4">￥182.5</li>
				<li class="info_5">
					<input type="button" value="-"onclick="checkTest03(this,0),checkTest02()"/>
					<input type="text" name="num" value="1"/>
					<input type="button" name="add" value="+" onclick="checkTest03(this,1),checkTest02()"/>
				</li>
				<li class="info_6">￥182.5</li>
				<li class="info_7"><a href="javascript:void(0)" onclick="checkTest04(this),checkTest02()">删除<br/>已到我的关注</a></li>
			</ul>
		</div>
		
		<!--商品展示栏结束-->
		
		<!--结算栏开始-->
		<div class="balance warp">
			<div class="balance_ul1">
				<ul>
					<li>
						<input type="checkbox" name="fav" onclick="checkTest01(this),checkTest02()"/>全选
					</li>
					<li>删除选中商品</li>
					<li>移动我的关注</li>
					<li>清除下柜商品</li>
				</ul>
			</div>
			<div class="balance_ul2">
				<ul>
					<li>已选择商品<span id="span_sumNumber"></span>件商品</li>
					<li>总价<span id="span_summaryMoney">￥0</span></li>
					<li><button>去结算</button></li>
				</ul>
			</div>
		</div>
		<!--结算栏结束-->
	</body>
</html>

```

## 15.3  总结

大体思路：获得节点对象，操作相应的节点。

1. 获得节点对象的方式：通过 id 属性获得，根据 this 指针表示当前对象，也可以根据节点的父子兄弟关系。

2. 计算商品总数量和总价格：采用遍历数组的方式，根据单选框或全选框是否勾选，每次调用都计算一次总和。

3. a 标签的属性 `href=""javascript:void(0)`表示在本页面中跳转。



# 16 原型列

> prototype  实现类似 Java 中类似继承的效果

## 16.1  测试

```js
<script>
    // 类
    function User(age,sex,email){
    //声明属性
    this.name = "赵云";
    this.age = age;
    this.sex = sex;
    this.email;			

    this.eat = function(){

        alert("吃饭 吃饭 吃饭 .....");
    }
}
// 类
function User2(){

    this.sleep = function(){
        alert("这里是 User2 中 的 sleep 方法， 好了 睡觉！");
    }

}

//使用原型列,必须放在 User 类创建对象之前
User.prototype = new User2();	

//创建 User 类对象
var user = new User(10,'男');
//添加 User 类成员变量
user.listen = "好运来";
alert(user.name+"|"+user.age+"|"+user.sex+"|"+user.email+"|"+user.listen);
//调用 eat方法
user.eat();
// User 类对象 user 调用  User2 的中 sleep 方法
user.sleep()
</script>
```

## 16.2 总结 

1.  类中的属性必须声明并赋值，才可以使用。只声明不赋值，属性是 undefined 类型 
2. 使用关键字 prototype ，是通过 `类名.prototype = new  类名2();` ，其中在前一个类创建对象之前，使用原型列。
3. 原型列中方法调用的顺序(以上面的源码为例), 当使用 User类对象调用方法，优先在 User 类中查找方法，若找到则直接调用方法即可。当 User 类找不到该方法时，则会到 原型列中的类 User2 查找方法，找到则直接调用方法。若方法都没有找到，则报 方法未定义。