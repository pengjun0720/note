
webAPI概述
js基础与Web APIs关联
js基础学习ECMAScript基础语法,为后面做铺垫==>JS,基础语法
webAPIs是js的应用,大量使用js基础语法做交互效果==>DOM,网页和BOM,浏览器

API
API介绍:
Application Programming Interface, 应用程序编程接口
一些预先定义的函数
给程序员提供的一种工具或者接口
会使用即可,不需了解内部如何实现
Web APIs, 浏览器接口
浏览器提供的一套操作浏览器功能和页面元素的API(BOM和DOM)
针对浏览器提供的接口,针对浏览器做交互效果
一般都有输入和输出(函数的传参和返回值),Web API很多都是方法(函数)

DOM
DOM介绍:
Document Object Model,文档对象模型
是W3C组织推荐的处理可扩展标记语言(html或xml)的标准接口
DOM树
文档(document): 一个页面,顶级节点
元素(element): 所有标签
节点(node): 所有内容(标签,属性,文本,注释等)
DOM将以上内容都看作是对象和节点
文档从上往下加载,必须等DOM构件完成,才能获取元素,所以script得写到文档面

学习API步骤
查阅文档MDN
了解功能作用
了解使用方法
了解参数和返回值

二 获取元素
1.根据ID获取: .getElementById("id名")
id名 是大小写敏感的字符串,需要加引号
document.getElementById('time');

document表示从文档根部开始查找
返回值是一个对象
通过console.log输出为标签结构
通过console.dir输出可以打印对象下具体属性和方法

2.根据标签名获取: .getElementsByTagName("标签名")
标签名是字符串,加引号,注意方法名中有s
由于返回值为多个对象,所以不能作为父元素,父元素只能是单个元素
获取ol[0]里面的所有li
document.getElementsByTagName('li');
var ol=document.getElementsByTagName('ol');
console.log(ol[0].getElementsByTagName('li'));

返回值
是指定标签名的对象的集合
得到的是动态的对象,会根据结构变化而变化
可通过索引号选中某一个元素作为父元素
以伪数组的形式存储的(HTMLcollection)
如果页面中只有一个元素,返回值还是一个伪数组	
如果页面中没有该元素,返回值是一个空的伪数组,而不是null
通过判断伪数组的length是否等于0,可以知道页面中有没有该元素
可以采用遍历的方式访问所有对象
HTMLCollection instanceof Array==>false


3.通过类名获取元素集合: .getElementsByClassName('类名')
类名是字符串
返回值是对象的集合,以伪数组形式存储
4.根据指定选择器返回第一个元素对象: .querySelector('css选择器')
选择器: 标签名/#ID名/.类名/复合选择器==>推荐使用
document.querySelector("#box>.out li:nth-child(2)")

5.根据选择器返回所有元素对象集合: .querySelectorAll('css选择器')
选择器是字符串
返回值是对象的集合,以伪数组形式存储
6.获取body元素: document.body
7.获取html元素: document.documentElement

