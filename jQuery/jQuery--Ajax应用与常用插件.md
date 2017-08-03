### 使用load()方法异步请求数据

```html
<body>
    <div id="divtest">
        <div class="title">
            <span class="fl">测试</span> 
            <span class="fr">
                <input id="btnShow" type="button" value="加载" />
            </span>
        </div>
        <ul></ul>
    </div> 
    <script type="text/javascript">
    /*
	 * 使用load()方法通过Ajax请求加载服务器中的数据，并把返回的数据放置到指定的元素中，它的调用格式为：
	 * load(url,[data],[callback])
	 * 参数url为加载服务器地址，可选项data参数为请求时发送的数据，callback参数为数据请求成功后，执行的回调函数。
	 */
        $(function () {
            $("#btnShow").bind("click", function () {
                var $this = $(this);
                $("ul")
                .html("<img src='...' alt=''/>")
                .load("http://www.xxx.xxx/xxx.html",function(){
                    $this.attr("disabled", "true");
                });
            })
        });
    </script>
</body>
```

### 使用getJSON()方法异步加载JSON格式数据

```html
<body>
    <div id="divtest">
        <div class="title">
            <span class="fl">我最喜欢的一项运动</span> 
            <span class="fr"> 
                <input id="btnShow" type="button" value="加载" />
            </span>
        </div>
        <ul></ul>
    </div>
    <script type="text/javascript">
    /*
     * 使用getJSON()方法可以通过Ajax异步请求的方式，获取服务器中的数据，并对获取的数据进行解析，显示在页面中，
     * 它的调用格式为：jQuery.getJSON(url,[data],[callback])或$.getJSON(url,[data],[callback])
     * url参数为请求加载json格式文件的服务器地址，可选项data参数为请求时发送的数据，callback参数为数据请求成功后，执行的回调函数。
     */
        $(function () {
            $("#btnShow").bind("click", function () {
                var $this = $(this);
               $.getJSON("http://www.xxx.com/xxx.json",function(data){
                    $this.attr("disabled", "true");
                    $.each(data, function (index, sport) {
                        if(index==3)
                        $("ul").append("<li>" + sport["name"] + "</li>");
                    });
                });
            })
        });
    </script>
</body>
```

### 使用getScript()方法异步加载并执行js文件

```html
<body>
    <div id="divtest">
        <div class="title">
            <span class="fl">我最喜欢的运动</span> 
            <span class="fr">
                <input id="btnShow" type="button" value="加载" />
            </span>
        </div>
        <ul></ul>
    </div>
    <script type="text/javascript"> 
    /*
     * 使用getScript()方法异步请求并执行服务器中的JavaScript格式的文件，
     * 它的调用格式如下所示：jQuery.getScript(url,[callback])或$.getScript(url,[callback])
     * 参数url为服务器请求地址，可选项callback参数为请求成功后执行的回调函数。
     */
        $(function () {
            $("#btnShow").bind("click", function () {
                var $this = $(this);
               $.getScript("http://xxx.xxx.com/xxx.js",function(){
                    $this.attr("disabled", "true");
                });
            })
        });
    </script>
</body>
```

### 使用get()方法以GET方式从服务器获取数据

```html
<body>
    <div id="divtest">
        <div class="title">
            <span class="fl">我的个人资料</span> 
            <span class="fr">
                <input id="btnShow" type="button" value="加载" />
            </span>
        </div>
        <ul></ul>
    </div>
    <script type="text/javascript">
    /*
     * 使用get()方法时，采用GET方式向服务器请求数据，并通过方法中回调函数的参数返回请求的数据
     * 它的调用格式如下：$.get(url,[callback])
     * 参数url为服务器请求地址，可选项callback参数为请求成功后执行的回调函数。
     */
        $(function () { 
            $("#btnShow").bind("click", function () {
                var $this = $(this);
                $.get("http://www.xxx.com/xxx.php",function(data){
                    $this.attr("disabled", "true");
                    $("ul").append("<li>xxx：" + data.name + "</li>");
                    $("ul").append("<li>xxx：" + data.say + "</li>");
                }, "json");
            })
        });
    </script>
</body>
```

### 使用post()方法以POST方式从服务器发送数据

```html
<body>
    <div id="divtest">
        <div class="title">
            <span class="fl">检测数字是否大于0</span> 
            <span class="fr"><input id="btnCheck" type="button" value="检测" /></span>
        </div>
        <ul>
           <li>请求输入一个数字 <input id="txtNumber" type="text" size="12" /></li>
        </ul>
    </div>
    <script type="text/javascript">
    /*
     * 与get()方法相比，post()方法多用于以POST方式向服务器发送数据，服务器接收到数据之后，进行处理，并将处理结果返回页面
     * 调用格式如下：$.post(url,[data],[callback])
     * 参数url为服务器请求地址，可选项data为向服务器请求时发送的数据，可选项callback参数为请求成功后执行的回调函数。
     */
        $(function () {
            $("#btnCheck").bind("click", function () {
                $.post("http://www.xxx.com/xxx.php",{
                    num:$("#txtNumber").val()
                },
                function (data) { 
                    $("ul").append("<li>你输入的<b>  "
                    + $("#txtNumber").val() + " </b>是<b> "
                    + data + " </b></li>");
                });
            })
        });
    </script>
</body>
```

