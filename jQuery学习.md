## jQuery介绍

   ```
   jQuery是一个使用最广泛的js端插件
        集成了很多js的元素操作方法、事件方法、动画效果、ajax请求等等功能
        框架：是很多插件的集合，可以解决一个完整项目开发的所有问题。
        
        underscore.js封装了很多常用的操作方法

        jQuery.validate 表单验证插件,基于jQuery使用

        jQuery版本的问题，在jQuery2.0之后不再支持ie早期版本(如ie6\7)
        如果你的页面需要支持ie早期版本，需要使用jQuery小于2.0的版本

        如何安装下载jQuery:
        1. node install jQuery@版本号
        2. bower install jQuery
        3. 通过官方网站或者github下载
        4. 可以使用cdn上提供的地址，引入在线版本。如(http://www.bootcdn.cn/)
   ```
## jQuery的使用

   ```
    此方法是js后期(最近)加入的方法，早期浏览器不支持
    此方法借鉴了jQuery的元素选择方法
    console.log(document.querySelector("#sName"));

    在使用jQuery的时候，使用$和jQuery关键字是等价的
    console.log(jQuery);
    console.log($);

    获取使用的jQuery版本号的方法
    console.log($.fn.jquery);
    console.log(jQuery.fn.jquery);

    通过原生js选择id为container的标签元素
    console.log(document.querySelector("#container"));

    通过使用jQuery获取id为container的标签元素
    console.log($("#container"));

        /***
         * 通过jQuery元素选择器获取的结果是一个jQuery对象
         * 通过原生js选择器获取的结果是一个js对象
         * 两者有很大的差别
         * 学习jQuery的时候一定要把原生方法和jQuery方法区分开
         * 尽量避免两者的混用
         */

      
    此方法是为原生js选择的元素添加click事件
        document.querySelector("#container").onclick = function(eve){
            alert("这个是container容器");
        }

     
     此方法是为jQuery选择的对象添加click事件
        $("#container").click(function(){
            alert("这个是container容器");
        })

        /****
         * 两种添加事件的写法不一样 不能混用
         */

        ///对页面中所有的p标签添加click事件
        $("p").click(function(){
            console.log(this);
            alert($(this).text());////通过jQuery获取标签的文本内容
            alert(this.innerText); ////在jQuery方法中使用了原生js方法
        });
   ```
## 表单提交事件

   ```
   ////为按钮添加click事件
    $("#btn").click(function(){
        点击click事件之后 我要获取表单中的输入内容
        通过val()方法获取或者设置表单元素的value值
        通过attr() 获取或者设置元素的属性
            $("#userName").attr("data-msg")///获取属性data-msg的值
            $("#userName").attr("data-msg","哈哈")////设置属性data-msg的值为"哈哈"
        对于data-xx的属性 可以通过 .data(xx)的方式获取如：
        $("#userName").data("msg") ////获取属性data-msg的值

        console.log($("#userName").val());

        console.log($("#userName").attr("data-msg"));

        ////输出xx属性的值
        console.log($("#email").attr("xx"));   ----><input type="text" xx="这个是自定义的属性" data-msg="请输入邮箱" name="email" id="email">    
    });

    /////实现全屏效果,需要使用jquery.fullscreen.js插件
    $("#btnFullScreen").click(function(){
        $(document).fullScreen(true);       
    });

    ////使用validate插件对表单元素进行验证(jquery.validate.js)
    $("#form").validate({
        debug:true, ////加此段的目的是禁止表单验证通过后进行提交
        rules:{
            userName:{
                required:true, ////必填项
                minlength:2, /////最小长度
                maxlength:10 /////最大长度
            },
            email:{
                required:true,
                email:true
            }
        },
        messages:{
            userName:{
                minlength:"用户名最小长度为2",
                maxlength:"用户名最大长度为10"
            },
            email:{
                email:"邮箱格式错误"
            }
        }
    })
   ```