事件基础
事件概述
简单理解
js使我们有能力创建动态页面,可以被js侦测到的行为
触发==>响应机制
组成(三要素)
1.事件源:
被触发的对象, 如buttun
2.事件类型:
如何触发, 如onclick
如果没有触发事件,直接操作,则在页面加载的时候执行
3.事件处理函数:
触发什么,如alert()
通过一个函数赋值的方式, 如alert()
如果用this,则指向调用者,也就是时间绑定对象
执行步骤
1, 获取事件源
eg, var div=document.querySelector('div')
2, 注册事件(绑定事件)
eg, div.onclick
3, 添加事件处理程序()
eg,fuction(){ console.log("我被点击了")}
操作元素
修改元素内容
元素.innerText="字符型内容"
修改元素中的纯文本,不识别html标签,去除空格和换行,非标准
元素.innerHTML="字符型内容"
识别html标签,保留空格和换行,W3C标准
可以通过修改内容直接插入/删除标签元素
修改元素属性
普通元素
元素.属性名=属性值
表单元素
表单属性
type(表单类型),value(表单值),checked(是否选中),selected,disabled(是否禁用)
表单事件
onfocus(得到焦点),onblur(失去焦点)
修改元素样式
元素.style, 行内样式操作
适合于样式少,功能简单
height,width,color等都是样式,不是属性名,只能通过style属性修改
权重
!important > js样式 > css样式
元素.className, 类名样式操作(内联)
适合于样式多,功能复杂
直接给一个类名设置一个样式, 需要时将元素类名改下
会覆盖之前的类名,如果想保留,可以使用多类名
案例
概述
自定义属性
淘宝二维码案例
京东密码框显示/隐藏提示信息
京东输入框得到/失去焦点
排他思想(算法)
使用场景
同一组元素,想要某一个元素实现某种样式,其他元素不变
步骤
获取一组元素
querySelectorAll选择一组元素
注册事件
for循环注册事件
设置样式
所有元素清除样式
使用for循环清除
不可以使用this给设置样式, this是指向外层循环
只能挨个清除,不能直接清除元素集合
给当前元素设置样式
可以使用this给当前元素设置样式
案例
按钮点击变色
百度换肤
表格经过变色
onmouseover(鼠标经过), onmouseout(鼠标离开)
表单全选
方法二:count
方法一:flag
是为了保存和使用和元素相关的临时数据,直接保存在页面,而不需要保存到数据库
只能使用特定方法操作, 不能使用内置属性的方法来操作
H5规定自定义属性名使用"data-自定义名称"作为属性名
操作
元素.getAttribute("属性"), 兼容性获取属性值
eg, div.getAttribute('data-name')
元素.dataset.自定义名称, H5新增的获取自定义属性值
获取所有data-开头的自定义属性集合
eg, div.getAttribute('data-list-name')
==>div.dataset.listName(转换驼峰命名)
元素.setAttribute("属性","值"), 设置属性值
eg, div.setAttribute('data-name', 'foo')
eg, div.setAttribute('class', 'footer')
不是className,直接写class
有时也可以直接写在标签中
元素.removeAttribute("属性"), 移除属性
eg, div.removeAttribute('data-name')
案例
tab栏切换
常规写法
自定义属性index

节点操作
节点概述
获取元素方式
利用DOM提供的方法获取元素(逻辑性不强,繁琐)
利用节点层次关系获取元素(逻辑性强,兼容性差)
父子兄关系
简介
所有内容都是节点(标签,属性,文本,注释等)	
所有节点均可通过js进行访问	
所有html元素(节点)均可被修改,创建,删除
基本属性
nodeType, 节点类型
1, 元素节点
2, 属性节点
3, 文本节点: 包括文字,空格,换行等
nodeName, 节点名称
nodeValue, 节点值

获取节点(属性)
1.父级节点
node.parentNode, 当前节点的父级节点(一个)
找不到返回null

2.子级节点
parentNode.childNodes, 当前节点的子级节点(集合)
返回值为子节点的集合(且即时更新),包含所有节点类型
如果只想获得里面的元素节点,需要专门处理,所以不提倡childNades
parentNode.children, 子元素节点(非标准但常用)
parentNode.children[0], 获取第一个子元素节点
parentNode.children[parentNode.children.length-1], 获取最后一个子元素节点
//通过div3获取兄弟节点div2和div4
//通过box获取子节点div1和div5
var div3 = document.querySelector("body div:nth-child(3)"),
    box = document.querySelector(".box")
var div1 = box.children[0],
    div2 = div3.previousElementSibling,
    div4 = div3.nextElementSibling,
    div5 = box.children[box.children.length - 1]
console.log(div1);
console.log(div2);
console.log(div3);
console.log(div4);
console.log(div5);


//  需求：鼠标经过 li，显示li里的下拉菜单ul；鼠标离开 li，隐藏ul
        var lis = document.querySelectorAll(".nav>li")
        var uls = document.querySelectorAll(".nav>li ul")
        for (let i = 0; i < lis.length; i++) {
            lis[i].onmouseover = function() {
                lis[i].children[1].style.display = "block"
            }
            lis[i].onmouseout = function() {
                lis[i].children[1].style.display = "none"
            }
        }

