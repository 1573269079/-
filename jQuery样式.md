## jQuery：轻量级的JavaScript库

### jQuery选择器

1. id选择器

	```
	id选择器：一个用来查找的ID，即元素的id属性
	$( "#id" )
	id选择器也是基本的选择器，jQuery内部使用JavaScript函数document.getElementById()来处理ID的获取。
	原生语法的支持总是非常高效的，所以在操作DOM的获取上，如果能采用id的话尽然考虑用这个选择器
	```
2. 类选择器

	```
	类选择器，顾名思义，通过class样式类名来获取节点
	描述：
	$( ".class" )
	类选择器，相对id选择器来说，效率相对会低一点，但是优势就是可以多选
	同样的jQuery在实现上，对于类选择器，如果浏览器支持，jQuery使用JavaScript的原生getElementsByClassName()函数来实现的
	```
	
3. 元素选择器
	```
	元素选择器：根据给定（html）标记名称选择所有的元素
	描述：
	$( "element" )
	搜索指定元素标签名的所有节点，这个是一个合集的操作。同样的也有原生方法getElementsByTagName()函数支持
	```
	
4. 全选择器（*选择器）

	```
	在CSS中，经常会在第一行写下这样一段样式
	* {padding: 0; margin: 0;}
	通配符*意味着给所有的元素设置默认的边距。jQuery中我们也可以通过传递*选择器来选中文档页面中的元素
	描述：
	$( "*" )
	抛开jQuery，如果要获取文档中所有的元素，通过document.getElementsByTagName()中传递"*"同样可以获取到
	不难发现，id、class、tag都可以通过原生的方法获取到对应的节点，但是我们还需要考虑一个兼容性的问题，比如:
	1. IE会将注释节点实现为元素，所以在IE中调用getElementsByTagName里面会包含注释节点，这个通常是不应该的
	2. getElementById的参数在IE8及较低的版本不区分大小写
	3. IE7及较低的版本中，表单元素中，如果表单A的name属性名用了另一个元素B的ID名并且A在B之前，那么getElementById会选中A
	4. IE8及较低的版本，浏览器不支持getElementsByClassName
	```
	
5. 层级选择器

	```
	选择器中的层级选择器:子元素 后代元素 兄弟元素 相邻元素
	```
	<table>
		<tr>
			<th>选择器</th>
			<th>描述</th>
		</tr>
		<tr>
			<td>$("parent > child")</td>
			<td>只选择器：选择所有指定“parent”元素中指定的“child”的直接子元素</td>
		</tr>
		<tr>
			<td>$("ancestor descendant")</td>
			<td>后代选择器：选择给定的祖先元素的所有后代元素，一个元素的后代可能是该元素的一个孩子，孙子，曾孙等</td>
		</tr>
		<tr>
			<td>$("prev + next")</td>
			<td>相邻兄弟选择器：选择所有紧接在“prev”元素后的“next”元素</td>
		</tr>
		<tr>
			<td>$("prev ~ siblings")</td>
			<td>一般兄弟选择器：匹配“prev”元素之后的所有兄弟元素。具有相同的父元素，并匹配过滤“siblings”选择器</td>
		</tr>
	</table>
	
	*  层级选择器都有一个参考节点
	*  后代选择器包含子选择器的选择的内容
	*  一般兄弟选择器包含相邻兄弟选择的内容
	*  相邻兄弟选择器和一般兄弟选择器所选择到的元素，必须在同一个父元素下
	
6. 筛选选择器

	```
	筛选选择器很多都不是CSS的规范，而是jQuery自己为了开发者的便利延展出来的选择器;
	筛选选择器的用法与CSS中的伪元素相似，选择器用冒号“：”开头，通过一个列表，看看基本筛选器的描述：
	```
	<table>
		<tr>
			<th>选择器</th>
			<th>描述</th>
		</tr>
		<tr>
			<td>$(":first")</td>
			<td>匹配第一个元素</td>
		</tr>
		<tr>
			<td>$(":last")</td>
			<td>匹配最后一个元素</td>
		</tr>
		<tr>
			<td>$(":not(selector)")</td>
			<td>一个用来过滤的选择器，选择所有元素去除不匹配给定的选择器元素</td>
		</tr>
		<tr>
			<td>$(":eq(index)")</td>
			<td>在匹配的集合中选择索引值为index的元素</td>
		</tr>
		<tr>
			<td>$(":gt(index)")</td>
			<td>选择匹配集合中所有大于给定index（索引值）的元素</td>
		</tr>
		<tr>
			<td>$(":even")</td>
			<td>选择索引值为偶数的元素，从0开始计数</td>
		</tr>
		<tr>
			<td>$(":odd")</td>
			<td>选择索引值为奇数的元素，从0开始计数</td>
		</tr>
		<tr>
			<td>$(":lt(index)")</td>
			<td>选择匹配集合中所有索引值小于给定index参数的元素</td>
		</tr>
		<tr>
			<td>$(":header")</td>
			<td>选择所有标题元素，eg:h1,h2,h3等</td>
		</tr>
		<tr>
			<td>$(":lang(language)")</td>
			<td>选择指定语言的所有元素</td>
		</tr>
		<tr>
			<td>$(":root")</td>
			<td>选择该文档的根元素</td>
		</tr>
		<tr>
			<td>$(":animated")</td>
			<td>选择所有正在执行动画效果的元素</td>
		</tr>
	</table>
	
	* :eq(), :lt(), :gt(), :even, :odd 用来筛选他们前面的匹配表达式的集合元素，根据之前匹配的元素在进一步筛选，注意jQuery合集都是从0开始索引
	* gt是一个段落筛选，从指定索引的下一个开始，gt(1) 实际从2开始
	
