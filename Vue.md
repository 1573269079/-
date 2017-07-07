###vue

```
		<link href="https://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.css" rel="stylesheet">
		<script src="https://cdn.bootcss.com/jquery/3.2.1/jquery.js"></script>
		<script src="https://cdn.bootcss.com/bootstrap/3.3.7/js/bootstrap.js"></script>
		<script src="https://cdn.bootcss.com/vue/2.3.4/vue.js"></script>
		<script src="https://cdn.bootcss.com/vue-resource/1.3.4/vue-resource.js"></script>
```

1. 指令  v-model	一般表单元素(input)	双向数据绑定
2. 循环

	```
		v-for="name in arr"      {{$index}}
		v-for="name in json"     {{$index}}	  {{$key}}
		
		vue2.0以后移除了 $index 和 $key 这两个隐式声明变量。
		  v-for="(name,index) in json"
			{{index}}
			
		会有重复数据？
		track-by='索引'	提高循环性能
		track-by='$index/uid'
	```
	>eg
	
	```html
    <div id="box">
        <input type="button" value="添加" @click="add">
        <ul>
            <li v-for="val in arr" track-by="$index">
                {{val}}
            </li>
        </ul>
    </div>
	```
	```javascript
        var vm=new Vue({
            data:{
                arr:['apple','pear','orange']
            },
            methods:{
                add:function(){
                    this.arr.push('tomato');
                }
            }
        }).$mount('#box');
	```

3. 事件

	```JavaScript
		<input type="button" value="按钮" @click="show(index)"/>
		<input type="button" value="添加" @click="add(index)" />
	
		v-on:click="函数"
		v-on:click/mouseout/mouseover/dblclick/mousedown.....
		new Vue({
			el:'#box',
			data:{ //数据
			    arr:['apple','banana','orange','pear']
			},
			methods:{
				show:function(i){
					alert(this.arr[i])
				},
				add:function(j){ //添加
					this.arr.push(this.arr[j])
				}
			}
		});
		//显示隐藏:  v-show=“true/false”
		//事件对象: @click="show($event)"
		//阻止冒泡:  a). ev.cancelBubble=true;	b). @click.stop	
		//阻止默认行为: a). ev.preventDefault();	b). @contextmenu.prevent
		//键盘:	@keydown	$event	ev.keyCode	@keyup

		//常用键:
		//	回车  	a). @keyup.13	b). @keyup.enter
		//左		@keyup/keydown.left
		//右		@keyup/keydown.right
		//上		@keyup/keydown.up
		//下		@keyup/keydown.down
	```
	