parentNode.firstChild, 第一个子节点
parentNode.lastChild, 最后一个子节点
parentNode.firstElementChild, 第一个子元素节点
有兼容性问题,IE9以上才支持
parentNode.laststElementChild, 最后一个子元素节点
有兼容性问题,IE9以上才支持

3.兄弟节点
node.preiousSibling, 当前元素的上一个兄弟节点(了解)
node.nextSibling, 当前元素的下一个兄弟节点(了解)
node.nextElementSibling, 当前元素的下一个兄弟元素节点
有兼容性问题,IE9以上才支持
node.preiousElementSibling, 当前元素的上一个兄弟元素节点
有兼容性问题,IE9以上才支持
自己封装一个兼容性的兄弟元素节点
if(node.nodeType===1){return node}



操作节点(方法)
1.创建新节点
document.createElement("tagName"), 动态创建元素节点
var li=document.createElement("li")
//var li=document.createElement("ul>li")  错误写法,只能写单一标签名称


2.添加新节点
node.appendChild(child), 在当前节点的子节点列表最后追加子节点
类似于数组中的push()或css中的::after伪元素	
var li=document.createElement("li")
var ul=document.querySelector("ul")
ul.appendChild(li)


node.insertBefore(child, 指定节点), 在当前节点的指定子节点的前面插入子节点
var li=document.createElement("li")
var ul=document.querySelector("ul")
ul.insertBefore(li, ul.children[0])


简易留言板发布留言案例
var btn = document.querySelector("button")
var ul = document.querySelector("ul")
var text = document.querySelector("textarea")
btn.onclick = function() {
    if (text.value !== "") {
        var li = document.createElement("li")
        li.innerHTML = text.value
         ul.insertBefore(li, ul.children[0])
    }
}


3.移除节点
parent.removeChild(child), 移除节点
var box=document.querySelector(".box")
var btn=document.querySelector("button")
btn.onclick=function(){
    if(box.children.length){//判断还有没有内容
        box.removeChild(box.children[0])//删除第一个元素
    }else
        this.disabled=true//禁用删除按钮
}


