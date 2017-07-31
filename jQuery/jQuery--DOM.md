1. jQuery节点创建与属性的处理

	#### 创建元素节点：
	
	直接把这个节点的结构给通过HTML标记字符串描述出来，通过$()函数处理，$("html结构"):`$("<div></div>")`
	
	#### 创建为本节点：
	与创建元素节点类似，可以直接把文本内容一并描述:`$("<div>我是文本节点</div>")`
	
	#### 创建为属性节点：
	与创建元素节点同样的方式:`$("<div id='test' class='aaron'>我是文本节点</div>")`
	
2. DOM内部插入append()与appendTo()

	<table>
		<tr>
			<th>选择器</th>
			<th>描述</th>
		</tr>
		<tr>
			<td>append(content)</td>
			<td>向每个匹配的元素内部追加内容</td>
		</tr>
		<tr>
			<td>appendTo(content)</td>
			<td>把所有匹配的元素追加到另一个，指定的元素集合中</td>
		</tr>
	</table>
	
	append：这个操作与对指定的元素执行原生的appendChild方法，将它们添加到文档中的情况类似。
	
	appendTo：实际上，使用这个方法是颠倒了常规的$(A).append(B)的操作，即不是把B追加到A中，而是把A追加到B中。
	
	简单的总结就是：
	.append()和.appendTo()两种方法功能相同，主要的不同是语法——内容和目标的位置不同
	
	<b>
		1. append()前面是被插入的对象，后面是要在对象内插入的元素内容<br>
		2. appendTo()前面是要插入的元素内容，而后面是被插入的对象
	</b>
	
3. DOM外部插入after()与before()

	<table>
		<tr>
			<th>选择器</th>
			<th>描述</th>
		</tr>
		<tr>
			<td>.after(content)</td>
			<td>在匹配元素集合中的每个元素后面插入参数所指定的内容，作为其兄弟节点</td>
		</tr>
		<tr>
			<td>.before(content)</td>
			<td>据参数设定，在匹配元素的前面插入内容</td>
		</tr>
		<tr>
			<td colspan="2">before与after都是用来对相对选中元素外部增加相邻的兄弟节点</td>
		</tr>
		<tr>
			<td colspan="2">2个方法都是都可以接收HTML字符串，DOM 元素，元素数组，或者jQuery对象，用来插入到集合中每个匹配元素的前面或者后面</td>
		</tr>
		<tr>
			<td colspan="2">2个方法都支持多个参数传递after(div1,div2,....)</td>
		</tr>
		<tr>
			<td colspan="2">after向元素的后边添加html代码，如果元素后面有元素了，那将后面的元素后移，然后将html代码插入</td>
		</tr>
		<tr>
			<td colspan="2">before向元素的前边添加html代码，如果元素前面有元素了，那将前面的元素前移，然后将html代码插</td>
		</tr>
	</table>
	
4. DOM内部插入prepend()与prependTo()

	<table>
		<tr>
			<th>选择器</th>
			<th>描述</th>
		</tr>
		<tr>
			<td>prepend()</td>
			<td>向每个匹配的元素内部牵制内容</td>
		</tr>
		<tr>
			<td>prependTo()</td>
			<td>把所有匹配的元素前置到另一个指定的元素集合中</td>
		</tr>
		<tr>
			<td colspan="2">.prepend()方法将指定元素插入到匹配元素里面作为它的第一个子元素 (如果要作为最后一个子元素插入用.append()).</td>
		</tr>
		<tr>
			<td colspan="2">.prepend()和.prependTo()实现同样的功能，主要的不同是语法，插入的内容和目标的位置不同</td>
		</tr>
		<tr>
			<td colspan="2">对于.prepend() 而言，选择器表达式写在方法的前面，作为待插入内容的容器，将要被插入的内容作为方法的参数</td>
		</tr>
		<tr>
			<td colspan="2">而.prependTo() 正好相反，将要被插入的内容写在方法的前面，可以是选择器表达式或动态创建的标记，待插入内容的容器作为参数。</td>
		</tr>
	</table>
	<table>
		<tr>
			<th>append()</th>
			<th>prepend()</th>
			<th>appendTo()</th>
			<th>prependTo()</th>
		</tr>
		<tr>
			<td>向每个匹配的元素内部追加内容</td>
			<td>向每个匹配的元素内部前置内容</td>
			<td>把所有匹配的元素追加到另一个指定元素的集合中</td>
			<td>把所有匹配的元素前置到另一个指定的元素集合中</td>
		</tr>
	</table>