## query

   ```
    $("#id") 根据id选择一个标签和document.getElementById("id")方法效果类似
    $(".class") 根据class的值选择多个元素
    $("span") 通过表签名
    $("div span") 选择div表中中的span标签
    $("#div span") 选择id为div的元素内的span标签
    $("li.li-item") 选择所有class="li-item"的li标签

    选中的元素可以通过each进行遍历，获取每一个值
    可以通过 .text() 获取或者设置元素的文本内容
    可以通过 .html() 获取或者设置元素的html内容
    可以通过 .css() 设置样式,两个参数(参数一：样式名，参数二：样式值)

    console.log($(".li-item").length);选择页面中所有class="li-item"的元素，不管元素的类型
    console.log($("div.li-item").length);选择页面中所有的class="li-item"的div元素
    console.log($("ul li.li-item").length);选择ul中的所有class="li-item"的li元素
    console.log($("ul li").length);选择ul中的所有li元素

    遍历选中的li节点
    $(".li-item").each(function(index){
        console.log(index);
        $(this).text(); ////获取当前元素的text值
        $(this).text("当前值为1"); ////修改当前元素的text值为1
        text 表示文本元素 ,html表示内部的html内容
        console.log("当前标签的text:"+$(this).text("当前的li内容为:"+(index+1)));
        console.log("当前标签的html:"+$(this).html("<a href='http://www.baidu.com'>当前的li内容为:"+(index+1)+"</a>"));
    });


    通过标签名选择标签元素
    $("ul").html() //输出ul节点内部的所有html内容
    $("ul").text() //输出ul节点内部的所有文本内容
    console.log(($("ul").text()))

    选择ul中所有的class="li-item"的li元素
    $("ul .li-item") //写法一
    $("li.li-teim")  //写法二

    /****
     * 通过在元素后面跟上[]的方式 实现属性选择
     */
    $("ul li[class!='li-item']") 选择ul中所有的class!="li-item"的li元素
    $("ul li[data-val]") 选择ul中所有的包含data-val的li元素
    $("input[name='']") 根据表单的name值选择元素
    $("li.li-item").css("color","red"); 为所有的class="li-item"的li设置颜色为红色
    $(".content").css("background-color","#6a6a79");为.content元素设置背景颜色

    ////原生js写法
    // document.getElementsByClassName("content")[0].style.backgroundColor = "blue";
});


 $("#block").toggle(2000); 设置元素的可见性(如果当前不可见那么置为可见，如果可见设置为不可见)
   ```
   ```
   当页面html中存在两个id相同的元素时,我们通过元素选择器获得的是第一个元素,对元素添加事件的时候,也是只有第一个元素有效果

    选中class="cur"的标签方法如下
    $(".cur");
    $(".nav-header .cur");
    $("nav .cur");
    $(".nav-header").find(".cur");  //在选中元素的基础上做查找

    通过eq选中指定索引位置的元素
    $(".nav-header li").eq(2);  //选中第三个li元素,eq选中指定索引位置(从0开始)的元素

    选中class="nav-header"的标签的所有子集(即标签开始结束位置中间)
    $(".section").children(); //选中的结果为nav标签
    $(".section nav").children(); //选中ul所有内容和两个a标签的所有内容
    $(".section nav").parent(); //返回父一级 选中section
    $(".section nav").parents(); //返回所有的父级  避免使用此方法

    //查找同一级的所有元素,不包含自己
    //对对象进行后续操作是js中最常见的写法
    $(".nav-header").find(".cur").siblings().css("color","red");

    找到和自己同级的下一个元素  紧挨自己的
    $(".nav-header").find(".cur").next().css("color","green");

    pre查找紧挨自己的 上一个同级元素
    $(".nav-header li").eq(3).prev().text("我是第三个元素")


    查找同级的紧挨自己的后续元素
    $(".nav-header").find(".cur").nextAll();

    查找同级的紧挨自己的前面元素
    $(".nav-header li").eq(3).prevAll().text("我是第四个元素前面的")

    查找class="content"的元素,对元素做each循环操作
    $(".content").each(function(){
    设置当前div的color值为当前div中h3标签的color值
     $(this).css("color",$(this).find("h3").css("color"));

     添加多个css样式的写法
      $(this).css({
         "font-size":"24px",
          "text-align":"center"
      })

    var text = $(this).find("h3").text(); //获取当前div中h3的文本内容
    遍历div中的class="articles"的元素,进行循环赋值
    $(this).find('.article-item').each(function(index){
         $(this).text(text+(index+1));
     })

     $(".article-item").addClass('article-title'); 添加样式
     $(".article-item").removeClass('article-title'); 删除样式

     $(window).width();//获取窗口的宽
     $(window).height();//获取窗口的高

     监听窗口大小改变的事件
     $(window).resize(function(){
        console.log('window is changing size....');
        console.log("width:"+$(window).width());
        console.log("width:"+$(window).height());
     })
 
   ```