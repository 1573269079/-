## 多列等高布局实现方式

```html
<div id="container">
	<div class="left">等高布局</div>
	<div class="right">等高布局等高布局等高布局等高布局等高布局等高布局等高布局等高布局等高布局等高布局</div>
</div>
```

#### 使用正负margin与padding相冲的方式实现

```css
#container{
	width:400px;
	margin:0 auto;
	background-color:#eee;
	overflow:hidden;
}
.left,.right{
	width:200px;
	float:left;
	font-size:16px;
	line-height:24px;
	color:#333;
	padding-bottom:5000px;/*给一个足够大的padding和负margin*/
	margin-bottom:-5000px;
}
.left{background-color:pink;}
.right{background-color:yellow;}
```

#### display:flex的方式实现

```
container设置为display:flex，子元素设置为flex:1
```

#### display:table-cell实现

```
container设置为display：table，子元素设置为display:table-cell
```

#### 父容器设置背景色

```css
#container{
	width:400px;
	margin:0 auto;
	background-color:pink;
	overflow:hidden;
}
.left,.right{
	width:200px;
	float:left;
	font-size:16px;
	line-height:24px;
	color:#333;
}
.right{background-color:yellow;}
``` 

#### 父容器多重背景色--线性渐变

```css
#container{
	width:400px;
	margin:0 auto;
	background-image:linear-gradient(90deg,yellow 50%.pink 0);
	overflow:hidden;
}
.left,.right{
	width:200px;
	float:left;
	font-size:16px;
	line-height:24px;
	color:#333;
}
```

#### border实现

```css
#container{
	border-left:200px solid yellow;
	background-color:pink;
	width:200px;
	font-size:16px;
	line-height:24px;
	color:#333;
}
.left{
	width:200px;
	margin-left:-200px;
	float:left;
}
```

## 多列均匀布局

#### display:flex
#### 借助伪元素及text-align:justify

```html
<div class="container">
	<div class="justify">
		<i>1</i>
		<i>2</i>
		<i>3</i>
		<i>4</i>
		<i>5</i>
	</div>
</div>
```
```css
.justify{
	text-align:justify;
	text-align-last:justify;/*新增这一行*/
}
.justify i{
	width:24px;
	line-height:24px;
	display:inline-block;
	text-align:center;
}
```

```css
/*text-align-last兼容性不是很好，可以使用::after*/
.justify{text-align:justify;}
.justify i{
	width:24px;
	line-height:24px;
	display:inline-block;
	text-align:center;
	border-radius:50%;
}
.justify:after{
	content:"";
	display:inline-block;
	position:relative;
	width:100%;
}
```

## 列表布局边界线问题

#### margin负边距（外层设置width，overflow设置为hidden,内层设置负边距，margin-left:-1px;就可以把左侧边距隐藏）

```html
<div class="ul-container">
	<ul>
		<li>html</li>
		<li>css</li>
		<li>javascript</li>
		<li>gulp</li>
		<li>grunt</li>
		<li>sass</li>
		<li>scss</li>
		<li>less</li>
	</ul>
</div>
```

```css
ul{
	width:300px;
	margin-left:-1px;
}
li{
	float:left;
	width:99px;
	line-height:30px;
	text-align:center;
	border-left:1px solid #999;
	font-size:18px;
	margin-bottom:10px;
}
.ul-container{
	width:300px;
	margin:50px auto;
	overflow:hidden;
	background:#eee;
	padding:10px 0;
}
```

#### 使用伪类选择器

```css
/*使用伪类选择器，选择第3n个元素去掉边框*/
li:nth-child(3n){border-right:none;}
```

## css中伪元素before或after中content的特殊用法attr

#### 鼠标移上去显示tips效果

```html
<div class="tips">
	<span data-tips="鼠标移上去显示tips效果">鼠标移上去显示tips效果</span>
</div>
```
```css
.tips{margin-top:30px;}
span{
	position:relative;
	display:inline-block;
}
span:hover{
	cursor:pointer;
}
span:hover:before{
	content:attr(data-tips);
	background-color:#2085c5;
	border-radius:3px;
	color:#fff;
	padding:10px;
	position:absolute;
	left:100%;
	top:-70px;
	margin-left:8px;
	white-space:pre;
}
span:hover:after{
	content:'';
	position:absolute;
	width:0;
	height:0;
	border-right:8px solid #2085c5;
	border-bottom:8px solid transparent;
}
```

#### 制作半边文字

```htnml
<span class="tips" data-content="微">微</span>
<span class="tips" data-content="信">信</span>
<span class="tips" data-content="前">前</span>
<span class="tips" data-content="端">端</span>
```
```css
.tips{
	position:relative;
	display:inline-block;
	font-size:60px;/*任何宽度*/
	color:black;/*任何颜色*/
	overflow:hidden;
	white-space:pre;/*处理空格*/
}
.tips:before{
	display:block;
	z-index:1;
	position:absolute;
	top:0;
	left:0;
	width:50%;
	content:attr(data-content);/*伪元素动态获取内容*/
	overflow:hidden;
	color:#f00;
}
```