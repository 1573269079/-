### 函数中的this四种绑定方式

1. this的默认绑定

	```javascript
	/*
	 * 当一个函数没有明确的调用对象的时候，也就是单纯作为独立函数调用的时候，
	 * 将对函数的this使用默认绑定：绑定到全局的window对象
	 */
	//eg1:
	function fire(){
		console.log(this === window)
	}
	fire();//输出true
	
	//eg2:函数 innerFire在一个外部函数fire里面声明且调用，它的this是指向仍然是window
	function fire(){
		//定义在函数内部的函数
		function innerFire(){
			console.log(this === window)
		}
		innerFire();//独立函数调用
	}
	fire();//输出true
	
	//eg3:obj.fire()的调用实际上使用到了this的隐式绑定
	var obj = {
		fire:function(){
			function innerFire(){
				console.log(this === window)
			}
			innerFire();//独立调用函数
		}
	}
	obj.fire();//true
	
	* 函数作为独立函数调用，无论它的位置在哪里，它的行为表现，都和直接在全局环境中调用无异
	```
	
2. this的隐式绑定

	```javascript
	/*
	 * 当函数被一个对象“包含”的时候，我们称函数的this被隐式绑定到这个对象里面了，
	 * 这时候，通过this可以直接访问所绑定的对象里面的其他属性
	 */
	//eg1:
	var obj = {
		a:1,
		fire:function(){
			console.log(this.a)
		}
	}
	obj.fire(); //  1
	
	// eg2-1:
	function fire(){
		console.log(this.a);
	}
	var obj = {
		a:1,
		fire:fire
	}
	obj.fire();    // 1
	
	//eg2-2:
	var obj = {
		a:1,
		fire:function(){
			console.log(this.a)
		}
	}
	obj.fire();    // 1
	/*
	 * fire函数并不会因为它被定义在obj对象的内部和外部而有任何区别，
	 * 在上述隐式绑定的两种形式下，fire通过this还是可以访问到obj内的a属性
	 * this是动态绑定的，或者说是在代码运行期绑定而不是在书写期
	 * 函数于对象的独立性， this的传递丢失问题
	 */
	//eg3:
	var obj = {
		a:1,  // a是定义在对象obj中的属性        1
		fire:function(){
			console.log(this.a)
		}
	}
	var  a = 2; //a是定义在全局环境中的变量      2
	var fireInGrobal = obj.fire;
	fireInGrobal();   //  2
	obj中的fire函数的引用（ fireInGrobal）在调用的时候，
	行为表现（输出）完全看不出来它就是在obj内部定义的，
	其原因在于：我们隐式绑定的this丢失了！！
	 从而 fireInGrobal调用的时候取得的this不是obj，而是window
	 
	 //eg4:
	 var a = 2;
	 var obj = {
	 	a:1,   // a是定义在对象obj中的属性
	 	fire:function(){
	 		console.log(this.a)
	 	}
	 }
	 function otherFire(fn){
	 	fn();
	 }
	 otherFire(obj.fire);  //输出    2
	 在上面，我们的关键角色是otherFire函数，它接受一个函数引用作为参数，
	 然后在内部直接调用，但它做的假设是参数fn仍然能够通过this去取得obj内部的a属性，
	 但实际上, this对obj的绑定早已经丢失了，所以输出的是全局的a的值(2),而不是obj内部的a的值（1）
	 
	* 在一串对象属性链中，this绑定的是最内层的对象
	var obj = {
		a:1,
		obj2:{
			a:2,
			obj3:{
				a:3,
				getA:function(){
					console.log(this.a)
				}
			}
		}
	}
	obj.obj2.obj3.getA();    //  3
	```
	
3. this的显示绑定（call和bind方法）

	```javascript
	call的基本使用方式： fn.call(object)
	fn是你调用的函数，object参数是你希望函数的this所绑定的对象。
	fn.call(object)的作用：
	1.即刻调用这个函数（fn）
	2.调用这个函数的时候函数的this指向object对象
	
	var obj = {
		a:1,  // a是定义在对象obj中的属性
		fire:function(){
			console.log(this.a);
		}
	}
	var a = 2; // a是定义在全局环境中的变量
	var fireInGrobal = obj.fire;
	fireInGrobal();  //  2
	fireInGrobal.call(obj);  // 1
	原本丢失了与obj绑定的this参数的fireInGrobal再次重新把this绑回到了obj
	在fireInGrobal.call(obj)外面包装一个函数,能够一次性 返回一个this被永久绑定到obj的fireInGrobal函数，
	这样我们就不必每次调用fireInGrobal都要在尾巴上加上call
	
	//eg:
	var obj = {
		a:1,
		fire:function(){
			console.log(this.a)
		}
	}
	var a = 2;  // a是定义在全局环境中的变量
	var fn = obj.fire;
	var fireInGrobal = function(){
		fn.call(obj)  //硬绑定
	}
	fireInGroball();   // 1
	
	//使用bind
	var fireInGrobal = function(){ fn.call(obj) //硬绑定 }
	简化为：
	var fireInGrobal = fn.bind(obj);
	
	call和bind的区别是：在绑定this到对象参数的同时：
	1.call将立即执行该函数
	2.bind不执行函数，只返回一个可供执行的函数
	```
	
4. new 绑定

	```javascript
	执行new操作的时候，将创建一个新的对象，并且将构造函数的this指向所创建的新对象
	function foo (a) {
	     this.a = a;
	}
	  
	var a1  = new foo (1);
	var a2  = new foo (2);
	var a3  = new foo (3);
	var a4  = new foo (4);
	  
	console.log(a1.a); // 输出1
	console.log(a2.a); // 输出2
	console.log(a3.a); // 输出3
	console.log(a4.a); // 输出4
	```