5. DOM外部插入insertAfter()与insertBefore()

	<table>
		<tr>
			<th>选择器</th>
			<th>描述</th>
		</tr>
		<tr>
			<td>insertAfter()</td>
			<td>在目标元素前面插入集合中每个匹配的元素</td>
		</tr>
		<tr>
			<td>insertBefore()</td>
			<td>在目标元素后面插入集合中每个匹配的元素</td>
		</tr>
		<tr>
			<td colspan="2">.before()和.insertBefore()实现同样的功能。主要的区别是语法——内容和目标的位置。 对于before()选择表达式在函数前面，内容作为参数，而.insertBefore()刚好相反，内容在方法前面，它将被放在参数里元素的前面</td>
		</tr>
		<tr>
			<td colspan="2">..after()和.insertAfter() 实现同样的功能。主要的不同是语法——特别是（插入）内容和目标的位置。 对于after()选择表达式在函数的前面，参数是将要插入的内容。对于 .insertAfter(), 刚好相反，内容在方法前面，它将被放在参数里元素的后面</td>
		</tr>
		<tr>
			<td colspan="2">before、after与insertBefore。insertAfter的除了目标与位置的不同外，后面的不支持多参数处理</td>
		</tr>
		<tr>
			<td colspan="2">insertAfter将JQuery封装好的元素插入到指定元素的后面，如果元素后面有元素了，那将后面的元素后移，然后将JQuery对象插入；</td>
		</tr>
		<tr>
			<td colspan="2">insertBefore将JQuery封装好的元素插入到指定元素的前面，如果元素前面有元素了，那将前面的元素前移，然后将JQuery对象插入；</td>
		</tr>
	</table>

6. DOM节点删除之empty()的基本用法

	```
	empty 顾名思义，清空方法，但是与删除又有点不一样，因为它只移除了 指定元素中的所有子节点。
	这个方法不仅移除子元素（和其他后代元素），同样移除元素里的文本。元素里任何文本字符串都被看做是该元素的子节点。
	通过empty移除了当前div元素下的所有p元素,但是本身id=test的div元素没有被删除
	```
	
7. DOM节点删除之remove()的有参用法和无参用法

	```
	1. remove与empty一样，都是移除元素的方法，但是remove会将元素自身移除，同时也会移除元素内部的一切，包括绑定的事件及与该元素相关的jQuery数据。
	2. remove表达式参数：
	   remove比empty好用的地方就是可以传递一个选择器表达式用来过滤将被移除的匹配元素集合，可以选择性的删除指定的节点
	```
	
	<table>
		<tr>
			<th>empty</th>
			<th>remove</th>
		</tr>
		<tr>
			<td>empty()方法并不是删除节点，而是清空节点，它能清空元素中的所有后代节点</td>
			<td>该节点与该节点所包含的所有后代节点将同时被删除</td>
		</tr>
		<tr>
			<td>empty不能删除自己本身这个节点</td>
			<td>提供传递一个筛选的表达式，删除指定合集中的元素</td>
		</tr>
	</table>
	
8. DOM节点删除之保留数据的删除操作detach()

	```html
	//这个方法不会把匹配的元素从jQuery对象中删除，因而可以在将来再使用这些匹配的元素。与remove()不同的是，所有绑定的事件、附加的数据等都会保留下来。
	//$("div").detach()这一句会移除对象，仅仅是显示效果没有了。但是内存中还是存在的。当你append之后，又重新回到了文档流中。就又显示出来了。
	<body>
	    <p>P元素1，默认给绑定一个点击事件</p>
	    <p>P元素2，默认给绑定一个点击事件</p>
	    <button id="bt1">点击删除 p 元素</button>
	    <button id="bt2">点击移动 p 元素</button>
	    <script type="text/javascript"> 
	    var p;
	    $("#bt1").click(function() {
	        if (!$("p").length) return; //去重
	        //通过detach方法删除元素
	        //只是页面不可见，但是这个节点还是保存在内存中
	        //数据与事件都不会丢失
	        p = $("p").detach()
	    });
	    $("#bt2").click(function() {
	        //把p元素在添加到页面中
	        //事件还是存在
	        $("body").append(p);
	    });
	    </script>
	</body>
	```
	
