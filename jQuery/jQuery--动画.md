### 动画基础隐藏和显示
1. jQuery中隐藏元素的hide方法

	```
	.hide( options )
	当提供hide方法一个参数时，.hide()就会成为一个动画方法。
	.hide()方法将会匹配元素的宽度，高度，以及不透明度，同时进行动画操作
	快捷参数：
	.hide("fast / slow")
	这是一个动画设置的快捷方式，'fast' 和 'slow' 分别代表200和600毫秒的延时，就是元素会执行200/600毫秒的动画后再隐藏
	注意：
	jQuery在做hide操作的时候，是会保存本身的元素的原始属性值，再之后通过对应的方法还原的时候还是初始值。
	比如一个元素的display属性值为inline，那么隐藏再显示时，这个元素将再次显示inline。
	一旦透明度 达到0，display样式属性将被设置为none，这个元素将不再在页面中影响布局
	```
	```html
	<body>
	    <h2>hide</h2>
	    <div class="left">
	        <h4>测试一</h4>
	        <div id="a1">hide操作</div> 
	        <button>直接hide</button>
	        <script type="text/javascript">
	        //点击buttom1 直接隐藏
	        $("button:first").click(function() {
	            $("#a1").hide()
	        });
	        </script>
	        <h4>测试一</h4>
	        <div id="a2">hide动画操作</div>
	        <button>hide带动画</button>
	        <script type="text/javascript">
	        //点击buttom2 执行动画隐藏
	        $("button:last").click(function() {
	            $("#a2").hide({
	                duration: 3000,
	                complete: function() {
	                    alert('执行3000ms动画完毕')
	                }
	            })
	        });
	        </script>
	    </div>
	</body>
	```
	
2. jQuery中显示元素的show方法

	```
	$('elem').hide(3000).show(3000)
	让元素执行3秒的隐藏动画，然后执行3秒的显示动画。
	注意事项：
	1. show与hide方法是修改的display属性，通过是visibility属性布局需要通过css方法单独设置
	2. 如果使用!important在你的样式中，比如display: none !important，如果你希望.show()方法正常工作，必须使用.css('display', 'block !important')重写样式
	3. 如果让show与hide成为一个动画，那么默认执行动画会改变元素的高度，高度，透明度
	```
	```html
	<body> 
	    <h2>hide-show</h2>
	    <div class="left">
	        <div id="a1">hide-show</div>
	        <button>直接hide-show动画</button>
	    </div>
	    <script type="text/javascript">
	    //点击button
	    //执行3秒隐藏
	    //执行3秒显示
	    $("button").click(function() {
	        $("#a1").hide(3000).show(3000)
	    });
	    </script>
	</body>
	```
	
3. jQuery中显示与隐藏切换toggle方法

	```
	基本的操作：toggle();
	这是最基本的操作，处理元素显示或者隐藏，因为不带参数，所以没有动画。通过改变CSS的display属性，匹配的元素将被立即显示或隐藏，没有动画。
	如果元素是最初显示，它会被隐藏
	如果隐藏的，它会显示出来
	display属性将被储存并且需要的时候可以恢复。如果一个元素的display值为inline，然后是隐藏和显示，这个元素将再次显示inline
	提供参数：.toggle( [duration ] [, complete ] )
	同样的提供了时间、还有动画结束的回调。在参数对应的时间内，元素会发生显示/隐藏的改变，在改变的过程中会把元素的高、宽、不透明度进行一系列动画效果。这个元素其实就是show与hide的方法
	直接定位：.toggle(display)
	直接提供一个参数，指定要改变的元素的最终效果
	其实就是确定是使用show还是hide方法
	if ( display === true ) {
	  $( "elem" ).show();
	} else if ( display === false ) {
	  $( "elem" ).hide();
	}
	```
	```html
	<body>
	    <h2>通过toggle切换显示与隐藏</h2> 
	    <div class="left">显示到隐藏</div>
	    <div class="right">隐藏到显示</div>
	    <button>直接show-hide动画</button>
	    <button>直接hide-show动画</button>
	    <script type="text/javascript">
	    $("button:first").click(function() {
	        $(".left").toggle(3000)
	    });
	    </script>
	    <script type="text/javascript">
	    $("button:last").click(function() {
	        $(".right").toggle(3000)
	    });
	    </script>
	</body>
	```
	