### 使用serialize()方法序列化表单元素值

```html
<body>
    <div id="divtest">
        <div class="title">
            <span class="fl">我的个人资料</span> 
            <span class="fr">
                <input id="btnAction" type="button" value="序列化" />
            </span>
        </div>
        <form action="">
        <ul>
            <li>姓名：<input name="Text1" type="text" size="12" /></li>
            <li>
                <select name="Select1">
                    <option value="0">男</option>
                    <option value="1">女</option>
                </select>
            </li>
            <li><input name="Checkbox1" type="checkbox" />资料是否可见 </li>
            <li id="litest"></li>
        </ul>
        </form>
    </div>
    <script type="text/javascript">
    /*
     * 使用serialize()方法可以将表单中有name属性的元素值进行序列化，生成标准URL编码文本字符串，直接可用于ajax请求
     * 它的调用格式如下：$(selector).serialize()
     * 其中selector参数是一个或多个表单中的元素或表单元素本身。
     */
        $(function () {
            $("#btnAction").bind("click", function () {
                $("#litest").html($("form").serialize())
            })
        })
    </script>
</body>
```

### 使用ajax()方法加载服务器数据

```html
<body>
    <div id="divtest">
        <div class="title">
            <span class="fl">检测数字的奇偶性</span> 
            <span class="fr">
                <input id="btnCheck" type="button" value="检测" />
            </span>
        </div>
        <ul>
           <li>请求输入一个数字 
               <input id="txtNumber" type="text" size="12" />
           </li>
        </ul>
    </div>
    <script type="text/javascript">
    /*
     * 使用ajax()方法是最底层、功能最强大的请求服务器数据的方法，它不仅可以获取服务器返回的数据，还能向服务器发送请求并传递数值
     * 它的调用格式如下：jQuery.ajax([settings])或$.ajax([settings])
     * 参数settings为发送ajax请求时的配置对象，在该对象中，url表示服务器请求的路径，data为请求时传递的数据，dataType为服务器返回的数据类型，success为请求成功的执行的回调函数，type为发送数据请求的方式，默认为get。
     */
        $(function () {
            $("#btnCheck").bind("click", function () {
                $.ajax({ 
                    url:"http://www.xxx.com/xxx.php",
                    data: { num: $("#txtNumber").val() },
                    type:"POST",
                    success: function (data) {
                        $("ul").append("<li>你输入的<b>  "
                        + $("#txtNumber").val() + " </b>是<b> "
                        + data + " </b></li>");
                    }
                });
            })
        });
    </script>
</body>
```

### 使用ajaxSetup()方法设置全局Ajax默认选项

```html
<body>
    <div id="divtest">
        <div class="title">
            <span class="fl">奇偶性和是否大于0</span> 
            <span class="fr">
                <input id="btnShow_1" type="button" value="验证1" />
                <input id="btnShow_2" type="button" value="验证2" />
            </span>
        </div>
        <ul>
           <li>请求输入一个数字 
               <input id="txtNumber" type="text" size="12" />
           </li>
        </ul>
    </div>
    <script type="text/javascript">
    /*
     * 使用ajaxSetup()方法可以设置Ajax请求的一些全局性选项值，设置完成后，后面的Ajax请求将不需要再添加这些选项值
     * 它的调用格式为：jQuery.ajaxSetup([options])或$.ajaxSetup([options])
     * 可选项options参数为一个对象，通过该对象设置Ajax请求时的全局选项值。
     */
        $(function () {
            $.ajaxSetup({
                type:'post',
            success:function(data){
                    $("ul").append("<li>你输入的<b>  "
                        + $("#txtNumber").val() + " </b>是<b> "
                        + data + " </b></li>"); 
                }
            });
            $("#btnShow_1").bind("click", function () {
                $.ajax({
                    data: { num: $("#txtNumber").val() },
                    url: "http://www.xxx.com/xxx.php"
                });
            })
            $("#btnShow_2").bind("click", function () {
                $.ajax({
                    data: { num: $("#txtNumber").val() },
                    url: "http://www.xxx.com/xxx.php"
                });
            })
        });
    </script>
</body>
```

### 使用ajaxStart()和ajaxStop()方法

```html
<body>
    <div id="divtest">
        <div class="title">
            <span class="fl">加载一段文字</span> 
            <span class="fr">
                <input id="btnShow" type="button" value="加载" />
            </span>
        </div> 
        <ul>
           <li id="divload"></li>
        </ul>
    </div>
    <script type="text/javascript">
    /*
     * ajaxStart()和ajaxStop()方法是绑定Ajax事件。ajaxStart()方法用于在Ajax请求发出前触发函数，ajaxStop()方法用于在Ajax请求完成后触发函数
     * 它们的调用格式为： $(selector).ajaxStart(function())和$(selector).ajaxStop(function())
     * 两个方法中括号都是绑定的函数，当发送Ajax请求前执行ajaxStart()方法绑定的函数，请求成功后，执行ajaxStop ()方法绑定的函数。
     */
        $(function () {
            $("#divload").ajaxStart(function(){
                $(this).html("正在请求数据...");
            });
            $("#divload").ajaxStop(function(){
                $(this).html("数据请求完成！");
            }); 
            $("#btnShow").bind("click", function () {
                var $this = $(this);
                $.ajax({
                    url: "http://www.xx.com/xxx.php",
                    dataType: "json",
                    success: function (data) {
                        $this.attr("disabled", "true");
                    }
                });
            })
        });
    </script>
</body>
```