7. 内容筛选选择器

	<table>
		<tr>
			<th>选择器</th>
			<th>描述</th>
		</tr>
		<tr>
			<td>$(":contains(text)")</td>
			<td>选择所有包含指定文本的元素</td>
		</tr>
		<tr>
			<td>$(":parent")</td>
			<td>选择所有含有子元素或者文本的元素</td>
		</tr>
		<tr>
			<td>$(":empty")</td>
			<td>选择所有没有子元素的元素（包含文本节点）</td>
		</tr>
		<tr>
			<td>$(":has(selector)")</td>
			<td>选择元素中至少包含指定选择器的元素</td>
		</tr>
	</table>
	
	*  :contains与:has都有查找的意思，但是contains查找包含“指定文本”的元素，has查找包含“指定元素”的元素
	*  如果:contains匹配的文本包含在元素的子元素中，同样认为是符合条件的。
	*  :parent与:empty是相反的，两者所涉及的子元素，包括文本节点
	
8. 可见性筛选选择器

	元素有显示状态与隐藏状态，jQuery根据元素的状态扩展了可见性筛选选择器:visible与:hidden
	<table>
		<tr>
			<th>选择器</th>
			<th>描述</th>
		<tr>
		<tr>
			<td>$(":visible")</td>
			<td>选择所有显示的元素</td>
		<tr>
		<tr>
			<td>$(":hidden")</td>
			<td>选择所有隐藏的元素</td>
		<tr>
	</table>
	
	 几种方式可以隐藏一个元素：
	*  CSS display的值是none。
	*  type="hidden"的表单元素。
	*  宽度和高度都显式设置为0。
	*  一个祖先元素是隐藏的，该元素是不会在页面上显示
	*  CSS visibility的值是hidden
	*  CSS opacity的指是0
	```
	如果元素中占据文档中一定的空间,元素被认为是可见的。
	可见元素的宽度或高度，是大于零。
	元素的visibility: hidden 或 opacity: 0被认为是可见的，因为他们仍然占用空间布局。
	```
	
9. 属性筛选选择器

	属性选择器让你可以基于属性来定位一个元素。可以只指定该元素的某个属性，
	这样所有使用该属性而不管它的值，这个元素都将被定位，也可以更加明确并定位在这些属性上使用特定值的元素
	<table>
		<tr>
			<th>选择器</th>
			<th>描述</th>
		<tr>
		<tr>
			<td>$("[attribute|='value']")</td>
			<td>选择指定属性值等于给定字符串或以该文字串为前缀（该字符串后跟一个连字符‘-’）的元素</td>
		<tr>
		<tr>
			<td>$("[attribute*='value']")</td>
			<td>选择指定属性具有包含一个给定的子字符串的元素（选择给定的属性是以包含某些值得元素）</td>
		<tr>
		<tr>
			<td>$("[attribute~='value']")</td>
			<td>选择指定属性用空格分隔的值中包含一个给定值得元素</td>
		<tr>
		<tr>
			<td>$("[attribute='value']")</td>
			<td>选择指定属性是给定值得元素</td>
		<tr>
		<tr>
			<td>$("[attribute!='value']")</td>
			<td>选择不存在指定属性，或者指定属性值不等于给定值得元素</td>
		<tr>
		<tr>
			<td>$("[attribute^='value']")</td>
			<td>选择指定属性是以给定字符串开始的元素</td>
		<tr>
		<tr>
			<td>$("[attribute$='value']")</td>
			<td>选择指定属性是以给定值结尾的元素，这个比较是区分大小写的</td>
		<tr>
		<tr>
			<td>$("[attribute]")</td>
			<td>选择所有具有指定属性的元素，该属性可以使任何值</td>
		<tr>
		<tr>
			<td>$("[attributeFilter1][attributeFilterN]")</td>
			<td>选择匹配所有指定的属性筛选器的元素</td>
		<tr>
	</table>
	