9. DOM节点删除之detach()和remove()区别

	<table>
		<tr>
			<th>方法名</th>
			<th>参数</th>
			<th>事件及数据是否被移除</th>
			<th>元素自身是否被移除</th>
		</tr>
		<tr>
			<td>remove</td>
			<td>支持选择器表达</td>
			<td>是</td>
			<td>是（无参数时），有参数是要根据参数所涉及的范围</td>
		</tr>
		<tr>
			<td>detach</td>
			<td>支持选择器表达</td>
			<td>否</td>
			<td>是（无参数时），有参数是要根据参数所涉及的范围</td>
		</tr>
		<tr>
			<td colspan="4">remove：移除节点</td>
		</tr>
		<tr>
			<td colspan="4">无参数，移除自身整个节点以及该节点的内部的所有节点，包括节点上事件与数据</td>
		</tr>
		<tr>
			<td colspan="4">有参数，移除筛选出的节点以及该节点的内部的所有节点，包括节点上事件与数据</td>
		</tr>
		<tr>
			<td colspan="4">detach：移除节点</td>
		</tr>
		<tr>
			<td colspan="4">移除的处理与remove一致</td>
		</tr>
		<tr>
			<td colspan="4">与remove()不同的是，所有绑定的事件、附加的数据等都会保留下来</td>
		</tr>
		<tr>
			<td colspan="4">例如：$("p").detach()这一句会移除对象，仅仅是显示效果没有了。但是内存中还是存在的。当你append之后，又重新回到了文档流中。就又显示出来了。</td>
		</tr>
	</table>

10. DOM拷贝clone()

	```javascript
	//1、.clone()方法深度 复制所有匹配的元素集合，包括所有匹配元素、匹配元素的下级元素、文字节点。
	//2、 clone方法比较简单就是克隆节点，如果节点有事件或者数据之类的其他处理，我们需要通过clone(ture)传递一个布尔值ture用来指定，这样不仅仅只是克隆单纯的节点结构，还要把附带的事件与数据给一并克隆了
	$("div").on('click', function() {//执行操作})
	//clone处理一
	$("div").clone()   //只克隆了结构，事件丢失
	//clone处理二
	$("div").clone(true) //结构、事件与数据都克隆
	```
	
	* clone()方法时，在将它插入到文档之前，我们可以修改克隆后的元素或者元素内容，如 $(this).clone().css('color','red') 增加一个颜色
	* 通过传递true，将所有绑定在原始元素上的事件处理函数复制到克隆元素上
    * clone()方法是jQuery扩展的，只能处理通过jQuery绑定的事件与数据
    * 元素数据（data）内对象和数组不会被复制，将继续被克隆元素和原始元素共享。深复制的所有数据，需要手动复制每一个

11. DOM替换replaceWith()和replaceAll()

	```
	.replaceWith( newContent )：用提供的内容替换集合中所有匹配的元素并且返回被删除元素的集合,用$()选择节点A，调用replaceWith方法，传入一个新的内容B（HTML字符串，DOM元素，或者jQuery对象）用来替换选中的节点A
	.replaceAll( target ) ：用集合的匹配元素替换每个目标元素,.replaceAll()和.replaceWith()功能类似，但是目标和源相反，用上述的HTML结构，我们用replaceAll处理
	
	.replaceAll()和.replaceWith()功能类似，主要是目标和源的位置区别
	.replaceWith()与.replaceAll() 方法会删除与节点相关联的所有数据和事件处理程序
	.replaceWith()方法，和大部分其他jQuery方法一样，返回jQuery对象，所以可以和其他方法链接使用
	.replaceWith()方法返回的jQuery对象引用的是替换前的节点，而不是通过replaceWith/replaceAll方法替换后的节点
	```
	
