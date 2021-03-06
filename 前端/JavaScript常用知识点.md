# JavaScript常用知识点

## js中onload函数和jquery的ready函数

```JavaScript
window.onload = function(){
	do something
}
```
```jQuery
$(document).ready(function(){});或者
$().ready(function(){});或者
$(function(){});
```
1. onload函数是整个页面加载完(包括图片也加载完)后执行; ready函数是dom加载完(图片可能还未加载)后执行
2. onload函数只执行一次, 最后一次加载的内容覆盖之前的, 只会执行最后一次加载的内容; ready可以执行多次加载

## js中对象属性

### 访问 JavaScript 属性

访问对象属性的语法是：

```js
objectName.property; // person.age
```

或者

```js
objectName["property"]       // person["age"]
```

或者

```js
objectName[expression]       // x = "age"; person[x]
```

### JavaScript for...in 语句遍历对象的属性。

```js
var person = {fname:"Bill", lname:"Gates", age:62}; 

for (x in person) {
    txt += person[x];
}
```

## 删除属性

delete 关键词从对象中删除属性：

```js
var person = {firstName:"Bill", lastName:"Gates", age:62, eyeColor:"blue"};
delete person.age;   // 或 delete person["age"];
```

delete 关键词会同时删除属性的值和属性本身。

删除完成后，属性在被添加回来之前是无法使用的。

delete 操作符被设计用于对象属性。它对变量或函数没有影响。

delete 操作符不应被用于预定义的 JavaScript 对象属性。这样做会使应用程序崩溃。



## Closure(闭包概念)

### 概念
闭包就是一个对象（一种特殊的数据结构），它包含一个指向构成该闭包的函数的指针以及在闭包创建时外部函数的词法环境的引用。同时在闭包里面访问的外部函数词法环境里面属性也叫做非本地变量。
### 什么时候会创建闭包
当在一个内部函数被暴露到定义它的外部函数的外面时，也就是说如果一个内部函数能够从定义它的函数的外面被访问时，这个时候闭包就被创建了（这里说创建是因为闭包也是一个对象），同时该闭包函数的[[scope]]属性有对外部函数词法环境的引用，所以在外部函数调用结束后，闭包依然能够访问外部函数的词法环境对象。
```javascript
function Person(name) {
  this._name = name;
  this.getName = function() {
    return this._name;
  };
}

var p = new Person();
```
### 什么时候使用闭包
Javascript里面的闭包可以做许多有用的事情，如配置回调函数或者模仿Java语言中的private data等等。
```javascript
window.addEventListener("load", function() {
  var showMessage = getClosure("some message<br />");
  window.setInterval(showMessage, 1000);
});

function getClosure(message) {
  function showMessage() {
    document.getElementById("message").innerHTML += message;
  }
  return showMessage;
}
```

# js常用工具代码
## cookie的set和get
```javascript
var Cookie = {
	set: function (key, val, time) {//设置cookie方法
		var date = new Date(); //获取当前时间
		var expiresDay = time;  //将date设置为n天以后的时间
		date.setTime(date.getTime() + expiresDay * 24 * 3600 * 1000); //格式化为cookie识别的时间
		document.cookie = key + "=" + val + ";expires=" + date.toGMTString();  //设置cookie
	},
	get: function (key) {//获取cookie方法
		/*获取cookie参数*/
		var getCookie = document.cookie.replace(/[ ]/g, "");  //获取cookie，并且将获得的cookie格式化，去掉空格字符
		var arrCookie = getCookie.split(";")  //将获得的cookie以"分号"为标识 将cookie保存到arrCookie的数组中
		var tips;  //声明变量tips
		for (var i = 0; i < arrCookie.length; i++) {   //使用for循环查找cookie中的tips变量
			var index = arrCookie[i].indexOf("=");
			var k = arrCookie[i].substring(0, index);
			// var arr=arrCookie[i].split("=");   //将单条cookie用"等号"为标识，将单条cookie保存为arr数组
			if (key == k) {  //匹配变量名称，其中arr[0]是指的cookie名称，如果该条变量为tips则执行判断语句中的赋值操作
				tips = arrCookie[i].substring(index + 1);   //将cookie的值赋给变量tips
				break;   //终止for循环遍历
			}
		}
		return tips;
	},
	delete: function (key) { //删除cookie方法
		var date = new Date(); //获取当前时间
		date.setTime(date.getTime() - 10000); //将date设置为过去的时间
		document.cookie = key + "=v; expires =" + date.toGMTString();//设置cookie
	}
};
```
## 页面传值获取url携带的参数
```javascript
function getUrlParam(name) {
	var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)"); //构造一个含有目标参数的正则表达式对象
	var r = window.location.search.substr(1).match(reg);  //匹配目标参数
	if (r != null) return unescape(r[2]);
	return null; //返回参数值
}
```
## byte, kb, mb, gb字节转化
```javascript
function formatBytes(bytes, decimals) {
	if (bytes === 0) return '0 Byte';
	var k = 1024;
	var dm = decimals + 1 || 3;
	var sizes = ['Bytes', 'KB', 'MB', 'GB', 'TB', 'PB', 'EB', 'ZB', 'YB'];
	var i = Math.floor(Math.log(bytes) / Math.log(k));
	return parseFloat((bytes / Math.pow(k, i)).toFixed(dm)) + ' ' + sizes[i];
}
```
## 将毫秒值转为本地时间
```javascript
function getLocalTime(nS) {
	var date = new Date(nS);
	var Y = date.getFullYear() + '-';
	var M = (date.getMonth() + 1 < 10 ? '0' + (date.getMonth() + 1) : date.getMonth() + 1) + '-';
	var D = (date.getDate() < 10 ? '0' + date.getDate() : date.getDate()) + ' ';
	var h = (date.getHours() < 10 ? '0' + date.getHours() : date.getHours()) + ':';
	var m = (date.getMinutes() < 10 ? '0' + date.getMinutes() : date.getMinutes()) + ':';
	var s = (date.getSeconds() < 10 ? '0' + date.getSeconds() : date.getSeconds());
	return Y + M + D + h + m + s;
}
```
## js字符串判空
```javascript
//判断字符是否为空的方法
function isEmpty(obj) {
	if (typeof obj == "undefined" || obj == null || obj == "") {
		return true;
	} else {
		return false;
	}
}
// 简化
function isEmpty(obj) {
        return typeof obj == "undefined" || obj == null || obj === "";
    }
```