### 上卷下拉效果

1. 下拉动画slideDown

	```
	.slideDown()：用滑动动画显示一个匹配元素
	.slideDown()方法将给匹配元素的高度的动画，这会导致页面的下面部分滑下去，弥补了显示的方式
	.slideDown( [duration ] [, complete ] )
	持续时间（duration）是以毫秒为单位的，数值越大，动画越慢，不是越快。字符串 'fast' 和 'slow' 分别代表200和600毫秒的延时。如果提供任何其他字符串，或者这个duration参数被省略，那么默认使用400 毫秒的延时。
	具体使用：
	$("ele").slideDown(1000, function() {
	    //等待动画执行1秒后,执行别的动作....
	});
	注意事项：
	1. 下拉动画是从无到有，所以一开始元素是需要先隐藏起来的，可以设置display:none
	2. 如 果提供回调函数参数，callback会在动画完成的时候调用。将不同的动画串联在一起按顺序排列执行是非常有用的。
	这个回调函数不设置任何参数，但是 this会设成将要执行动画的那个DOM元素，如果多个元素一起做动画效果，那么要非常注意，
	回调函数会在每一个元素执行完动画后都执行一次，而不是这组 动画整体才执行一次
	```
	
2. 上卷动画slideUp

	```
	$("elem").slideUp();
	这个使用的含义就是：找到元素的高度，然后采用一个下滑动画让元素一直滑到隐藏，
	当高度为0的时候，也就是不可见的时，修改元素display 样式属性被设置为none。
	带参数：
	.slideUp( [duration ] [, easing ] [, complete ] )
	同样可以提供一个时间，然后可以使用一种过渡使用哪种缓动函数，jQuery默认就2种，可以通过下载插件支持。最后一个动画结束的回调方法。
	因为动画是异步的，所以要在动画之后执行某些操作就必须要写到回调函数里面，这里要特别注意
	```
	
3. 上卷下拉切换slideToggle

	```
	基本的操作：slideToggle();
	这是最基本的操作，获取元素的高度，使这个元素的高度发生改变，从而让元素里的内容往下或往上滑。
	提供参数：.slideToggle( [duration ] ,[ complete ] )
	同样的提供了时间、还有动画结束的回调。在参数对应的时间内，元素会完成动画，然后出发回调函数
	同时也提供了时间的快速定义，字符串 'fast' 和 'slow' 分别代表200和600毫秒的延时
	slideToggle("fast") 
	slideToggle("slow") 
	注意：
	1. display属性值保存在jQuery的数据缓存中，所以display可以方便以后可以恢复到其初始值
	2. 当一个隐藏动画后，高度值达到0的时候，display 样式属性被设置为none，以确保该元素不再影响页面布局
	```
	
### 淡入淡出效果

1. 淡出动画fadeOut

	```
	fadeOut()函数用于隐藏所有匹配的元素，并带有淡出的过渡动画效果
	所谓"淡出"隐藏的，元素是隐藏状态不对作任何改变，元素是可见的，则将其隐藏。
	.fadeOut( [duration ], [ complete ] )
	通过不透明度的变化来实现所有匹配元素的淡出效果，并在动画完成后可选地触发一个回调函数。
	这个动画只调整元素的不透明度，也就是说所有匹配的元素的高度和宽度不会发生变化。
	```
	
2. 淡入动画fadeIn

	```
	fadeOut是淡出效果，相反的还有淡入效果fadeIn,方法使用上两者都是一致的，只是结果相反
	.fadeIn( [duration ], [ complete ] )
	1. duration：指定过渡动画运行多长时间(毫秒数)，默认值为400。该参数也可以为字符串"fast"(=200)或"slow"(=600)。
	2. 元素显示完毕后需要执行的函数。函数内的this指向当前DOM元素。
	fadeIn()函数用于显示所有匹配的元素，并带有淡入的过渡动画效果。
	注意：
	1. 淡入的动画原理：操作元素的不透明度从0%逐渐增加到100%
	2. 如果元素本身是可见的，不对其作任何改变。如果元素是隐藏的，则使其可见
	```
	