4. 属性

	```
		v-bind:src=""  width/height/title....
	
		简写:  :src=""	推荐
		<img src="{{url}}" alt="">	效果能出来，但是会报一个404错误
		<img v-bind:src="url" alt="">	效果可以出来，不会发404请求
		
	class和style:
		:class=""	v-bind:class=""
		:style=""	v-bind:style=""
		:class="[red]"	red是数据
		:class="[red,b,c,d]"
		:class="{red:a, blue:false}"
		:class="json"
		data:{
			json:{red:a, blue:false}
		}
	style:
		:style="[c]"
		:style="[c,d]"   复合样式，采用驼峰命名法
		:style="json"
	```
	
	>css

	```html
    <div id="box">
    	//1
     	<strong :class="[red]">文字...</strong>
     	//2
     	<strong :class="[red,b]">文字...</strong>
     	//3
    	<strong :class="{red:true,blue:true}">文字...</strong>
    	//4
     	<strong :class="{red:a,blue:b}">文字...</strong>
     	//5
        <strong :class="json">文字...</strong>
    </div>

	```
	```css
        .red{
            color: red;
        }
        .blue{
            background: blue;
        }
	```
	```javascript
		//1
		window.onload=function(){
	            new Vue({
	                el:'#box',
	                data:{
	                    red:'red'
	                },
	                methods:{
	                }
	            });
	    };
        //2
		window.onload=function(){
	            new Vue({
	                el:'#box',
	                data:{
	                    red:'red',
	                    b:'blue'
	                },
	                methods:{
	                }
	            });
	    };
		//4
		window.onload=function(){
	            new Vue({
	                el:'#box',
	                data:{
	                    a:true,
	                    b:false
	                },
	                methods:{
	                }
	            });
	    };
		//5
		window.onload=function(){
	            new Vue({
	                el:'#box',
	                data:{
	                    json:{
	                        red:true,
	                        blue:true
	                    }
	                },
	                methods:{
	                }
	            });
	    };
	```
	
	>style
	
	```html
		<div id="box">
			//1
	        <strong :style="{color:'red'}">文字...</strong>
	        //2
	        <strong :style="[c]">文字...</strong>
	        // 3
	        <strong :style="[c,b]">文字...</strong>
	        //4
	         <strong :style="a">文字...</strong>
	    </div>
	```
	```css
	    .red{
	        color: red;
	    }
	    .blue{
	        background: blue;
	    }
	```
	```javascript
		//2
	    window.onload=function(){
	        new Vue({
	            el:'#box',
	            data:{
	                c:{color:'red'}
	            },
	            methods:{
	            }
	        });
	    };
	    //3
	    window.onload=function(){
	        new Vue({
	            el:'#box',
	            data:{
	                c:{color:'red'},
	                b:{backgroundColor:'blue'}
	            },
	            methods:{
	            }
	        });
	    };
	    //4
	    window.onload=function(){
	        new Vue({
	            el:'#box',
	            data:{
	                a:{
	                    color:'red',
	                    backgroundColor:'gray'
	                }
	            },
	            methods:{
	            }
	        });
	    };
	```

5. 模板

	```
		{{msg}}		数据更新模板变化
		{{*msg}}	数据只绑定一次
		{{{msg}}}	HTML转意输出
	```
	
6. 过滤器

	```
		{{msg| filterA}}
		{{msg| filterA | filterB}}

		uppercase	eg:	{{'welcome'| uppercase}}
		lowercase
		capitalize

		currency	钱

		{{msg| filterA 参数}}
	```
	```html
	<div id="box">
        {{'welcome'|uppercase}}  //转为大写
        {{'WELCOME'|lowercase}}  //专为小写
        {{'WELCOME'|lowercase|capitalize}} //首字母大写
        {{12|currency}} //12美元
        {{12|currency '￥'}} //12元
    </div>
	```
	
7. 交互

	```
	$http	（ajax）      引入: vue-resouce.js
	get:
		获取一个普通文本数据:
		this.$http.get('aa.txt').then(function(res){
		    alert(res.data);
		},function(res){
		    alert(res.status);
		});
		给服务发送数据:√
		this.$http.get('get.php',{
		    a:1,
		    b:2
		}).then(function(res){
		    alert(res.data);
		},function(res){
		    alert(res.status);
		});
	post:
		this.$http.post('post.php',{
		    a:1,
		    b:20
		},{
		    emulateJSON:true
		}).then(function(res){
		    alert(res.data);
		},function(res){
		    alert(res.status);
		});
	jsonp:
		https://sug.so.360.cn/suggest?callback=suggest_so&word=a
		https://sp0.baidu.com/5a1Fazu8AA54nxGko9WTAnF6hhy/su?wd=a&cb=jshow
		this.$http.jsonp('https://sp0.baidu.com/5a1Fazu8AA54nxGko9WTAnF6hhy/su',{
		    wd:'a'
		},{
		    jsonp:'cb'	//callback名字，默认名字就是"callback"
		}).then(function(res){
		    alert(res.data.s);
		},function(res){
		    alert(res.status);
		});
	```
	
