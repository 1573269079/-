### 跨浏览器事件

```javascript
//跨浏览器添加事件
function addEvent(obj,type,fn){
    if(obj.addEventListener){
        obj.addEventListener(type,fn,false);
    }else if(obj.attachEvent){//IE
        obj.attchEvent('on'+type,fn);
    }
}

//跨浏览器移除事件
function removeEvent(obj,type,fn){
    if(obj.removeEventListener){
        obj.removeEventListener(type,fn,false);
    }else if(obj.detachEvent){//兼容IE
        obj.detachEvent('on'+type,fn);
    }
}

//跨浏览器阻止默认行为
function preDef(ev){
    var e = ev || window.event;
    if(e.preventDefault){
        e.preventDefault();
    }else{
        e.returnValue =false;
    }
}

//跨浏览器获取目标对象
function getTarget(ev){
    if(ev.target){//w3c
        return ev.target;
    }else if(window.event.srcElement){//IE
        return window.event.srcElement;
    }
}

//跨浏览器获取滚动条位置，sp == scroll position
function getSP(){
    return{
        top: document.documentElement.scrollTop || document.body.scrollTop,
        left : document.documentElement.scrollLeft || document.body.scrollLeft;
    }
}

//跨浏览器获取可视窗口大小
function  getWindow () {
	if(typeof window.innerWidth !='undefined') {
		return{
			width : window.innerWidth,
			height : window.innerHeight
		}
	} else{
		return {
			width : document.documentElement.clientWidth,
			height : document.documentElement.clientHeight
		}
	}
},
```

### HTML5 DOM 选择器   

```javascript
// querySelector() 返回匹配到的第一个元素
var item = document.querySelector('.item');
console.log(item);
// querySelectorAll() 返回匹配到的所有元素，是一个nodeList集合
var items = document.querySelectorAll('.item');
console.log(items[0]);
```

### 阻止默认行为

```javascript
// 原生js
document.getElementById('btn').addEventListener('click', function (event) {
    event = event || window.event;
    if (event.preventDefault){
        // w3c方法 阻止默认行为
        event.preventDefault();
    } else{
        // ie 阻止默认行为
        event.returnValue = false;
    }
}, false);
// jQuery
$('#btn').on('click', function (event) {
    event.preventDefault();
});
```

### 阻止冒泡

```javascript
// 原生js
document.getElementById('btn').addEventListener('click', function (event) {
    event = event || window.event;
    if (event.stopPropagation){
        // w3c方法 阻止冒泡
        event.stopPropagation();
    } else{
        // ie 阻止冒泡
        event.cancelBubble = true;
    }
}, false);
// jQuery
$('#btn').on('click', function (event) {
    event.stopPropagation();
});
```

### 鼠标滚轮事件

```javascript
$('#content').on("mousewheel DOMMouseScroll", function (event) { 
    // chrome & ie || // firefox
    var delta = (event.originalEvent.wheelDelta && (event.originalEvent.wheelDelta > 0 ? 1 : -1)) || 
        (event.originalEvent.detail && (event.originalEvent.detail > 0 ? -1 : 1));  
    if (delta > 0) { 
        // 向上滚动
        console.log('mousewheel top');
    } else if (delta < 0) {
        // 向下滚动
        console.log('mousewheel bottom');
    } 
});
```

### 检测浏览器是否支持svg

```javascript
function isSupportSVG() { 
    var SVG_NS = 'http://www.w3.org/2000/svg';
    return !!document.createElementNS &&!!document.createElementNS(SVG_NS, 'svg').createSVGRect; 
} 
// 测试
console.log(isSupportSVG());
```

### 检测浏览器是否支持canvas

```javascript
function isSupportCanvas() {
    if(document.createElement('canvas').getContext){
        return true;
    }else{
        return false;
    }
}
// 测试，打开谷歌浏览器控制台查看结果
console.log(isSupportCanvas());
```

### 检测是否是微信浏览器

```javascript
function isWeiXinClient() {
    var ua = navigator.userAgent.toLowerCase(); 
    if (ua.match(/MicroMessenger/i)=="micromessenger") { 
        return true; 
    } else { 
        return false; 
    }
}
// 测试
alert(isWeiXinClient());
```

### jQuery 获取鼠标在元素上的坐标

```javascript
$('#ele').click(function(event){
    //获取鼠标在图片上的坐标 
    console.log('X：' + event.offsetX+'\n Y:' + event.offsetY); 
    //获取元素相对于页面的坐标 
    console.log('X：'+$(this).offset().left+'\n Y:'+$(this).offset().top);
});
```