3. 淡入淡出切换fadeToggle

	```
	fadeToggle()函数用于切换所有匹配的元素，并带有淡入/淡出的过渡动画效果。
	fadeToggle切换fadeOut与fadeIn效果，所谓"切换"，即如果元素当前是可见的，则将其隐藏(淡出)；如果元素当前是隐藏的，则使其显示(淡入)。
	
	常用语法：.fadeToggle( [duration ] ,[ complete ] )
	
	可选的 duration 参数规定效果的时长。它可以取以下值："slow"、"fast" 或毫秒。 可选的 callback 参数是 fadeToggle完成后所执行的函数名称。
	
	fadeToggle() 方法可以在 fadeIn() 与 fadeOut() 方法之间进行切换。如果元素已淡出，则 fadeToggle() 会向元素添加淡入效果。
	如果元素已淡入，则 fadeToggle() 会向元素添加淡出效果。
	```
	
4. 淡入效果fadeTo

	```
	淡入淡出fadeIn与fadeOut都是修改元素样式的opacity属性，但是他们都有个共同的特点，变化的区间要么是0，要么是1
	1. fadeIn：淡入效果，内容显示，opacity是0到1
	2. fadeOut：淡出效果，内容隐藏，opacity是1到0
	
	语法:
	.fadeTo( duration, opacity ,callback)
	
	必需的 duration参数规定效果的时长。它可以取以下值："slow"、"fast" 或毫秒。fadeTo() 方法中必需的 opacity 参数将淡入淡出效果设置为给定的不透明度（值介于 0 与 1 之间）。可选的 callback 参数是该函数完成后所执行的函数名称。
	```
	
5. 动画切换的比较


	<table>
		<tr>
			<td colspan = "3">toggle、sildeToggle以及fadeToggle的区别</td>
		</tr>
		<tr>
			<td>toggle：切换显示与隐藏效果</td>
			<td>sildeToggle：切换上下拉卷滚效果</td>
			<td>fadeToggle：切换淡入淡出效果</td>
		</tr>
		<tr>
			<td colspan = "3">toggle与slideToggle细节区别</td>
		</tr>
		<tr>
			<td>toggle：动态效果为从右至左。横向动作，toggle通过display来判断切换所有匹配元素的可见性</td>
			<td>slideToggle：动态效果从下至上。竖向动作，slideToggle 通过高度变化来切换所有匹配元素的可见性</td>
			<td></td>
		</tr>
		<tr>
			<td colspan = "3">fadeToggle方法</td>
		</tr>
		<tr>
			<td>fadeToggle() 方法在 fadeIn() 和 fadeOut() 方法之间切换。</td>
			<td>元素是淡出显示的，fadeToggle() 会使用淡入效果显示它们。</td>
			<td>元素是淡入显示的，fadeToggle() 会使用淡出效果显示它们</td>
		</tr>
	</table>
	
### 自定义动画

1. animate

	```
	语法：
	.animate( properties ,[ duration ], [ easing ], [ complete ] )
	
	参数分解：
	1. properties：一个或多个css属性的键值对所构成的Object对象。
	2. duration时间： 动画执行的时间，持续时间是以毫秒为单位的；值越大表示动画执行的越慢，不是越快。还可以提供'fast' 和 'slow'字符串，分别表示持续时间为200 和 600毫秒。
	3. easing动画运动的算法： jQuery库中默认调用 swing。如果需要其他的动画算法，请查找相关的插件
	4. complete回调： 动画完成时执行的函数，这个可以保证当前动画确定完成后发会触发
	
	.animate({
	    left: 50, 
	    width: '50px'   
	    opacity: 'show',  
	    fontSize: "10em",
	}, 500);
	
	.animate( properties, options )
	options参数:
	1. duration - 设置动画执行的时间
	2. easing - 规定要使用的 easing 函数，过渡使用哪种缓动函数
	3. step：规定每个动画的每一步完成之后要执行的函数
	4. progress：每一次动画调用的时候会执行这个回调，就是一个进度的概念
	5. complete：动画完成回调
	
	$('#elem').animate({
	    width: 'toggle',  
	    height: 'toggle'
	  }, {
	    duration: 5000,
	    specialEasing: {
	      width: 'linear',
	      height: 'easeOutBounce'
	    },
	    complete: function() {
	      $(this).after('<div>Animation complete.</div>');
	    }
	  });
	```
	
