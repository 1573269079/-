###检测IE浏览器

```javascript
$(document).ready(function() { 
	if (navigator.userAgent.match(/msie/i) ){ 
		alert('I am an old fashioned Internet Explorer'); 
	} 
}); 
```

### 平滑滚动至页面顶部

```javascript
//以下是jQuery最为常见的一种实现效果：点击一条链接以平滑滚动至页面顶部。
$("a[href='#top']").click(function() { 
  $("html, body").animate({ scrollTop: 0 }, "slow"); 
  return false; 
}); 
```

### 保持始终处于顶部

```javascript
//以下代码片段允许某一元素始终处于页面顶部。可以想见，其非常适合处理导航菜单、工具栏或者其它重要信息。
$(function(){ 
	var $win = $(window) 
	var $nav = $('.mytoolbar');  
	var navTop = $('.mytoolbar').length && $('.mytoolbar').offset().top;  
	var isFixed=0;  
	processScroll()  
	$win.on('scroll', processScroll)  
	function processScroll() {  
		var i, scrollTop = $win.scrollTop() 
		if (scrollTop >= navTop && !isFixed) {  
		isFixed = 1 
		$nav.addClass('subnav-fixed') 
	} else if (scrollTop <= navTop && isFixed) {  
		isFixed = 0 
		$nav.removeClass('subnav-fixed')  
	} 
} 
```

### 替换html标签

```javascript
//jQuery能够非常轻松地实现html标签替换。
$('li').replaceWith(function(){ 
  return $("<div />").append($(this).contents()); 
}); 
```

### 检测屏幕宽度

```javascript
var responsive_viewport = $(window).width(); 
/* if is below 481px */
if (responsive_viewport < 481) { 
    alert('Viewport is smaller than 481px.'); 
} /* end smallest screen */
```

### 自动修复损坏图片

```javascript
//检测损坏图片并根据我们的选择加以替换。
$('img').error(function(){ 
	$(this).attr('src', 'img/broken.png'); 
}); 
```

### 检测复制、粘贴与剪切操作

```javascript
$("#textA").bind('copy', function() { 
    $('span').text('copy behaviour detected!') 
}); 
$("#textA").bind('paste', function() { 
    $('span').text('paste behaviour detected!') 
}); 
$("#textA").bind('cut', function() { 
    $('span').text('cut behaviour detected!') 
}); 
```

### 自动为外部链接添加target=“blank”属性

```javascript
var root = location.protocol + '//' + location.host; 
$('a').not(':contains(root)').click(function(){ 
    this.target = "_blank"; 
}); 
```

### 悬停时淡入/淡出

```javascript
$(document).ready(function(){ 
    $(".thumbs img").fadeTo("slow", 0.6); // This sets the opacity of the thumbs to fade down to 60% when the page loads 
  	$(".thumbs img").hover(function(){ 
        $(this).fadeTo("slow", 1.0); // This should set the opacity to 100% on hover 
   },function(){ 
        $(this).fadeTo("slow", 0.6); // This should set the opacity back to 60% on mouseout 
	}); 
}); 
```

### 禁用文本/密码输入中的空格

```javascript
$('input.nospace').keydown(function(e) { 
	if (e.keyCode == 32) { 
		return false; 
	} 
}); 
```