### 表单验证插件——validate

```html
<script type="text/javascript" src="http://www.imooc.com/data/jquery.validate.js"></script>
<script type="text/javascript" src="http://www.imooc.com/data/jquery.validate.messages_cn.js"></script>
<body>
    <form id="frmV" method="get" action="#">
        <div id="divtest">
            <div class="title">
                <span class="fl">表单验证插件</span> 
                <span class="fr">
                    <input id="btnSubmit" type="submit" value="提交" />
                </span> 
            </div>
            <div class="content">
                <span class="fl">邮箱：</span><br />
                <input id="email" name="email" type="text" /><br />
                <span class="tip"></span>
            </div>
        </div>
    </form>
    <script type="text/javascript">
    /*
     * 该插件自带包含必填、数字、URL在内容的验证规则，即时显示异常信息，此外，还允许自定义验证规则
     * 插件调用方法如下：$(form).validate({options})
     * form参数表示表单元素名称，options参数表示调用方法时的配置对象，所有的验证规则和异常信息显示的位置都在该对象中进行设置。
     */
        $(function () {
            $("#frmV").validate( 
              { 
                  /*自定义验证规则*/
                  rules: {
                        email:{
                            required:true,
                            email:true
                      }
                  },
                  /*错误提示位置*/
                  errorPlacement: function (error, element) {
                      error.appendTo(".tip");
                  }
              }
            );
        });
    </script>
</body> 
```

### 表单插件——form

```html
<script type="text/javascript" src="http://www.imooc.com/data/jquery.form.js"></script>

<body>
    <form id="frmV" method="post" action="#">
        <div id="divtest">
            <div class="title">
                <span class="fl">个人信息页</span> 
                <span class="fr">
                    <input id="btnSubmit" type="submit" value="提交" />
                </span>
            </div>
            <div class="content">
                <span class="fl">用户名：</span><br />
                <input id="user" name="user" type="text" /><br />
                <span class="fl">昵称：</span><br />
                <input id="nick" name="nick" type="text" />
                <div class="tip"></div>
            </div>
        </div>
    </form>
    <script type="text/javascript">
    /*
     * 通过表单form插件，调用ajaxForm()方法，实现ajax方式向服务器提交表单数据，并通过方法中的options对象获取服务器返回数据
     * 调用格式如下：$(form). ajaxForm ({options})
     * 其中form参数表示表单元素名称；options是一个配置对象，用于在发送ajax请求过程，设置发送时的数据和参数。
     */
        $(function () {
            var options = {
                url: "http://www.imooc.com/data/form_f.php", 
                target: ".tip"
            }
            $("#frmV").ajaxForm(options)
        });
    </script>
</body>
```

### 图片灯箱插件——lightBox

```html
<link rel="stylesheet" type="text/css" href="http://www.imooc.com/data/jquery.notesforlightbox.css" />
<script type="text/javascript" src="http://www.imooc.com/data/jquery.notesforlightbox.js"></script>
<body>
    <div id="divtest">
        <div class="title">
            <span class="fl">我的相册</span>
        </div>
        <div class="content">
            <div class="divPics">
                <ul>
                    <li><a href="xx.jpg" title="第1篇风景图片">
                        <img src="xx.jpg" alt="" />
                    </a></li>
                    <li><a href="xx.jpg" title="第2篇风景图片">
                        <img src="xx.jpg" alt="" />
                    </a></li>
                    <li><a href="xx.jpg" title="第3篇风景图片">
                        <img src="xx.jpg" alt="" />
                    </a></li>
                </ul>
            </div> 
        </div>   
    </div>
    <script type="text/javascript">
    /*
     * 该插件可以用圆角的方式展示选择中的图片，使用按钮查看上下张图片，在加载图片时自带进度条，还能以自动播放的方式浏览图片
     * 调用格式如下：$(linkimage).lightBox({options})
     * 其中linkimage参数为包含图片的<a>元素名称，options为插件方法的配置对象。
     */
        $(function () {
            $(".divPics a").lightBox({ 
                overlayBgColor: "#666", //图片浏览时的背景色
                overlayOpacity: 0.5, //背景色的透明度
                containerResizeSpeed: 600 //图片切换时的速度
            })
        });
    </script>
</body>
```

### 图片放大镜插件——jqzoom