10. 子元素筛选选择器

	<table>
		<tr>
			<th>选择器</th>
			<th>描述</th>
		<tr>
		<tr>
			<td>$(":first-child")</td>
			<td>选择所有父级元素下的第一个子元素</td>
		<tr>
		<tr>
			<td>$(":last-child")</td>
			<td>选择所有父级元素下的最后一个子元素</td>
		<tr>
		<tr>
			<td>$(":only-child")</td>
			<td>如果某个元素是其父元素的唯一子元素，就会被选中</td>
		<tr>
		<tr>
			<td>$(":nth-child(n)")</td>
			<td>选择父元素的第n个子元素</td>
		<tr>
		<tr>
			<td>$(":nth-last-child")</td>
			<td>选择父元素的第n个子元素，计数从最后一个元素开始到第一个</td>
		<tr>
	</table>	
	
	*  :first只匹配一个单独的元素，但是:first-child选择器可以匹配多个：即为每个父级元素匹配第一个子元素。这相当于:nth-child(1)
	*  :last 只匹配一个单独的元素， :last-child 选择器可以匹配多个元素：即，为每个父级元素匹配最后一个子元素
	*  如果子元素只有一个的话，:first-child与:last-child是同一个
	*  :only-child匹配某个元素是父元素中唯一的子元素，就是说当前子元素是父元素中唯一的元素，则匹配
	*  jQuery实现:nth-child(n)是严格来自CSS规范，所以n值是“索引”，也就是说，从1开始计数，:nth-child(index)从1开始的，而eq(index)是从0开始的
	*  nth-child(n) 与 :nth-last-child(n) 的区别前者是从前往后计算，后者从后往前计算
	
11. 表单元素选择器

	<table>
		<tr>
			<th>选择器</th>
			<th>描述</th>
		<tr>
		<tr>
			<td>$(":input")</td>
			<td>选择所有input,textarea,select和button元素</td>
		<tr>
		<tr>
			<td>$(":text")</td>
			<td>匹配所有文本框</td>
		<tr>
		<tr>
			<td>$(":password")</td>
			<td>匹配所有密码框</td>
		<tr>
		<tr>
			<td>$(":radio")</td>
			<td>匹配所有单选框</td>
		<tr>
		<tr>
			<td>$(":checkbox")</td>
			<td>匹配所有复选框</td>
		<tr>
		<tr>
			<td>$(":submit")</td>
			<td>匹配所有提交按钮</td>
		<tr>
		<tr>
			<td>$(":image")</td>
			<td>匹配所有图像域</td>
		<tr>
		<tr>
			<td>$(":reset")</td>
			<td>匹配所有重置按钮</td>
		<tr>
		<tr>
			<td>$(":button")</td>
			<td>匹配所有按钮</td>
		<tr>
		<tr>
			<td>$(":file")</td>
			<td>匹配所有文件域</td>
		<tr>
	</table>	
	
12. 表单对象属性筛选选择器

	<table>
		<tr>
			<th>选择器</th>
			<th>描述</th>
		<tr>
		<tr>
			<td>$(":enabled")</td>
			<td>选取可用的表单元素</td>
		<tr>
		<tr>
			<td>$(":disabled")</td>
			<td>选取不可用的表单元素</td>
		<tr>
		<tr>
			<td>$(":checked")</td>
			<td>选取被选中的input元素</td>
		<tr>
		<tr>
			<td>$(":selected")</td>
			<td>选取被选中的option元素</td>
		<tr>
	</table>
	
	*  选择器适用于复选框和单选框，对于下拉框元素, 使用 :selected 选择器
	*  在某些浏览器中，选择器:checked可能会错误选取到<option>元素，所以保险起见换用选择器input:checked，确保只会选取<input>元素

13. .attr()与.removeAttr()

	```
	操作特性的DOM方法主要有3个，getAttribute方法、setAttribute方法和removeAttribute方法。
	而在jQuery中用一个attr()与removeAttr()就可以全部搞定了，包括兼容问题。
	jQuery中用attr()方法来获取和设置元素属性,attr是attribute（属性）的缩写，在jQuery DOM操作中会经常用到attr()。
	```
	
	attr()有4个表达式
	* attr(传入属性名)：获取属性的值
	* attr(属性名, 属性值)：设置属性的值
	* attr(属性名,函数值)：设置属性的函数值
	* attr(attributes)：给指定元素设置多个属性值，即：{属性名一: “属性值一” , 属性名二: “属性值二” , … … }
	
	removeAttr()删除方法 .removeAttr( attributeName ) : 为匹配的元素集合中的每个元素中移除一个属性（attribute）
	