简易留言板删除留言案例
//方法一:
var btn = document.querySelector("button")
var ul = document.querySelector("ul")
var text = document.querySelector("textarea")
btn.onclick = function() {
    if (text.value !== "") {
        var li = document.createElement("li")
        li.innerHTML = text.value+'<a href="javascript:;" 
        style="float:right">删除</a>'
         ul.insertBefore(li, ul.children[0])
    }
    var lis=document.querySelectorAll("li")
    for(var i=0;i<lis.length;i++){
        lis[i].onclick=function(){
            ul.removChild(this.parentNede)
        }
    }
    
    //方法二
        var btn1 = document.querySelector(".fabu")
        var btn2 = document.querySelector(".shanchu")
        var ul = document.querySelector("ul")
        var text = document.querySelector("textarea")
        btn1.onclick = function() {
            if (text.value !== "") {
                var li = document.createElement("li")
                li.innerHTML = text.value
                ul.insertBefore(li, ul.children[0])
                text.value = ""
            }
        }
        btn2.onclick = function() {
            if (ul.children.length) { //判断还有没有内容
                ul.removeChild(ul.children[0]) //删除第一个元素
            } else
                this.disabled = true //禁用删除按钮
        }
4.复制节点
node.cloneNode(参数)
参数为空或者false,表示浅拷贝,复制标签不复制内容
参数为true,表示深拷贝,复制标签和内容
    <div>hello</div>
    <div class="box"></div>
    <script>
        var div = document.querySelector("div"),
            box = document.querySelector(".box")
        var copydiv1 = div.cloneNode()
        var copydiv2 = div.cloneNode(true)
        box.appendChild(copydiv1)
        box.insertBefore(copydiv2, box.children[0])
       console.log(box.children[0])
       console.log(box.children[1])
    </script>


案例:动态生成表格
模拟动态数据,采用对象方式存储
var datas=[
    {name:"魏璎珞",
        subject:"JavaScript",
        score:100
    },{
        name:"傅恒",
        subject:"C#",
        score:98
    },{
        name:"明玉",
        subject:"HTML",
        score:90
    },{
        name:"弘历",
        subject:"SQL",
        score:88
    }]

根据数据结构,动态追加行.列.添加数据
        var tbody = document.querySelector("tbody") //获取要追加的父元素
        for (var i = 0; i < datas.length; i++) { //外层循环控制行
            var tr = document.createElement("tr") //根据数组长度动态生成tr
            tbody.appendChild(tr) //追加行
            for (var key in datas[i]) { //内层循环控制列
                //根据对象属性数量生成td
                var tdData = document.createElement("td") 
                tr.appendChild(tdData) //追加单元格
                tdData.innerHTML = datas[i][key] //填充数据
            }
            var tdDel = document.createElement("td") //创建删除单元格
            tdDel.innerHTML = "<a href='javascript:;'>删除</a>" //删除按钮
            tr.appendChild(tdDel) //追加删除单元格
            var trs = document.querySelectorAll("tr") //获取所有行
            //循环给每个删除按钮注册事件
            for (let i = 0; i < trs.length; i++) { 
                tdDel.children[0].onclick = function() {
                    tbody.removeChild(trs[i]) //删除当前a所在行
                }
            }
       }


小结:
创建元素的三种方法
innerHTML
可添加标签和内容
采用字符串拼接形式,内存消耗高
document.createElement("tagName")
只能添加标签,不能添加内容
耗时更长,效率较低
document.write()
文档加载完成后调用,会导致页面重绘
   	
效率测试
console.time()+console.timeEnd()

事件高级

注册事件(绑定事件)
注册事件方式
传统方式(赋值操作)
利用on开头的事件
同一个元素同一个事件只能有一个处理函数,后面会覆盖前面(注册事件的唯一性)
事件监听注册事件方式(方法)
w3c标准,推荐方式
H5新增方法,有兼容性问题
同一个元素同一个事件可以注册多个处理函数

addEventListener(),事件监听方式
element.addEventListener("Type",listener[,useCapture])
"type"为字符串,不加on,如"click"
listener为监听器,如function(){}
userCapture为true,在则处于捕获阶段,否则为冒泡阶段
        var btn = document.querySelector("button")
        btn.addEventListener("click", function() {
            console.log("我被点击了1")
        })
        btn.addEventListener("click", function() {
            console.log("我被点击了2")
        })

IE9以下绑定事件的方法
element.attachEvent("type",fn)
type事件类型前加on


删除事件(解绑事件)
传统方式:
element.onclick=fn ===> element.onclick=null
事件监听:
element.addEventListener("Type",Listener) ===> element.removeEventListener(Type,Listener)
事件监听中的监听器,必须抽取出来(给一个函数名封装),才能够移除事件(因为有多个匿名监听器)
了解:
element.attachEvent("type",fn)===> element.dispatchEvent("Type",fn)


DOM事件流理论
事件流
事件传播过程
点击一个元素后,事件会在元素节点与根节点之间传播,这个路径称事件流
路径中所有的节点都会收到这个事件
3个阶段
事件捕获阶段
当前目标阶段
事件冒泡阶段
注意
js代码只能执行捕获或者冒泡其中的一个阶段
onclick和attachEvent只能得到冒泡阶段
addEventListener()第三个参数如果是true,则可以在捕获阶段调用事件处理程序
普通事件执行先执行父级,在执行子级
实际开发中更少使用捕获,更关注冒泡
有些事件没有冒泡,如onblur,onfocus,onmouseover,onmouseleave
冒泡有时会带来麻烦,有时会有巧妙用处


4. 事件对象	
4.1 简介
event就是一个事件对象,写在侦听函数的小括号中,当做形参
事件对象只有有了事件才会存在,是系统给我们自动创建的,不需要我们传递参数
事件对象是我们事件的一系列相关数据的集合,比如鼠标坐标,键盘按键
这个事件对象我们可以自己命名,比如event,evt,e
有兼容性问题,IE6/7/8通过window.event获取事件对象
官方解释
event代表了事件的状态,比如键盘,鼠标的状态,事件发生后
跟事件相关的一系列信息数据都放在这个对象里,就是event,有很多属性和方法

4.2 使用语法
event是形参,系统帮我们设定为事件对象,不需要传递实参
注册事件时,event被自动创建,并依次传递给事件监听器(事件处理函数)

4.3 兼容性方案
标准浏览器中是浏览器给方法传递的参数,只需要定义形参e就可以获取到
IE678中,浏览器不会给方法传递参数,需要的话要到window.event获取
解决:e = e || window.event;

4.4 常见属性和方法

4.4.1 触发事件的对象
e.target,目标指向, 返回触发事件的对象(标准)	
e.target和this区别
e.target返回触发事件的对象(被点击的对象)
this返回绑定事件对象
e.srcElement,源头元素, 返回触发事件的对象(非标准,ie678使用)
兼容性问题(了解)
e=e || window.event;
var target=e.target || e.srcElement;

4.4.2 阻止冒泡
e.cancelBubble=true,取消泡泡, 该属性阻止冒泡(非标准,ie678使用)
e.stopPropagation(),停止传播, 该方法阻止冒泡(标准)
兼容性问题(了解)
        var html = document.documentElement
        var body = document.body
        var ul = document.querySelector("ul")
        var li = document.querySelector("li")
        function fn1(e) {
            console.log(this + "我被点击了")
            e.stopPropagation()
        }
        html.addEventListener("click", fn1)
        body.addEventListener("click", fn1)
        ul.addEventListener("click", fn1)
        li.addEventListener("click", fn1)

4.4.3 阻止事件默认行为,如阻止链接跳转,阻止按钮提交
e.preventDefault(), 传统方式和监听方式可用, 该方法阻止默认事件/默认行为(标准方式)
return false, 仅传统方式,后面代码会不执行(传统方式)
e.returnValue, 仅传统方式, 该属性阻止默认事件/默认行为(IE 6/7/8)
var a = document.querySelector("a")
a.addEventListener("click", function(e) {
    e.preventDefault()  //阻止链接跳转
})

4.4.4 事件类型
e.type, 返回事件的类型, 如click,mouseover(不带on)

4.5 事件委托
简介:又叫做事件代理==> jQuery中叫事件委派,将事件委托给另一个元素处理
原理: 不需要给每个子节点单独设置监听器,只需给父节点添加监听器,然后利用事件冒泡原理影响设置每个子节点
例如, 给ul注册事件,然后利用事件对象的target来找到当前点击的li,因为点击li,事件会冒泡到ul上,ul有注册事件,就会触发事件监听器
作用:只操作了一次DOM,提高了程序的性能
注意:常与e.target搭配使用,操作触发事件的子元素对象

7. 常用的鼠标事件
7.1 常用的鼠标事件
鼠标事件 触发条件
onclick 鼠标点击
onmouseover 鼠标经过
onmouseout 鼠标离开
onfocus 获得焦点
onblur 失去焦点
onmousemove 鼠标移动
onmouseup 鼠标弹起
onmousedown 鼠标按下
contextmenu,用于控制显示鼠标默认菜单
//禁用鼠标右键菜单
document.addEventListener('contextmenu',function(e)){
    e.preventDefault();
}

selectstart, 鼠标开始选中事件	
//禁止鼠标选中
document.addEventListener('selectstart',function(e)){
    e.preventDefault();
}


7.2 鼠标事件对象 MouseEvent
常用鼠标事件对象

案例:返回当前鼠标坐标
document.addEventListener("click", function(e) {
   console.log("浏览器可视区坐标:", e.clientX, e.clientY)
   console.log("文档页面坐标:", e.pageX, e.pageY)  //实际开发中常用
   console.log("电脑屏幕坐标:", e.screenX, e.screenY)
})

案例:跟随鼠标的盒子
var div = document.querySelector("div")
document.addEventListener("mousemove", function(e) {
    //盒子要加绝对定位 position: absolute;
    div.style.left = e.pageX - 25 + "px"//一定要加单位px
    div.style.top  = e.pageY - 25 + "px"
})



8. 常用的键盘事件
8.1 常用的键盘事件

使用传统注册方式要加on,使用addEventListener不需要加on
三个事件的执行顺序: keydown > keypress > 填入/删除内容 > keyup
如果想要获取操作后的最新内容,使用keyup
keyup和keydown不区分大小写,keypress区分大小写

8.2 键盘事件对象 KeyboardEvent
key,返回该键的字符,有较大兼容性问题
keyCode, 返回该键的ASCII值
document.addEventListener("keyup", function(e) {
    console.log(e.keyCode)
})

常见按键对应的ASCII码值
Enter ==> 13
A ==> 65，往后依次+1
a ==> 97，往后依次+1
leftArrow ==> 37,顺时针依次+1
8.3 ASCII码值 
案例:用户按下"s",把光标定位到搜索框
使用keyCode判断按键是否为"s"
使用focus()方法使输入框获得焦点,不是onfocus()
var search = document.querySelector(".search");
//使用keyup而不使用keydown,keydown会将s输入进搜索框
document.addEventListener("keyup",function(e){
    if(e.keyCode===83){
        search.focus();//不是onfocus()
    }
})

案例:京东输入框文字放大
        var con = document.querySelector(".con")
        var text = document.querySelector(".text")
        //输入框输入时
        text.addEventListener("keyup", function() {
            if (text.value === "")
                con.style.display = "none"
            else con.style.display = "block"
            con.innerHTML = text.value
        })
        //输入框获得焦点时
        text.addEventListener("focus", function() {
            if (text.value === "")
                con.style.display = "none"
            else con.style.display = "block"
            con.innerHTML = text.value
        })
        //输入框失去焦点时
        text.addEventListener("blur", function() {
            con.style.display = "none"
        })


BOM
1. BOM概述
1.1 什么是BOM
即浏览器对象模型,提供了独立于内容而与浏览器窗口进行交互的对象,核心对象是window
由一系列相关的对象构成,并且每个对象都提供了很多方法和属性
缺乏标准,JavaScript语法的标准化组织是ECA,DOM的标准化组织是W3C,BOM最初是Netscape浏览器标准的一部分



--------------------------------------------------------------------------------
1.2 BOM构成
BOM比DOM更大,它包含了DOM
window对象是浏览器的顶级对象,具有双重角色
是JS访问浏览器窗口的一个接口
是一个全局对象
定义在全局作用域中的变量和函数,都会变成window对象的属性和方法



--------------------------------------------------------------------------------


2. window对象
2.1 窗口加载事件
2.1.1 load事件
window.onload=function(){...}或者
window.addEventListener("load",funciton(){...})

当内容完全加载完成(包括图像,脚本,css,文件等外链资源),触发该事件,就调用事件处理函数
有了window.onload,可以将js代码放在页面中的任何位置
传统注册事件方式只能写一次,如果有多个,以最后一个为准,
事件监听方式则没有限制
2.2.2 DOMContentLoaded事件
window.onDOMContentLoaded=function(){...}或者
window.addEventListener("DOMContentLoaded",function(){...})

仅当DOM加载完成(不包括样式表,图片,flash等外链资源),触发该事件,调用事件处理函数
页面图片很多的话,从用户访问到onload触发可能要很长时间,交互效果不好,此时用DOMContentLoaded时间比较合适
IE9+才支持
2.2.3 补充知识点
load是window对象的事件,不能用于document
load和DOMContentLoaded都是衡量网页加载快慢的重要指标
var img=document.querySelector("img")
window.addEventListener("load",funciton(){console.log(img)})
window.addEventListener("DOMContentLoaded",function(){console.log(img)})


2.2 调整窗口大小事件
2.2.1 resize事件
window.onresize=function(){...}或者
window.addEventListener("resize",function(){...})

只要窗口大小发生像素变化,就会触发这个事件
经常利用这个事件完成响应式布局.
window.innerWidth当前浏览器窗口的宽度

3. 定时器
3.1 两种定时器
window.setTimeout(),一次性定时器
window.setInterval(),周期性定时器

3.2 setTimeout()
window.setTimeout(调用函数,延迟时间)  //window可省略

设置一个一次性定时器,定时器到期后执行调用函数,只执行一次
延迟时间单位为毫秒,不加单位,缺省默认0ms
也可以用科学计数法表示,如3000 ===> 3e3
调用函数可以直接写函数,或者写函数名
这个函数也称为回调函数(callback)
setTimeout(function()={...},3000) //直接写匿名函数
setTimeout(fn1,3000) //直接写函数名
setTimeout("fn1()",3000) //写"函数名()",不提倡

页面中可能有很多定时器,通常给定时器加标识符/变量名(timeoutID)
定时器的返回值是一个唯一编号
var timeoutID=setTimeout(function(){...},times)


3.3 停止setTimeout()定时器
clearTimeout(timeoutID)

注意:通常需要给定时器起个标识符,否则不好停止定时器
        var start = document.querySelector(".start")
        var end = start.nextElementSibling  //下一个兄弟元素
        var timer  //注意标识符要在全局声明,否则停止计时器事件访问不到
        start.addEventListener("click", function() {
            timer = setTimeout(function() {
                    console.log("hi~~");
                },
                2000)
        })
        end.addEventListener("click", function() {
            clearTimeout(timer)  //销毁定时器
        })


3.4 setInterval()
setInterval(回调函数,间隔时间)

设置一个周期性定时器,每隔一段时间调用一次函数,可执行很多次
实际使用时可先调用一次函数,再使用setInterval()重复调用,防止页面刷新时有空白期
其他语法规范同setTimeout()
案例:京东倒计时效果
字符串/日期对象前加"+",可以转换为数字型(隐式转换)
        var hour = document.querySelector(".h"),
            minute = document.querySelector(".m"),
            second = document.querySelector(".s")
        timeEnd = +new Date("2020-8-7 24:00:00") //结束时间戳，准成数字型
        countDown()  //执行一次，防止页面刷新出现空白期
        setInterval(countDown, 1000)  //只写函数名
        function countDown() {
            var timeStart = Date.now(), //开始时间戳
                time = (timeEnd - timeStart) / 1000, //时间差ms
                h = parseInt(time / 60 / 60 % 24), //转成整数
                m = parseInt(time / 60 % 60),
                s = parseInt(time % 60)
            hour.innerHTML = h < 10 ? "0" + h : h
            minute.innerHTML = m < 10 ? "0" + m : m
            second.innerHTML = s < 10 ? "0" + s : s
        }


3.5 停止setInterval()定时器
clearInterval(timeoutID)

注意:定时器通常定义为全局变量,否则在事件执行函数外面可能访问不到
通常在全局定义,赋值为null,null也是一个对象,如var timer=null

3.6 this
this的指向在函数定义的时候是确定不了的,只有函数执行的时候才能确定,一般最终指向调用它的对象
现阶段,需要了解的this指向
全局作用域,普通函数,定时器中 ==> 全局对象window
方法调用中 ==> 调用者
构造函数中 ==> 实例对象

4. JS执行机制
4.1 JS是单线程
js语言一大特点就是单线程,即同一时间只能做一件事
所有任务都需要排队,js执行时间过长的话,页面渲染不连贯,会有加载阻塞的感觉

4.2 同步和异步
为了解决单线程问题,利用多核cpu的计算能力,HTML5提出Web Worker标准,允许JavaScript脚本创建多个进程.于是,JS中出现了同步和异步
console,log(1)
setTimeout(function(){
    console.log(2)
},0)
console,log(3)
执行顺序:1 3 2

同步任务:同步任务在主线程上执行,形成一个主线程执行栈
异步任务:异步任务放入任务队列(消息队列)中,通过回调函数实现
普通事件, 如click,resize
资源加载, 如load,error
定时器, 包括setInterval,setTimeout

4.4 执行机制
主线程不断重复: 获取任务>执行任务>再获取任务>再执行任务
这种机制被称为事件循环(eventloop)

5. location对象
5.1 什么是location对象
window对象提供的一个属性,用于获取或设置窗体的URL,并可以解析URL
返回值是一个对象,所以location属性也称为location对象

5.2 URL
统一资源定位符,互联网上标准资源的地址
包含的信息指出文件的位置以及浏览器该怎么处理它们
一般语法格式:
protocol://host[:port]/path/[?query]#fragment
eg,http://www.itcast.cn/index.html?name=andy&age=18#link




5.3 location对象的属性

重点:href和search
案例:获取URL参数数据
//第一个登录页面


5.4 location对象的方法



6. navigator对象
包含有关浏览器的信息,有很多属性
最常用的是userAgent,可以返回由客户机发送服务器的user-agent头部的值

7. history对象
与浏览器历史记录进行交互
包含用户(在浏览器窗口中)访问过的URL
实际开发中比较少用,一般会在OA办公系统用到


PC端网页特效
1. 元素偏移量offset系列
翻译过来就是偏移量,可以动态的得到该元素的位置(偏移),大小等
位置是元素距离带有定位父元素的位置(top和left)
大小是元素自身的大小(width和height)(包含padding+border+width)
注意:返回值不带单位
1.1 offset属性


1.2 offset与style区别


案例:显示鼠标在盒子内的坐标
//鼠标在盒子内移动,得到鼠标在盒子内的坐标(onmousemove)
//得到鼠标在页面中的坐标(e.pageX,e.pageY)
//得到盒子在页面中的坐标(box.offsetLeft,box.offsetTop)
//鼠标在盒子内的坐标=鼠标在页面中的坐标-盒子在页面中的坐标


案例:模态框的拖拽
//事件源:模态框最上面一行
//绑定事件:mousedown(按下),mousemove(移动),mouseup(弹起)
//拖拽过程:按下时,得到鼠标在盒子内的坐标
//拖拽过程:移动时,将动态的位置赋给模态框的left和top
//位置:模态框在页面的位置=鼠标在页面的坐标-鼠标在盒子内的坐标



2. 元素可视区client系列
翻译过来就是客户端,获取元素可视区的相关信息,动态得到元素的边框大小,元素大小
2.1 client系列属性


2.2 淘宝flexble.js源码分析
立即执行函数
创建一个独立的作用域,避免了命名冲突
pageshow事件


3. 元素滚动scroll系列
翻译过来就是滚动的,可以动态的得到该元素的大小,滚动距离等
3.1 scroll系列属性


*. 三大系列总结
offset系列经常用于获取元素位置: offsetLeft, offsetTop
client系列经常用于获取元素大小: clientWidth, clientHeight
scroll系列经常用于获取滚动距离: scrollTop, scrollLeft
页面滚动距离通过window.pageXOffset获取



*. 面试常问:mouseenter和mouseover区别?
相同点: 都是鼠标移动到元素上就会触发
不同点: 
mouseover: 鼠标经过自身盒子和子盒子都会触发,搭配mouseout
mouseenter: 鼠标经过自身盒子才会触发(因为不会冒泡),搭配mouseleave

4. 动画函数封装
4.1 动画实现原理
核心原理: 通过定时器setInterval()不断移动位置
实现步骤: 
1.获取盒子当前位置
2.让盒子在当前的位置添加移动1个距离
3.利用定时器不断重复执行
4.添加结束定时器的条件
5.注意:此元素需要添加定位,才能使用element.style.left

4.2  动画函数简单封装

4.3 动画函数给不同元素记录不同定时器

4.4 缓动效果原理
让元素运动速度有所变化,最常见的就是慢慢停下来
匀速动画：盒子位置+固定值
缓动动画：盒子位置+变化的值
思路:
1.让盒子每次移动的距离慢慢变小,速度就会慢慢降下来
2.核心算法:(目标值-现在的位置)/10作为每次移动的距离步长
3.停止的条件:让当前盒子位置等于目标位置就定制计时器 
















     