```html
<link href="http://www.imooc.com/data/jquery.jqzoom.css" rel="stylesheet" type="text/css" />
<script type="text/javascript" src="http://www.imooc.com/data/jquery.jqzoom.js"></script>
<body>
    <div id="divtest">
        <div class="title">
            <span class="fl">图片放大镜</span> 
        </div>
        <div class="content">
            <a href="http://xxx/xxx.jpg" id="jqzoom" title="">
                 <img src="xx.jpg" alt=""/>
            </a>
        </div>
    </div>
    <script type="text/javascript">
    /*
     * 在调用jqzoom图片放大镜插件时，需要准备一大一小两张一样的图片，在页面中显示小图片，当鼠标在小图片中移动时，调用该插件的jqzoom()方法，显示与小图片相同的大图片区域，从而实现放大镜的效果
     * 调用格式如下：$(linkimage).jqzoom({options})
     * 其中linkimage参数为包含图片的<a>元素名称，options为插件方法的配置对象。
     */
        $(function () { 
            $("#jqzoom").jqzoom({ //绑定图片放大插件jqzoom
                zoomWidth: 123, //小图片所选区域的宽
                zoomHeight: 123, //小图片所选区域的高
                zoomType: 'reverse' //设置放大镜的类型
            });
        });
    </script>
</body>
```

### cookie插件——cookie

```
使用cookie插件后，可以很方便地通过cookie对象保存、读取、删除用户的信息，还能通过cookie插件保存用户的浏览记录
它的调用格式为：保存：$.cookie(key，value)；读取：$.cookie(key)，删除：$.cookie(key，null)
其中参数key为保存cookie对象的名称，value为名称对应的cookie值。
```

### 搜索插件——autocomplete

```html
<link href="http://www.imooc.com/data/jquery.autocomplete.css" rel="stylesheet" type="text/css" />
<script src="http://www.imooc.com/data/jquery.autocomplete.js" type="text/javascript"></script>   
<body>
    <div id="divtest">
        <div class="title">
            <span class="fl">搜索插件</span>
        </div>
        <div class="content">
            <span class="fl">用户名</span><br />
            <input id="txtSearch" name="txtSearch" type="text" />
            <div class="tip">
            </div>
        </div>
    </div>
    <script type="text/javascript">
    /*
     * 搜索插件的功能是通过插件的autocomplete()方法与文本框相绑定，当文本框输入字符时，绑定后的插件将返回与字符相近的字符串提示选择
     * 调用格式如下：$(textbox).autocomplete(urlData,[options]);
     * textbox参数为文本框元素名称，urlData为插件返回的相近字符串数据，可选项参数options为调用插件方法时的配置对象。
     */
        $(function () {
            var arrUserName = ["王五", "刘明", "李小四", "刘促明", "李渊", "张小三", "王小明"];
            $("#txtSearch").autocomplete(arrUserName,{
                minChars: 0, //双击空白文本框时显示全部提示数据
                formatItem: function (data, i, total) {
                    return "<I>" + data[0] + "</I>"; //改变匹配数据显示的格式
                },
                formatMatch: function (data, i, total) { 
                    return data[0];
                },
                formatResult: function (data) {
                    return data[0];
                }
            }).result(SearchCallback); 
            function SearchCallback(event, data, formatted) {
                $(".tip").show().html("您的选择是：" + (!data ? "空" : formatted));
            }
        });
    </script>
</body>
```

### 右键菜单插件——contextmenu

```html
<link href="http://www.imooc.com/data/jquery.contextmenu.css" rel="stylesheet" type="text/css" />
<script src="http://www.imooc.com/data/jquery.contextmenu.js" type="text/javascript"></script>
<body>
    <div id="divtest">
        <div class="title"><span class="fl">点击右键</span></div>
        <div class="content">
            <input id="btnSubmit" type="button" value="提交" />
            <div class="tip"></div>
        </div>
        <div class="contextMenu" id="sysMenu">
            <ul>
                <li id="Li3"><img src="xx.jpg" alt="" />保存</li>
                <li id="Li4"><img src="xx.jpg" alt="" />退出</li>
            </ul>
        </div>
    </div>
    <script type="text/javascript"> 
    /*
     * 右键菜单插件可以绑定页面中的任意元素，绑定后，选中元素，点击右键，便通过该插件弹出一个快捷菜单，点击菜单各项名称执行相应操作
     * 调用代码如下：$(selector).contextMenu(menuId,{options});
     * Selector参数为绑定插件的元素，meunId为快捷菜单元素，options为配置对象。
     */
        $(function () {
           $("#btnSubmit").contextMenu('sysMenu',
              { bindings:
                 {
                     'Li3': function (Item) {
                         $(".tip").show().html("您点击了“保存”项");
                     },
                     'Li4': function (Item) {
                         $(".tip").show().html("您点击了“退出”项");
                     }
                 }
              });
        });
    </script>
</body>
```

### 自定义对象级插件——lifocuscolor插件