14. html()及.text()

	#### .html()方法 
	获取集合中第一个匹配元素的HTML内容 或 设置每一个匹配元素的html内容，具体有3种用法：
	1. .html() 不传入值，就是获取集合中第一个匹配元素的HTML内容
	2. .html( htmlString )  设置每一个匹配元素的html内容
	3. .html( function(index, oldhtml) ) 用来返回设置HTML内容的一个函数
	
	#### .text()方法
	得到匹配元素集合中每个元素的文本内容结合，包括他们的后代，或设置匹配元素集合中每个元素的文本内容为指定的文本内容。，具体有3种用法：
	1. .text() 得到匹配元素集合中每个元素的合并文本，包括他们的后代
	2. .text( textString ) 用于设置匹配元素内容的文本
	3. .text( function(index, text) ) 用来返回设置文本内容的一个函数
	
		```javascript
		 //通过.text()的回调，获取原本的内容，修改，在重新赋值
        $(".left a:first").text(function(idnex,text){
            return '增加新的文本内容' + text
        })
		```
		
	#### .html与.text的异同:
	1. .html与.text的方法操作是一样，只是在具体针对处理对象不同
	2. .html处理的是元素内容，.text处理的是文本内容
	3. .html只能使用在HTML文档中，.text 在XML 和 HTML 文档中都能使用
	4. 如果处理的对象只有一个子文本节点，那么html处理的结果与text是一样的
	5. 火狐不支持innerText属性，用了类似的textContent属性，.text()方法综合了2个属性的支持，所以可以兼容所有浏览器
	
15. .val()

	#### .val()方法
	1. .val()无参数，获取匹配的元素集合中第一个元素的当前值
	2. .val( value )，设置匹配的元素集合中每个元素的值
	3. .val( function ) ，一个用来返回设置值的函数
	#### 注意事项：
	1. 通过.val()处理select元素， 当没有选择项被选中，它返回null
	2. .val()方法多用来设置表单的字段的值
	3. 如果select元素有multiple（多选）属性，并且至少一个选择项被选中， .val()方法返回一个数组，这个数组包含每个选中选择项的值
	
	#### .html(),.text()和.val()的差异总结：  
	
	<table>
		<tr>
			<th>.html()</th>
			<th>.text()</th>
			<th>.val()</th>
		<tr>
		<tr>
			<td>.html()是用来读取元素的html内容（包括html标签）</td>
			<td>.text()用来读取元素的纯文本内容，包括其后代元素</td>
			<td>.val()是用来读取表单元素的"value"值</td>
		<tr>
		<tr>
			<td colspan="2">.html()和.text()方法不能使用在表单元素上</td>
			<td>.val()只能使用在表单元素上</td>
		<tr>
		<tr>
			<td colspan="3">.html()方法使用在多个元素上时，只读取第一个元素；.val()方法和.html()相同，如果其应用在多个元素上时，只能读取第一个表单元素的"value"值，但是.text()和他们不一样，如果.text()应用在多个元素上时，将会读取所有选中元素的文本内容。</td>
		<tr>
		<tr>
			<td colspan="3">.html(),.text(),.val()三种方法都是用来读取选定元素的内容；</td>
		<tr>
		<tr>
			<td colspan="3">.html(),.text(),.val()都可以使用回调函数的返回值来动态的改变多个元素的内容。</td>
		<tr>
		<tr>
			<td colspan="3">.html(htmlString),.text(textString)和.val(value)三种方法都是用来替换选中元素的内容，如果三个方法同时运用在多个元素上时，那么将会替换所有选中元素的内容。</td>
		<tr>
	</table>
	
16. 增加样式.addClass()

	#### .addClass( className )方法
	1. .addClass( className ) : 为每个匹配元素所要增加的一个或多个样式名
	2. .addClass( function(index, currentClass) ) : 这个函数返回一个或更多用空格隔开的要增加的样式名
	
	<b>.addClass()方法不会替换一个样式类名。它只是简单的添加一个样式类名到元素上</b>
	