8. vue生命周期:
	
	```
		钩子函数:
		created	->   实例已经创建	
		beforeCompile	->   编译之前
		compiled	->   编译之后
		ready		->   插入到文档中
		beforeDestroy	->   销毁之前
		destroyed	->   销毁之后
	```
	```html
	 <div id="box">
        {{msg}}
  	 </div>
	```
	```javascript
        var vm=new Vue({
            el:'#box',
            data:{
                msg:'well'
            },
            created:function(){
                alert('实例已经创建');
            },
            beforeCompile:function(){
                alert('编译之前');
            },
            compiled:function(){
                alert('编译之后');
            },
            ready:function(){
                alert('插入到文档中');
            },
            beforeDestroy:function(){
                alert('销毁之前');
            },
            destroyed:function(){
                alert('销毁之后');
            }
        });
        /*点击页面销毁vue对象*/
        document.onclick=function(){
            vm.$destroy();
        };
	```
	
9. v-html  &  v-text  &  v-cloak

	* v-cloak		防止闪烁, 比较大段落
	
		>  `<div class="reply" v-for="item in msgData" v-cloak></div>`
	* v-html
	
		```
	    <div id="box">
        	<span>{{{msg}}}</span>
        	<span v-html="msg"></span>
    	</div>
   		<script>
		    new Vue({
		        el:'#box',
		        data:{
		            msg:'<strong>welcome</strong>'
		        }
		    });
    	</script>
		```
	* v-text
	
		```
	    <div id="box">
        	<span>{{msg}}</span>
        	<span v-text="msg"></span>
	    </div>
	    <script>
	        new Vue({
	            el:'#box',
	            data:{
	                msg:'welcome'
	            }
	        });
	    </script>
		```
10. 计算属性的使用

	```
	computed:{
		b:function(){	//默认调用get
			return 值
		}
	}
	computed:{
		b:{
			get:
			set:
		}
	}
	* computed里面可以放置一些业务逻辑代码，一定记得return
	```
	>eg
	
	```html
    <div id="box">
        a => {{a}}
        <br>
        b => {{b}}
    </div>
	```
	```javascript
	//1
    var vm=new Vue({
        el:'#box',
        data:{
            a:1
        },
        computed:{
            b:function(){
                //业务逻辑代码
                return this.a+1;
            }
        }
    });
    document.onclick=function(){
        vm.a=101;
    };
    //2
    var vm=new Vue({
        el:'#box',
        data:{
            a:1
        },
        computed:{
            b:{
                get:function(){
                    return this.a+2;
                },
                set:function(val){
                    this.a=val;
                }
            }
        }
    });
    document.onclick=function(){
        vm.b=10;
    };
	```
11. vue实例简单方法

	```
	vm.$el	->  就是元素
	vm.$data  ->  就是data
	vm.$mount ->  手动挂在vue程序
	vm.$options	->   获取自定义属性
	vm.$destroy	->   销毁对象
	vm.$log();	->  查看现在数据的状态
	```
	>eg
	
	```html
	//1
    <div id="box">
        {{a}}
    </div>
    //2
    <div id="box">
        <span v-text="a"></span>
    </div>
    //3
    <div id="box">
        <span v-text="a"></span>
        <br>
        {{aa}}
    </div>
    //4
    <div id="box">
        <span v-text="a"></span>
    </div>
	```
	```javascript
	//1
        var vm=new Vue({
            el:'#box',
            data:{
                a:1
            }
        });
        vm.$el.style.background='red';
        
        var vm=new Vue({
            el:'#box',
            data:{
                a:1
            }
        });
        console.log(vm.$data.a);
    //2 
        var vm=new Vue({
            data:{
                a:1
            }
        }).$mount('#box');
    //3
        var vm=new Vue({
            aa:11, //自定义属性,
            show:function(){
                alert(1);
            },
            data:{
                a:1
            }
        }).$mount('#box');
        vm.$options.show();
        console.log(vm.$options.aa);
    //4
        var vm=new Vue({
            data:{
                a:1,
                b:2
            }
        }).$mount('#box');
        console.log(vm.$log());
	```
	