```html
<script src="http://www.imooc.com/data/jquery.lifocuscolor.js" type="text/javascript"></script>  
<body>
    <div id="divtest">
        <div class="title"> 
            <span class="fl">对象级别的插件</span>
        </div>
        <div class="content">
            <ul id="u1">
                <li><span>橘子</span><span>水果</span></li>
                <li><span>芹菜</span><span>蔬菜</span></li>
                <li><span>香蕉</span><span>水果</span></li>
            </ul>
        </div>
    </div>
    <script type="text/javascript">
    /*
     * 自定义的lifocuscolor插件可以在<ul>元素中，鼠标在表项<li>元素移动时，自定义其获取焦点时的背景色，即定义<li>元素选中时的背景色
     * 调用格式为：$(Id).focusColor(color)
     * 参数Id表示<ul>元素的Id号，color表示<li>元素选中时的背景色。
     */
        $(function () {
           $("#u1").focusColor("#333") //调用自定义的插件  
        })
    </script>
</body>
```

### 自定义类级别插件—— twoaddresult

```html
<script src="http://www.imooc.com/data/jquery.twoaddresult.js" type="text/javascript"></script>
<body>
    <div id="divtest">
        <div class="title">
            <span class="fl">自定义类级别插件</span> 
            <span class="fr">
                <input id="btnCount" type="button" value="计算" />
            </span>
        </div>
        <div class="content">
            两数相减：
            <input id="Text1" type="text" class="txt" />
            -
            <input id="Text2" type="text" class="txt" />
            =
            <input id="Text3" type="text" class="txt" />
        </div>
    </div> 
    <script type="text/javascript">
    /*
     * 通过调用自定义插件twoaddresult中的不同方法，可以实现对两个数值进行相加和相减的运算，导入插件后
     * 调用格式分别为：$.addNum(p1,p2) 和 $.subNum(p1,p2)
     * 调用格式分别为计算两数值相加和相减的结果，p1和p2为任意数值。
     */
        $(function () {
            $("#btnCount").bind("click", function () {
                $("#Text3").val(
                    $.subNum($("#Text1").val(),$("#Text2").val())
        		);
            });
        });
    </script>
</body>
```

### 拖曳插件——draggable

```html
<script src="http://www.imooc.com/data/jquery-ui-1.9.2.min.js" type="text/javascript"></script>
<body>
    <div id="divtest">
        <div id="x" class="drag">沿x轴拖拽</div>
        <div id="y" class="drag">沿y轴拖拽</div>
    </div>
    <script type="text/javascript"> 
    /*
     * 拖曳插件draggable的功能是拖动被绑定的元素，当这个jQuery UI插件与元素绑定后，可以通过调用draggable()方法，实现各种拖曳元素的效果
     * 调用格式如下：$(selector). draggable({options})
     * options参数为方法调用时的配置对象，根据该对象可以设置各种拖曳效果，如“containment”属性指定拖曳区域，“axis”属性设置拖曳时的坐标方向。
     */
        $(function () {
            $("#x").draggable({containment:"#divtest",axis:"x"})
            $("#y").draggable({containment:"#divtest",axis:"y"})
        });
    </script>
</body>
```

### 放置插件——droppable

```html
<script src="http://www.imooc.com/data/jquery-ui-1.9.2.min.js" type="text/javascript"></script>   
<body>
    <div id="divtest">
        <div class="box">
            <div class="title">产品区</div>
            <div class="drag"><div>苹果</div></div>
        </div>
        <div class="box">
            <div class="title">回收站</div>
            <div class="cart"><div id="tip">还没有产品</div></div>
        </div>
    </div>
    <script type="text/javascript">
    /*
     * 除使用draggable插件拖曳任意元素外，还可以调用droppable UI插件将拖曳后的任意元素放置在指定区域中，类似购物车效果
     * 调用格式如下：$(selector).droppable({options})
     * selector参数为接收拖曳元素，options为方法的配置对象，在对象中，drop函数表示当被接收的拖曳元素完全进入接收元素的容器时，触发该函数的调用。
     */
        $(function () {
            $(".drag").draggable();
            $(".cart").droppable({ 
                drop: function () {
                       $(this).css("background","#eee").find("#tip").html("")
                }
            })
        });
    </script>
</body>
```

### 拖曳排序插件——sortable

```html
<script src="http://www.imooc.com/data/jquery-ui-1.9.2.min.js" type="text/javascript"></script>
<body>
    <div id="divtest">
        <div class="title">
            <span class="fl">我最喜欢的运动</span>
        </div>
        <div class="content">
            <ul>
                <li>1)足球</li>
                <li>2)散步</li>
                <li>3)篮球</li>
                <li>4)乒乓球</li>
                <li>5)骑自行车</li>
            </ul>
        </div>
    </div>
    <script type="text/javascript">
    /*
     * 拖曳排序插件的功能是将序列元素（例如<option>、<li>）按任意位置进行拖曳从而形成一个新的元素序列，实现拖曳排序的功能
     * 它的调用格式为：$(selector).sortable({options});
     * selector参数为进行拖曳排序的元素，options为调用方法时的配置对象
     */
        $(function () {
            $("ul").sortable({
               delay:2, //防止与点击事件冲突，延时2秒
               opacity:0.5 //以透明度0.5拖动
            })
        });
    </script>
</body>
```

### 面板折叠插件——accordion