12. DOM包裹wrap()方法

	```html
	<!-- .wrap( wrappingElement )：在集合中匹配的每个元素周围包裹一个HTML结构-->
	<p>p元素</p>
	<!--给p元素增加一个div包裹-->
	<script>
	$('p').wrap('<div></div>')
	</script>
	<!--最后的结构，p元素增加了一个父div的结构-->
	<div>
	    <p>p元素</p>
	</div>
	<!--.wrap( function ) ：一个回调函数，返回用于包裹匹配元素的 HTML 内容或 jQuery 对象,使用后的效果与直接传递参数是一样，只不过可以把代码写在函数体内部，写法不同而已-->
	<script>
	$('p').wrap(function() {
	    return '<div></div>';   //与第一种类似，只是写法不一样
	})
	</script>
	```
	
13. DOM包裹unwrap()方法

	```html
	<!--jQuery提供了一个unwrap()方法 ，作用与wrap方法是相反的。将匹配元素集合的父级元素删除，保留自身（和兄弟元素，如果存在）在原来的位置。-->
	<div>
    	<p>p元素</p>
	</div>
	<script>
		$('p').unwrap();
	</script>
	<!--找到p元素，然后调用unwrap方法，这样只会删除父辈div元素了-->
	<p>p元素</p>
	```
	
14. DOM包裹wrapAll()方法

	```html
	<!-- .wrapAll( wrappingElement )：给集合中匹配的元素增加一个外面包裹HTML结构-->
	<p>p元素</p>
	<p>p元素</p>
	<!--给所有p元素增加一个div包裹-->
	<script>
		$('p').wrapAll('<div></div>')
	</script>
	<!--最后的结构，2个P元素都增加了一个父div的结构-->
	<div>
	    <p>p元素</p>
	    <p>p元素</p>
	</div>
	
	<!--.wrapAll( function ) ：一个回调函数，返回用于包裹匹配元素的 HTML 内容或 jQuery 对象
	通过回调的方式可以单独处理每一个元素-->
	<script>
		$('p').wrapAll(function() {
		    return '<div><div/>'; 
		})
	</script>
	<!--以上的写法的结果如下，等同于warp的处理了-->
	<div>
	    <p>p元素</p>
	</div>
	<div>
	    <p>p元素</p>
	</div>
	```
	
15. DOM包裹wrapInner()方法

	```html
	<!--.wrapInner( wrappingElement )：给集合中匹配的元素的内部，增加包裹的HTML结构-->
	<div>p元素</div>
	<div>p元素</div>
	<!--给所有元素增加一个p包裹-->
	<script>
		$('div').wrapInner('<p></p>')
	</script>
	<!--最后的结构，匹配的div元素的内部元素被p给包裹了-->
	<div>
	    <p>p元素</p>
	</div>
	<div>
	    <p>p元素</p>
	</div>
	<!--.wrapInner( function ) ：允许我们用一个callback函数做参数，每次遇到匹配元素时，该函数被执行，返回一个DOM元素，jQuery对象，或者HTML片段，用来包住匹配元素的内容-->
 	<script>
	 	$('div').wrapInner(function() {
		    return '<p></p>'; 
		})
	</script>
	<div>
	    <p>p元素</p>
	</div>
	<div>
	    <p>p元素</p>
	</div>
	```
	<b>当通过一个选择器字符串传递给.wrapInner() 函数，其参数应该是格式正确的 HTML，并且 HTML 标签应该是被正确关闭的。</b>
	
16. jQuery遍历之children()方法

	```html
	<div class="div">
	    <ul class="son">
	        <li class="grandson">1</li>
	    </ul>
	</div>
	<!--代码如果是$("div").children()，那么意味着只能找到ul，因为div与ul是父子关系，li与div是祖辈关系，因此无法找到。-->
	<!--注意：jQuery是一个合集对象，所以通过children是匹配合集中每一给元素的第一级子元素-->
	<script type="text/javascript">
	//因为jQuery是合集对象，可能需要对这个合集对象进行一定的筛选，找出目标元素，所以允许传一个选择器的表达式
    //找到所有class=div的元素
    //找到其对应的子元素ul，然后筛选出最后一个，给边宽加上颜色
        $('.div').children(':last').css('border', '3px solid blue')
   </script>
	```
	