17. 删除样式.removeClass()

	#### .removeClass( )方法
	1. .removeClass( [className ] )：每个匹配元素移除的一个或多个用空格隔开的样式名
	2. .removeClass( function(index, class) ) ： 一个函数，返回一个或多个将要被移除的样式名
	
	<b>如果一个样式类名作为一个参数,只有这样式类会被从匹配的元素集合中删除 。 如果没有样式名作为参数，那么所有的样式类将被移除</b>
	
18. 切换样式.toggleClass()

	jQuery提供一个toggleClass方法用于简化这种互斥的逻辑，通过toggleClass方法动态添加删除Class，一次执行相当于addClass，再次执行相当于removeClass
	
	<b>.toggleClass( )方法：</b>在匹配的元素集合中的每个元素上添加或删除一个或多个样式类,取决于这个样式类是否存在或值切换属性。即：如果存在（不存在）就删除（添加）一个类
	1. .toggleClass( className )：在匹配的元素集合中的每个元素上用来切换的一个或多个（用空格隔开）样式类名
	2. .toggleClass( className, switch )：一个布尔值，用于判断样式是否应该被添加或移除
	3. .toggleClass( [switch ] )：一个用来判断样式类添加还是移除的 布尔值
	4. .toggleClass( function(index, class, switch) [, switch ] )：用来返回在匹配的元素集合中的每个元素上用来切换的样式类名的一个函数。接收元素的索引位置和元素旧的样式类作为参数
	
	<b>
	1. toggleClass是一个互斥的逻辑，也就是通过判断对应的元素上是否存在指定的Class名，如果有就删除，如果没有就增加
	2. toggleClass会保留原有的Class名后新增，通过空格隔开
	</b>
	
19. 样式操作.css()

	<b>.css() 方法：获取元素样式属性的计算值或者设置元素的CSS属性</b>
	
	<b>获取：</b>
	1. .css( propertyName ) ：获取匹配元素集合中的第一个元素的样式属性的计算值
	2. .css( propertyNames )：传递一组数组，返回一个对象结果
	
	<b>设置：</b>
	1. .css(propertyName, value )：设置CSS
	2. .css( propertyName, function )：可以传入一个回调函数，返回取到对应的值进行处理
	3. .css( properties )：可以传一个对象，同时设置多个样式
	
	<b>注意事项：</b>
	浏览器属性获取方式不同，在获取某些值的时候都jQuery采用统一的处理，比如颜色采用RBG，尺寸采用px
	.css()方法支持驼峰写法与大小写混搭的写法，内部做了容错的处理
	当一个数只被作为值（value）的时候， jQuery会将其转换为一个字符串，并添在字符串的结尾处添加px，例如 .css("width",50}) 与 .css("width","50px"})一样
	
20. .css()与.addClass()设置样式的区别

	<b>可维护性：</b>
	
	.addClass()的本质是通过定义个class类的样式规则，给元素添加一个或多个类。css方法是通过JavaScript大量代码进行改变元素的样式
	通过.addClass()我们可以批量的给相同的元素设置统一规则，变动起来比较方便，可以统一修改删除。如果通过.css()方法就需要指定每一个元素是一一的修改，日后维护也要一一的修改，比较麻烦
	
	<b>灵活性：</b>
	通过.css()方式可以很容易动态的去改变一个样式的属性，不需要在去繁琐的定义个class类的规则。一般来说在不确定开始布局规则，通过动态生成的HTML代码结构中，都是通过.css()方法处理的
	
	<b>样式值：</b>
	.addClass()本质只是针对class的类的增加删除，不能获取到指定样式的属性的值，.css()可以获取到指定的样式值。
	
	<b>样式的优先级：</b>
	css的样式是有优先级的，当外部样式、内部样式和内联样式同一样式规则同时应用于同一个元素的时候，优先级如下
	<p style="color:red;">外部样式 < 内部样式 < 内联样式</p>
	1. .addClass()方法是通过增加class名的方式，那么这个样式是在外部文件或者内部样式中先定义好的，等到需要的时候在附加到元素上
	2. 通过.css()方法处理的是内联样式，直接通过元素的style属性附加到元素上的
	<p style="color:red;">通过.css方法设置的样式属性优先级要高于.addClass方法</p>
	
	总结：
	1. .addClass与.css方法各有利弊，一般是静态的结构，都确定了布局的规则，可以用addClass的方法，增加统一的类规则
	2. 如果是动态的HTML结构，在不确定规则，或者经常变化的情况下，一般多考虑.css()方式
	
21. 元素的数据存储

	<b>jQuery提供的存储接口</b>
	```
	jQuery.data( element, key, value )   //静态接口,存数据
	jQuery.data( element, key )  //静态接口,取数据   
	.data( key, value ) //实例接口,存数据
	.data( key ) //实例接口,存数据  
	```