12. 过滤器

	* vue提供过滤器:
		```
		capitalize	uppercase	currency....
		debounce	配合事件，延迟执行
		```
		>eg(debounce)
		
		```
	    <div id="box">
        	<input type="text" @keyup="show | debounce 2000">
    	</div>
    	<script>
	        var vm=new Vue({
	            data:{
	            },
	            methods:{
	                show:function(){
	                    alert(1);
	                }
	            }
	        }).$mount('#box');
    	</script>
		```
	* filterBy	过滤数据
	
		```
	    <div id="box">
        	<input type="text" v-model="a">
	        <ul>
	            <li v-for="val in arr | filterBy a">
	                {{val}}
	            </li>
	        </ul>
    	</div>
    	<script>
	        var vm=new Vue({
	            data:{
	                arr:['width','height','background','orange'],
	                a:''
	            },
	            methods:{
	            }
	        }).$mount('#box');
    	</script>
		```
	* limitBy 参数(取几个)
	
		```
	    <div id="box">
        <ul>
            <li v-for="val in arr | limitBy 2 arr.length-2">  //第一个参数取几个，第二个参数从什么地方开始
                {{val}}
            </li>
        </ul>
	    </div>
	    <script>
	        var vm=new Vue({
	            data:{
	                arr:[1,2,3,4,5]
	            },
	            methods:{
	            }
	        }).$mount('#box');
	    </script>
		```
	* orderBy	排序
	
		```
	    <div id="box">
	        <input type="text" v-model="a">
	        <ul>
	            <li v-for="val in arr | orderBy a">
	                {{val}}
	            </li>
	        </ul>
	    </div>
	    <script>
	        var vm=new Vue({
	            data:{
	                arr:['width','height','background','orange'],
	                a:''
	            },
	            methods:{
	            }
	        }).$mount('#box');
	    </script>
		```
		
13. 	自定义过滤器

		```
		 model ->过滤 -> view
		Vue.filter(name,function(input){});
		```
		>eg
		
		```
		//1
		<div id="box">
        	{{a | toDou}}   ||  {{a | toDou 1 2}}
    	</div>
    	<script>
	        Vue.filter('toDou',function(input || input,a,b){
	            || alert(a+','+b);
	            return input<10?'0'+input:''+input;
	        });
	        var vm=new Vue({
	            data:{
	                a:9
	            },
	            methods:{
	            }
	        }).$mount('#box');
        </script>
        //2
        <div id="box">
        {{a | date}}
	    </div>
	    <script>
	        Vue.filter('date',function(input){
	            var oDate=new Date(input);
	            return oDate.getFullYear()+'-'+(oDate.getMonth()+1)+'-'+oDate.getDate()+' '+oDate.getHours()+':'+oDate.getMinutes()+':'+oDate.getSeconds();
	        });
	        var vm=new Vue({
	            data:{
	                a:Date.now()
	            },
	            methods:{
	            }
	        }).$mount('#box');
	    </script>
	    
	    //3
        <div id="box">
	        <input type="text" v-model="msg | fiterHtml">
	        <br>
	        <div v-html="msg"></div>
    	</div>
	    <script>
	        Vue.filter('fiterHtml',function(input){
	            return input.replace(/<[^<]+>/g,'');//正则替换 找到所有的<>的标签,都替换为空格
	        });
	        var vm=new Vue({
	            data:{
	                msg:'<strong>welcome</strong>'
	            },
	            methods:{
	            }
	        }).$mount('#box');
	    </script>
		```
		> 双向过滤器
		
		```
		Vue.filter('filterHtml',{
            read:function(input){ //model-view
                return input.replace(/<[^<+]>/g,'');
            },
            write:function(val){ //view -> model
                return val;
            }
		});
		数据 -> 视图
		model -> view
		view -> model
		```		
		