17. jQuery遍历之find()方法

	* find是遍历当前元素集合中每个元素的后代。只要符合，不管是儿子辈，孙子辈都可以。
	* 与其他的树遍历方法不同，选择器表达式对于 .find() 是必需的参数。如果我们需要实现对所有后代元素的取回，可以传递通配选择器 '*'。
	* find只在后代中遍历，不包括自己。
	* 选择器 context 是由 .find() 方法实现的；因此，$('.item-ii').find('li') 等价于 $('li', '.item-ii')(找到类名为item-ii的标签下的li标签)。
	
	<b>.find()和.children()方法是相似的</b>
	* children只查找第一级的子节点
	* find查找范围包括子节点的所有后代节点
	
18. jQuery遍历之parent()方法

	* parent()方法允许我们能够在DOM树中搜索到这些元素的父级元素，从有序的向上匹配元素，并根据匹配的元素创建一个新的 jQuery 对象
		<b>注意：jQuery是一个合集对象，所以通过parent是匹配合集中每一个元素的父元素</b>
	* parent()方法选择性地接受同一型选择器表达式,因为jQuery是合集对象，可能需要对这个合集对象进行一定的筛选，找出目标元素，所以允许传一个选择器的表达式
	
19. jQuery遍历之parents()方法

	* parents()方法允许我们能够在DOM树中搜索到这些元素的祖先元素，从有序的向上匹配元素，并根据匹配的元素创建一个新的 jQuery 对象;
	* 返回的元素秩序是从离他们最近的父级元素开始的
	
	<b>注意：jQuery是一个合集对象，所以通过parent是匹配合集中所有元素的祖辈元素</b>
	* parents()方法选择性地接受同一型选择器表达式
	
20. jQuery遍历之closest()方法

	* 粗看.parents()和.closest()是有点相似的，都是往上遍历祖辈元素，但是两者还是有区别的
	* 起始位置不同：.closest开始于当前元素 .parents开始于父元素
	* 遍历的目标不同：.closest要找到指定的目标，.parents遍历到文档根元素，closest向上查找，直到找到一个匹配的就停止查找，parents一直查找到根元素，并将匹配的元素加入集合
	* 结果不同：.closest返回的是包含零个或一个元素的jquery对象，parents返回的是包含零个或一个或多个元素的jquery对象
	
21. jQuery遍历之next()方法

	* jQuery是一个合集对象，所以通过next匹配合集中每一个元素的下一个兄弟元素
	* next()方法选择性地接受同一类型选择器表达式
	
22. jQuery遍历之prev()方法

	* jQuery是一个合集对象，所以通过prev是匹配合集中每一个元素的上一个兄弟元素
	* prev()方法选择性地接受同一类型选择器表达式

23. jQuery遍历之siblings()

	* jQuery是一个合集对象，所以通过siblings是匹配合集中每一个元素的同辈元素
	* siblings()方法选择性地接受同一类型选择器表达式
	
24. jQuery遍历之add()方法

	```html
	<!--.add()的参数可以几乎接受任何的$()，包括一个jQuery选择器表达式，DOM元素，或HTML片段引用。
	操作：选择所有的li元素，之后把p元素也加入到li的合集中-->
	<ul>
	    <li>list item 1</li>
	    <li>list item 3</li>
	</ul>
	<p>新的p元素</p>
	<script>
	//处理一：传递选择器
	$('li').add('p')
	//处理二：传递dom元素
	$('li').add(document.getElementsByTagName('p')[0])
	//还有一种方式，就是动态创建P标签加入到合集，然后插入到指定的位置，但是这样就改变元素的本身的排列了
	 $('li').add('<p>新的p元素</p>').appendTo(目标位置)
	</script>
	```
	
25. jQuery遍历之each()

	```
	1. each是一个for循环的包装迭代器
	2. each通过回调的方式处理，并且会有2个固定的实参，索引与元素
	3. each回调方法中的this指向当前迭代的dom元素
	eg:
	<ul>
	    <li>egegegege</li>
	    <li>Aaron</li>
	</ul>
	开始迭代li，循环2次
	$("li").each(function(index, element) {
	     index 索引 0,1
	     element是对应的li节点 li,li
	     this 指向的是li
	})
	这样可以在循环体会做一些逻辑操作了，如果需要提前退出，可以以通过返回 false以便在回调函数内中止循
	```