```html
<link href="Css/jquery-ui.css" rel="stylesheet" type="text/css" />
<script src="http://www.imooc.com/data/jquery-ui-1.9.2.min.js" type="text/javascript"></script>
<body>
    <div id="divtest">
        <div id="accordion">
            <h3>
                <a href="#">白富美</a></h3>
            <p>咱们结婚吧!</p>
            <h3>
                <a href="#">土豪族</a></h3>
            <p>咱们交个朋友吧!</p>
        </div>
    </div>
    
    <script type="text/javascript"> 
    /*
     * 面板折叠插件可以实现页面中指定区域类似“手风琴”的折叠效果，即点击标题时展开内容，再点另一标题时，关闭已展开的内容
     * 调用格式如下：$(selector).accordion({options});
     * 参数selector为整个面板元素，options参数为方法对应的配置对象。
     */
        $(function () {
            $("#accordion").accordion()
        });
    </script>
</body>
```

### 选项卡插件——tabs

```html
<link href="http://www.imooc.com/data/jquery-ui.css" rel="stylesheet" type="text/css" />
<script src="http://www.imooc.com/data/jquery-ui-1.9.2.min.js" type="text/javascript"></script>
<body>
    <div id="divtest">
        <div id="tabs">
            <ul>
                <li><a href="#tabs-1">最爱吃的水果</a></li>
                <li><a href="#tabs-2">最喜欢的运动</a></li>
            </ul>
            <div id="tabs-1">
                <p>橘子</p>
                <p>香蕉</p>
                <p>葡萄</p>
                <p>苹果</p>
                <p>西瓜</p>
            </div>
            <div id="tabs-2">
                <p>足球</p> 
                <p>散步</p>
                <p>篮球</p>
                <p>乒乓球</p>
                <p>骑自行车</p>
            </div>
        </div>
    </div>
    <script type="text/javascript">
    /*
     * 使用选项卡插件可以将<ul>中的<li>选项定义为选项标题，在标题中，再使用<a>元素的“href”属性设置选项标题对应的内容
     * 它的调用格式如下：$(selector).tabs({options});
     * selector参数为选项卡整体外围元素，该元素包含选项卡标题与内容，options参数为tabs()方法的配置对象，通过该对象还能以ajax方式加载选项卡的内容。
     */
        $(function () {
           $("#tabs").tabs({
                //设置各选项卡在切换时的动画效果
                fx: { opacity: "toggle", height: "toggle" },
                event: "mousemove" //通过移动鼠标事件切换选项卡
            })
        });
    </script>
</body>
```

### 对话框插件——dialog

```html
<link href="http://www.imooc.com/data/jquery-ui.css" rel="stylesheet" type="text/css" />
<script src="http://www.imooc.com/data/jquery-ui-1.9.2.min.js" type="text/javascript"></script>
<body>
    <div id="divtest">
        <div class="content">
            <span id="spnName" class="fl">张三</span>
            <input id="btnDelete" type="button" value="删除"  class="fr"/>
        </div>
        <div id='dialog-modal'></div>
    </div>
    <script type="text/javascript">
    /*
     * 对话框插件可以用动画的效果弹出多种类型的对话框，实现JavaScript代码中alert()和confirm()函数的功能
     * 它的调用格式为：$(selector).dialog({options});
     * selector参数为显示弹出对话框的元素，通常为<div>，options参数为方法的配置对象，在对象中可以设置对话框类型、“确定”、“取消”按钮执行的代码等。
     */
        $(function () {
            $("#btnDelete").bind("click", function () { //询问按钮事件
                if ($("#spnName").html() != null) { //如果对象不为空
                    sys_Confirm("您真的要删除该条记录吗？");
                    return false;
                }
            });
        });
        function sys_Confirm(content) { //弹出询问信息窗口
            $("#dialog-modal").dialog({
                height: 140,
                modal: true,
                title: '系统提示',
                hide: 'slide', 
                buttons: {
                    '确定': function () {
                        $("#spnName").remove();
                        $(this).dialog("close");
                    },
                    '取消': function () {
                        $(this).dialog("close");
                    }
                },
                open: function (event, ui) {
                    $(this).html("");
                    $(this).append("<p>" + content + "</p>");
                }
            });
        }
    </script>
</body>
```

### 菜单工具插件——menu