### 验证码倒计时代码

```javascript
<!-- dom -->
<input id="send" type="button" value="发送验证码">
// 原生js版本
var times = 60, // 临时设为60秒
timer = null;
document.getElementById('send').onclick = function () {
    // 计时开始
    timer = setInterval(function () {
        times--;
        if (times <= 0) {
            send.value = '发送验证码';
            clearInterval(timer);
            send.disabled = false;
            times = 60;
        } else {
            send.value = times + '秒后重试';
            send.disabled = true;
        }
    }, 1000);
}


// jQuery版本
var times = 60,
    timer = null;
$('#send').on('click', function () {
    var $this = $(this);
    // 计时开始
    timer = setInterval(function () {
        times--;
        if (times <= 0) {
            $this.val('发送验证码');
            clearInterval(timer);
            $this.attr('disabled', false);
            times = 60;
        } else {
            $this.val(times + '秒后重试');
            $this.attr('disabled', true);
        }
    }, 1000);
});
```

### 常用的一些正则表达式

```javascript

//匹配字母、数字、中文字符 
/^([A-Za-z0-9]|[\u4e00-\u9fa5])*$/ 
 
//验证邮箱 
/^\w+@([0-9a-zA-Z]+[.])+[a-z]{2,4}$/ 
 
//验证手机号 
/^1[3|5|8|7]\d{9}$/ 
 
//验证URL 
/^http:\/\/.+\./
 
//验证身份证号码 
/(^\d{15}$)|(^\d{17}([0-9]|X|x)$)/ 
 
//匹配中文字符的正则表达式 
/[\u4e00-\u9fa5]/ 
 
//匹配双字节字符(包括汉字在内) 
/[^\x00-\xff]/
```

### js时间戳、毫秒格式化

```javascript

function formatDate(now) { 
    var y = now.getFullYear();
    var m = now.getMonth() + 1; // 注意js里的月要加1 
    var d = now.getDate();
    var h = now.getHours(); 
    var m = now.getMinutes(); 
    var s = now.getSeconds();
    return y + "-" + m + "-" + d + " " + h + ":" + m + ":" + s; 
} 
var nowDate = new Date(1442978789184);
alert(formatDate(nowDate));
```

### js限定字符数（注意：一个汉字算2个字符）

```javascript
<input id="txt" type="text">
//字符串截取
function getByteVal(val, max) {
    var returnValue = '';
    var byteValLen = 0;
    for (var i = 0; i < val.length; i++) { if (val[i].match(/[^\x00-\xff]/ig) != null) byteValLen += 2; else byteValLen += 1; if (byteValLen > max) break;
        returnValue += val[i];
    }
    return returnValue;
}
$('#txt').on('keyup', function () {
    var val = this.value;
    if (val.replace(/[^\x00-\xff]/g, "**").length > 14) {
        this.value = getByteVal(val, 14);
    }
});
```

### 在字符串中查找子字符串

```javascript
<script type="text/javascript">
    var test = 'Welcome to my blog!';
    var value = 'blog';
    var subValue = test.indexOf(value);
    console.log(subValue);//14,子字符串的索引
</script>
```

### js判断是否移动端及浏览器内核

```javascript
var browser = { 
    versions: function() { 
        var u = navigator.userAgent; 
        return { 
            trident: u.indexOf('Trident') > -1, //IE内核 
            presto: u.indexOf('Presto') > -1, //opera内核 
            webKit: u.indexOf('AppleWebKit') > -1, //苹果、谷歌内核 
            gecko: u.indexOf('Firefox') > -1, //火狐内核Gecko 
            mobile: !!u.match(/AppleWebKit.*Mobile.*/), //是否为移动终端 
            ios: !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/), //ios 
            android: u.indexOf('Android') > -1 || u.indexOf('Linux') > -1, //android 
            iPhone: u.indexOf('iPhone') > -1 , //iPhone 
            iPad: u.indexOf('iPad') > -1, //iPad 
            webApp: u.indexOf('Safari') > -1 //Safari 
        };  
    }
} 
if (browser.versions.mobile() || browser.versions.ios() || browser.versions.android() || browser.versions.iPhone() || browser.versions.iPad()) { 
    alert('移动端'); 
}
```

### js对象冒充