14. 自定义指令

	```
	属性:
		Vue.directive(指令名称,function(参数){
			this.el	-> 原生DOM元素
		});
		<div v-red="参数"></div>
		指令名称: 	v-red  ->  red
		* 注意: 必须以 v-开头
	```
	>eg
	
	```
	//1
    <div id="box">
        <span v-red>asdfasd</span>
    </div>
    Vue.directive('red',function(){
        this.el.style.background='red';
	});
 	window.onload=function(){
        var vm=new Vue({
            el:'#box',
            data:{
                msg:'welcome'
            }
        });
    };
    //2
    <div id="box">
        <span v-red="a">asdfasd</span>
    </div>
    <script>
        Vue.directive('red',function(color){
            this.el.style.background=color;
        });
        window.onload=function(){
            var vm=new Vue({
                el:'#box',
                data:{
                    a:'blue'
                }
            });
        };
    </script>
    //3
    <div id="box">
        <span v-red="'blue'">asdfasd</span>
    </div>
    Vue.directive('red',function(color){
        this.el.style.background=color;
    });
    window.onload=function(){
        var vm=new Vue({
            el:'#box'
        });
    };
    //4
    <div id="box">
        <span v-red>asdfasd</span>
    </div>
    Vue.directive('red',{
        bind:function(){
            this.el.style.background='red';
        }
    });
    window.onload=function(){
        var vm=new Vue({
            el:'#box'
        });
    };
    
    
    //拖拽
    <div id="box">
        <div v-drag :style="{width:'100px', height:'100px', background:'blue', position:'absolute', right:0, top:0}"></div>
        <div v-drag :style="{width:'100px', height:'100px', background:'red', position:'absolute', left:0, top:0}"></div>
    </div>
    Vue.directive('drag',function(){
        var oDiv=this.el;
        oDiv.onmousedown=function(ev){
            var disX=ev.clientX-oDiv.offsetLeft;
            var disY=ev.clientY-oDiv.offsetTop;
            document.onmousemove=function(ev){
                var l=ev.clientX-disX;
                var t=ev.clientY-disY;
                oDiv.style.left=l+'px';
                oDiv.style.top=t+'px';
            };
            document.onmouseup=function(){
                document.onmousemove=null;
                document.onmouseup=null;
            };
        };
    });
    window.onload=function(){
        var vm=new Vue({
            el:'#box',
            data:{
                msg:'welcome'
            }
        });
    };
	```
	
15. 自定义键盘信息

	```
	//按字母c时，触发
    <div id="box">
        <input type="text" @keydown.c="show">  
    </div>
    window.onload=function(){
        var vm=new Vue({
            el:'#box',
            data:{
                a:'blue'
            },
            methods:{
                show:function(){
                    alert(1);
                }
            }
        });
    };
    //按回车键或者Ctrl键触发
    <div id="box">
        <input type="text" @keydown.myenter="show">
    </div>
    /*document.onkeydown=function(ev){
        console.log(ev.keyCode);
    };*/
    Vue.directive('on').keyCodes.ctrl=17; 
    Vue.directive('on').keyCodes.myenter=13;
    window.onload=function(){
        var vm=new Vue({
            el:'#box',
            data:{
                a:'blue'
            },
            methods:{
                show:function(){
                    alert(1);
                }
            }
        });
    };
	```
	
16. 监听数据变化

	```
	vm.$el/$mount/$options/....
	vm.$watch(name,fnCb);  //浅度
	vm.$watch(name,fnCb,{deep:true});  //深度监视 
	```
	```
    <div id="box">
        {{a}}
        <br>
        {{b}}
    </div>
    window.onload=function(){
	    var vm=new Vue({
	        el:'#box',
	        data:{
	            a:111,
	            b:2
	        }
	    });
        vm.$watch('a',function(){
            alert('发生变化了');
            this.b=this.a+100;
        });
        document.onclick=function(){
            vm.a=1;
        };
    };
	```
	```
    <div id="box">
        {{json | json}}
        <br>
        {{b}}
    </div>
    window.onload=function(){
	    var vm=new Vue({
	        el:'#box',
	        data:{
	            json:{name:'strive',age:16},
	            b:2
	        }
	    });
	    vm.$watch('json',function(){
	        alert('发生变化了');
	    },{deep:true});
	    document.onclick=function(){
	        vm.json.name='aaa';
	    };
	};
	```