```html
<link href="http://www.imooc.com/data/jquery-ui.css" rel="stylesheet" type="text/css" />
<script src="http://www.imooc.com/data/jquery-ui-1.9.2.min.js" type="text/javascript"></script>
<body>
    <ul id="menu">
        <li><a href="#">小明一中</a>
            <ul>
                <li><a href="#">高中部</a>
                    <ul>
                        <li><a href="#">高一(1)班</a></li>
                        <li><a href="#">高一(2)班</a></li>
                        <li><a href="#">高一(3)班</a>
                            <ul>
                                <li><a href="#">小胡</a></li>
                                <li><a href="#">小李</a></li>
                                <li><a href="#">小陈</a></li>
                            </ul>
                        </li>
                    </ul>
                </li>
                <li><a href="#">初中部</a>
                    <ul>
                        <li><a href="#">初一(1)班</a></li>
                        <li><a href="#">初一(2)班</a></li> 
                        <li><a href="#">初一(3)班</a></li>
                    </ul>
                </li>
                <li><a href="#">教研部</a></li>
            </ul>
        </li>
        <li class="ui-state-disabled"><a href="#">大明二中</a></li>
    </ul>
    <script type="text/javascript">
    /*
     * 菜单工具插件可以通过<ul>创建多级内联或弹出式菜单，支持通过键盘方向键控制菜单滑动，允许为菜单的各个选项添加图标
     * 调用格式如下：$(selector).menu({options});
     * selector参数为菜单列表中最外层<ul>元素，options为menu()方法的配置对象。
     */
        $(function () {
           $("#menu").menu()
        });
    </script>
</body>
```

### 微调按钮插件——spinner

```html
<link href="http://www.imooc.com/data/jquery-ui.css" rel="stylesheet" type="text/css" />
<script src="http://www.imooc.com/data/jquery-ui-1.9.2.min.js" type="text/javascript"></script>
<body>
    <div id="divtest">
        <div class="title">选择颜色值</div> 
        <div class="content">
            <span id="spnColor" class="input fl">
                <input />
            </span>
            <span id="spnPrev" class="prev fr"></span>
        </div>
    </div>
    <script type="text/javascript">
    /*
     * 微调按钮插件不仅能在文本框中直接输入数值，还可以通过点击输入框右侧的上下按钮修改输入框的值，还支持键盘的上下方向键改变输入值
     * 调用格式如下：$(selector).spinner({options});
     * selector参数为文本输入框元素，可选项options参数为spinner()方法的配置对象，在该对象中，可以设置输入的最大、最小值，获取改变值和设置对应事件。
     */
        $(function () {
            //定义变量
            var intR = 0, intG = 0, intB = 0, strColor;
            $("input").spinner({
                //初始化插件 
                max: 10,
                min: 0,
                //设置微调按钮递增/递减事件
                spin: function (event, ui) {
                    if (ui.value == 8)
                        spnPrev.style.backgroundColor = "red";
                    else
                        spnPrev.style.backgroundColor = "green";
                },
                //设置微调按钮值改变事件
                change: function (event, ui) {
                    var intTmp = $(this).spinner("value");
                    if (intTmp < 0) $(this).spinner("value", 0);
                    if (intTmp > 10) $(this).spinner("value", 10);
                    if (intTmp == 8)
                        spnPrev.style.backgroundColor = "red";
                    else
                        spnPrev.style.backgroundColor = "green";
                }
            });
        });
    </script>
</body>
```

### 工具提示插件——tooltip

```html
<link href="http://www.imooc.com/data/jquery-ui.css" rel="stylesheet" type="text/css" />
<script src="http://www.imooc.com/data/jquery-ui-1.9.2.min.js" type="text/javascript"></script>
<body>
    <div id="divtest">
        <div class="title">
            工具提示插件</div>
        <div class="content">
            <div>
                <label for="name">
                    姓名</label>
                <input id="name" name="name" title="我是土豪，欢迎与我做朋友" />
            </div>
        </div>
    </div>
    <script type="text/javascript">
    /*
     * 工具提示插件可以定制元素的提示外观，提示内容支持变量、Ajax远程获取，还可以自定义提示内容显示的位置
     * 它的调用格式如下：$(selector).tooltip({options});
     * 其中selector为需要显示提示信息的元素，可选项参数options为tooltip()方法的配置对象，在该对象中，可以设置提示信息的弹出、隐藏时的效果和所在位置。
     */
        $(function () {
            $("#name").tooltip({
                show: {
                    effect: "slideDown", 
                    delay: 350
                },
                hide: {
                    effect: "explode",
                    delay: 350
                },
                position: {
                    my: "left top",
                    at: "left bottom"
                }
            });
        });
    </script>
</body>
```

### 获取浏览器的名称与版本信息

```javascript
$(function () {
    var strTmp = "您的浏览器名称是：";
    if ($.browser.chrome) { //谷歌浏览器
        strTmp += "Chrome";
    }
    if ($.browser.mozilla) { //火狐相关浏览器
        strTmp += "Mozilla FireFox";
    }
    strTmp += "<br /><br /> 版本号是：" //获取版本号
           +$.browser.version;
    $(".content").html(strTmp); 
});
/*
在jQuery中，通过$.browser对象可以获取浏览器的名称和版本信息，
$.browser.chrome为true，表示当前为Chrome浏览器，
$.browser.mozilla为true，表示当前为火狐浏览器，
$.browser.version方式获取浏览器版本信息。
*/
```

### 检测浏览器是否属于W3C盒子模型