2. 停止动画stop

	```
	语法：
	.stop( [clearQueue ], [ jumpToEnd ] )
	.stop( [queue ], [ clearQueue ] ,[ jumpToEnd ] )
	stop可选的参数:
	1. .stop(); 停止当前动画，点击在暂停处继续开始
	2. .stop(true); 如果同一元素调用多个动画方法，尚未被执行的动画被放置在元素的效果队列中。这些动画不会开始，直到第一个完成。当调用.stop()的时候，队列中的下一个动画立即开始。如果clearQueue参数提供true值,那么在队列中的动画其余被删除并永远不会运行
	3. .stop(true,true); 当前动画将停止，但该元素上的 CSS 属性会被立刻修改成动画的目标值
	eg:
	$("#aaron").animate({
	    height: 300
	}, 5000)
	$("#aaron").animate({
	    width: 300
	}, 5000)
	$("#aaron").animate({
	    opacity: 0.6
	}, 2000)
	1. stop()：只会停止第一个动画，第二个第三个继续
	2. stop(true)：停止第一个、第二个和第三个动画
	3. stop(true ture)：停止动画，直接跳到第一个动画的最终状态 
	```

### jQuery核心

1. each方法的应用

	```
	.each只是处理jQuery对象的方法，jQuery还提供了一个通用的jQuery.each方法，用来处理对象和数组的遍历
	语法:
	jQuery.each(array, callback )
	jQuery.each( object, callback )
	第一个参数传递的就是一个对象或者数组，第二个是回调函数
	$.each(["Aaron", "慕课网"], function(index, value) {
	   //index是索引,也就是数组的索引
	   //value就是数组中的值了
	});
	
	jQuery.each()函数还会根据每次调用函数callback的返回值来决定后续动作。
	如果返回值为false，则停止循环(相当于普通循环中的break)；
	如果返回其他任何值，均表示继续执行下一个循环。
	$.each(["Aaron", "慕课网"], function(index, value) {
	    return false; //停止迭代
	});
	```
	
2. 查找数组中的索引inArray

	```
	语法：
	jQuery.inArray( value, array ,[ fromIndex ] )
	用法非常简单，传递一个检测的目标值，然后传递原始的数组，可以通过fromIndex规定查找的起始值，默认数组是0开始
	例如：在数组中查找值是5的索引
	$.inArray(5,[1,2,3,4,5,6,7]) //返回对应的索引：4
	注意：
	如果要判断数组中是否存在指定值，你需要通过该函数的返回值不等于(或大于)-1来进行判断
	```
	
3. 去空格.trim()方法

	```
	jQuery.trim()函数用于去除字符串两端的空白字符
	```
	
4. DOM元素的获取get方法

	```
	语法：
	.get( [index ] )
	注意2点
	1. get方法是获取的dom对象，也就是通过document.getElementById获取的对象
	2. get方法是从0开始索引
	所以第二个a元素的查找： $(a).get(1)
	负索引值参数
	get方法还可以从后往前索引，传递一个负索引值，注意的负值的索引起始值是-1
	同样是找到第二元素，可以传递 $(a).get(-2) 
	```
	
5. DOM元素的获取index方法

	```
	语法：参数接受一个jQuery或者dom对象作为查找的条件
	.index()
	.index( selector )
	.index( element )
	1. 如果不传递任何参数给 .index() 方法，则返回值就是jQuery对象中第一个元素相对于它同辈元素的位置
	2. 如果在一组元素上调用 .index() ，并且参数是一个DOM元素或jQuery对象， .index() 返回值就是传入的元素相对于原先集合的位置
	3. 如果参数是一个选择器， .index() 返回值就是原先元素相对于选择器匹配元素的位置。如果找不到匹配的元素，则 .index() 返回 -1
	```