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
	* :contains与:has都有查找的意思，但是contains查找包含“指定文本”的元素，has查找包含“指定元素”的元素
	* 如果:contains匹配的文本包含在元素的子元素中，同样认为是符合条件的。
	* :parent与:empty是相反的，两者所涉及的子元素，包括文本节点
	
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
	* CSS display的值是none。
	* type="hidden"的表单元素。
	* 宽度和高度都显式设置为0。
	* 一个祖先元素是隐藏的，该元素是不会在页面上显示
	* CSS visibility的值是hidden
	* CSS opacity的指是0
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