```
/*
浏览器的盒子模型分为两类，一类为标准的w3c盒子模型，另一类为IE盒子模型，
两者区别为在Width和Height这两个属性值中是否包含padding和border的值，w3c盒子模型不包含，IE盒子模型则包含，
在jQuery 中，可以通过$.support.boxModel对象返回的值，检测浏览器是否属于标准的w3c盒子模型。
*/
$(function () {
    var strTmp = "您打开的页面是：";
    if ($.support.boxModel) { //是W3C盒子模型
        strTmp += "W3C盒子模型"; 
    }
    else { //是IE盒子模型
        strTmp += "IE盒子模型";
    }
    $(".content").html(strTmp);
});
```

### 检测对象是否为空

```javascript
/*
在jQuery中，可以调用名为$.isEmptyObject的工具函数，检测一个对象的内容是否为空，如果为空，则该函数返回true，否则，返回false值
调用格式如下：$.isEmptyObject(obj);
参数obj表示需要检测的对象名称。
*/
$(function () {
    var obj = { "姓名": "土豪一族" };
    var strTmp = "您定义了一个：";
    if ($.isEmptyObject(obj)) { //检测是否为空
        strTmp += "空对象";
    }
    else {
        strTmp += "非空对象"; 
    }
    $(".content").html(strTmp);
});
```

### 检测对象是否为原始对象

```javascript
/*
调用名为$.isPlainObject的工具函数，能检测对象是否为通过{}或new Object()关键字创建的原始对象，如果是，返回true，否则，返回false值
调用格式为：$.isPlainObject (obj);
参数obj表示需要检测的对象名称。
*/
$(function () {
    var obj = "null";
    var strTmp = "您定义了一个：";
    if ($.isPlainObject (obj)) { //检测是否为原始对象
        strTmp += "原始对象";
    }
    else { 
        strTmp += "非原始对象";
    }
    $(".content").html(strTmp);
});
```

### 检测两个节点的包含关系

```javascript
/*
调用名为$.contains的工具函数，能检测在一个DOM节点中是否包含另外一个DOM节点，如果包含，返回true，否则，返回false值,
调用格式为：$.contains (container, contained);
参数container表示一个DOM对象节点元素，用于包含其他节点的容器，contained是另一个DOM对象节点元素，用于被其他容器所包含。
*/
$(function () {
    var node_a = document.body.firstChild;
    var node_b = document.body;
    var strTmp = "对象node_a";
    if ($.contains(node_a,node_b)) { //检测是否包含节点
        strTmp += " 包含 ";
    }
    else {
        strTmp += " 不包含 "; 
    }
    strTmp += "对象node_b";
    $(".content").html(strTmp);
});
```

### 字符串操作函数

```html
/*
调用名为$.trim的工具函数，能删除字符串中左右两边的空格符，但该函数不能删除字符串中间的空格
调用格式为：$.trim (str);
参数str表示需要删除左右两边空格符的字符串。
*/
<body>
    <div id="divtest">
        <div class="title">
            <span class="fl">字符串操作函数</span> 
            <span class="fr">
                <input id="btnShow" name="btnShow" type="button" value="计算" />
            </span>
        </div>
        <div class="content">
            <input id="txtName" name="txtName" type="text" />
            <div class="tip"></div>
        </div>
    </div>
    <script type="text/javascript">
        $(function () {
            $("#btnShow").bind("click", function () {
                $(".tip").html("");
                var strTmp = "内容：";
                var strOld = $("#txtName").val();
                var strNew =$.trim(strOld);
                strTmp += strOld; 
                strTmp += "<br/><br>除掉空格符前的长度："
                strTmp += strOld.length;
                strTmp += "<br/><br>除掉空格符后的长度："
                strTmp += strNew.length;
                $(".tip").show().append(strTmp);
            });
        });
    </script>
</body>
```

### URL操作函数

```
调用名为$. param的工具函数，能使对象或数组按照key/value格式进行序列化编码，该编码后的值常用于向服务端发送URL请求
调用格式为：$. param (obj);
参数obj表示需要进行序列化的对象，该对象也可以是一个数组，整个函数返回一个经过序列化编码后的字符串。
```

### 使用$.extend()扩展工具函数

```javascript
/*
 * 调用名为$. extend的工具函数，可以对原有的工具函数进行扩展，自定义类级别的jQuery插件
 * 调用格式为：$. extend ({options});
 * 参数options表示自定义插件的函数内容。
 */
/*------------------------------------------------------------/
功能：返回两个数中最小值
参数：数字p1,p2
返回：最小值的一个数
示例：$.MinNum(1,2);
/------------------------------------------------------------*/
(function ($) {
    $.extend({ 
        "MinNum": function (p1, p2) {
            return (p1 > p2) ? p2 : p1;
        }
    });
})(jQuery);
$(function () {
    $("#btnShow").bind("click", function () {
        $(".tip").html("");
        var strTmp = "17与18中最小的数是：";
        strTmp +=$.MinNum(17, 18);
        //显示在页面中
        $(".tip").show().append(strTmp);
    });
});
```

###  使用$.extend()扩展Object对象

```
除使用$.extend扩展工具函数外，还可以扩展原有的Object对象，在扩展对象时，两个对象将进行合并，当存在相同属性名时，后者将覆盖前者
调用格式为：$. extend (obj1,obj2,…objN);
参数obj1至objN表示需要合并的各个原有对象。
```