```javascript
<script type="text/javascript">
    function Person(name , age){
        this.name = name ;
        this.age = age ;
        this.say = function (){
            return "name : "+ this.name + " age: "+this.age ;
        } ;
    }
    var o = new Object() ;//可以简化为Object()
    Person.call(o , "zhangsan" , 20) ;
    console.log(o.say() );//name : zhangsan age: 20 
</script>
```

### js 异步加载和同步加载

```javascript
//异步加载也叫非阻塞模式加载，浏览器在下载js的同时，同时还会执行后续的页面处理。
//在script标签内，用js创建一个script元素并插入到document中，这种就是异步加载js文件了：
(function() {     
    var s = document.createElement('script');    
    s.type = 'text/javascript';     
    s.async = true;    
    s.src = 'http://yourdomain.com/script.js';    
    var x = document.getElementsByTagName('script')[0];    
     x.parentNode.insertBefore(s, x); 
})();
```

### 同步加载

```
平常默认用的都是同步加载。如：
<script src="http://yourdomain.com/script.js"></script>
同步模式又称阻塞模式，会阻止流览器的后续处理。停止了后续的文件的解析，执行，如图像的渲染。浏览器之所以会采用同步模式，是因为加载的js文件中有对dom的操作，重定向，输出document等默认行为，所以同步才是最安全的。
通常会把要加载的js放到body结束标签之前，使得js可在页面最后加载，尽量减少阻塞页面的渲染。这样可以先让页面显示出来。
同步加载流程是瀑布模型，异步加载流程是并发模型。
```

### js获取屏幕坐标

```javascript
//获取鼠标坐标
<script type="text/javascript">
    function mousePosition(ev){
        if(ev.pageX || ev.pageY){
            return {x:ev.pageX, y:ev.pageY};
        }
        return {
            x:ev.clientX + document.body.scrollLeft - document.body.clientLeft,
            y:ev.clientY + document.body.scrollTop - document.body.clientTop
        };
    }
    function mouseMove(ev){
        ev = ev || window.event;
        var mousePos = mousePosition(ev);
        document.getElementById('xxx').value = mousePos.x;
        document.getElementById('yyy').value = mousePos.y;
    }
    document.onmousemove = mouseMove;
</script>
X:<input id="xxx" type="text"> Y:<input id="yyy" type="text">

/*
 * documentElement 属性可返回文档的根节点。
 * scrollTop() 为滚动条向下移动的距离
 * document.documentElement.scrollTop 指的是滚动条的垂直坐标
 * document.documentElement.clientHeight 指的是浏览器可见区域高度
 */
```

##### IE

```
document.body.clientWidth ==> BODY对象宽度
document.body.clientHeight ==> BODY对象高度
document.documentElement.clientWidth ==> 可见区域宽度
document.documentElement.clientHeight ==> 可见区域高度
```

##### Firefox

```
document.documentElement.scrollHeight ==> 浏览器所有内容高度
document.body.scrollHeight ==> 浏览器所有内容高度
document.documentElement.scrollTop ==> 浏览器滚动部分高度
document.body.scrollTop ==>始终为0
document.documentElement.clientHeight ==>浏览器可视部分高度
document.body.clientHeight ==> 浏览器所有内容高度
```

##### Chrome

```
document.documentElement.scrollHeight ==> 浏览器所有内容高度
document.body.scrollHeight ==> 浏览器所有内容高度
document.documentElement.scrollTop==> 始终为0
document.body.scrollTop==>浏览器滚动部分高度
document.documentElement.clientHeight ==> 浏览器可视部分高度
document.body.clientHeight ==> 浏览器所有内容高度
```

##### PageX和clientX

```
PageX:鼠标在页面上的位置,从页面左上角开始,即是以页面为参考点,不随滑动条移动而变化
clientX:鼠标在页面上可视区域的位置,从浏览器可视区域左上角开始,即是以浏览器滑动条此刻的滑动到的位置为参考点,随滑动条移动 而变化.
PageX只有FF特有,IE则没有这个，所以在IE下使用这个：
PageY=clientY+scrollTop-clientTop;(只讨论Y轴,X轴同理,下同)
scrollTop代表的是被浏览器滑动条滚过的长度
offsetX:IE特有,鼠标相比较于触发事件的元素的位置,以元素盒子模型的内容区域的左上角为参考点,如果有boder`,可能出现负值
chrome和safari 完全支持所有属性
```

### js拖拽效果

```javascript
<style type="text/css">
    #login{
        height: 100px;
        width: 100px;
        border: 1px solid black;
        position: relative;
        top:200px;
        left: 200px;
        background: red;
    }
</style>
//offsetTop 返回的是数字，而 style.top 返回的是字符串，除了数字外还带有单位：px。
```

### js循环遍历数组

```javascript
<script>  
   //循环遍历数组  
   var animals = ["cat",'dog','human','whale','seal'];  
   var animalString = "";  
   for(var i = 0;i<animals.length;i++){  
       animalString += animals[i] + " ";  
   }  
   alert(animalString);  //输出数组里的每个项
</script> 
```

##### 遍历二维数组

```javascript
<script> 
	 var arr=[[0,0,0,0,0,0],[0,0,1,0,0,0],[0,2,0,3,0,0],[0,0,0,0,0,0]]; 
	 for(var i=0;i<arr.length;i++){ 
	 //遍历每一个具体的值 
	 for(var j=0;j<arr[i].length;j++){ 
	 document.writeln(arr[i][j]+" "); 
	 } 
	 document.writeln("<br/>"); 
	 } 
</script>
```

##### 排序数组

```javascript
var fruits = ['banana','apple','orange','strawberry'];
console.log(fruits.sort());//Array [ "apple", "banana", "orange", "strawberry" ]
var num = [32,43,2,5,-23,0,4];
console.log(num.sort());//Array [ -23, 0, 2, 32, 4, 43, 5 ]
//Array对象的sort方法会按照字母顺序来排序数组元素。对于数字，是按照字符编码的顺序进行排序
function compare(a,b){
    return a-b;
}
var num = [32,43,2,5,-23,0,4];
console.log(num.sort(compare));//Array [ -23, 0, 2, 4, 5, 32, 43 ] 
```

### js判断传入参数是否为质数

```javascript
function fn(input) {
  input = parseInt(input,10);
  return isPrime(input) ? 'is prime' : 'not prime';
}
 
function isPrime(input) {
  if (input < 2) {
    return false;
  } else {
    for (var i = 2; i <= Math.sqrt(input); i++) {
      if (input % i == 0) {
        return false;
      }
    }
  }
  return true;
}
```

### js判断字符串出现最多的字符，并统计次数

```javascript
//js实现一个函数，来判断一个字符串出现次数最多的字符，并统计这个次数
function countStr(str){
    var obj = {};
    for(var i = 0, l = str.length,k; i < l ;i++){ k = str.charAt(i); if(obj[k]){ obj[k]++; }else{ obj[k] = 1; } } var m = 0,i=null; for(var k in obj){ if(obj[k] > m){
            m = obj[k];
            i = k;
        }
    }
    return i + ':' + m;
}
```

### 阻止表单重复提交

```javascript
//有两种方法可以解决：一是提交之后，立刻禁用点击按钮；第二种就是提交之后取消后续的表单提交操作。
document.getElementById("btn").disabled = true;//第一次提交后，将按钮禁用
//这种方式只能用于通过提交按钮防止重复提交，还可以使用如下方式：
var flag = false;//设置一个监听变量
if(flag ==true)return;//退出事件
flag = true;//表示提交过一次了
```

### getBoundingClientRect() 获取元素位置

```javascript
//它返回一个对象，其中包含了left、right、top、bottom四个属性
var myDiv = document.getElementById('myDiv');
var x = myDiv.getBoundingClientRect().left; 
var y = myDiv.getBoundingClientRect().top; 
```

### html5全屏

```javascript
function fullscreen(element) {
    if (element.requestFullscreen) {
        element.requestFullscreen();
    } else if (element.mozRequestFullScreen) {
        element.mozRequestFullScreen();
    } else if (element.webkitRequestFullscreen) {
        element.webkitRequestFullscreen();
    } else if (element.msRequestFullscreen) {
        element.msRequestFullscreen();
    }
}
fullscreen(document.documentElement);
```

### 禁止右键或者f12查看源代码

```javascript
function click(e) {
	if (document.all) {
		if (event.button==2||event.button==3) { 
			oncontextmenu='return false';
		}
	}
	if (document.layers) {
		if (e.which == 3) {
			oncontextmenu='return false';
		}
	}
}
if (document.layers) {
	document.captureEvents(Event.MOUSEDOWN);
}
document.onmousedown=click;
document.oncontextmenu = new Function("return false;")
document.onkeydown =document.onkeyup = document.onkeypress=function(){ 
	if(window.event.keyCode == 123) { 
		window.event.returnValue=false;
		return(false); 
	} 
}
```