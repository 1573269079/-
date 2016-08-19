## vuejs   (vue.min.js    jquery.min.js)

###  Hello Word

```JavaScript
        <div id="app">
           {{message}}
        </div> 


        new Vue({
            el:'#app',
            data:{
                message:'Hello Vue.js!'
            }
        })
```
 
### Two-way Binding(双向绑定)  

```JavaScript
    <div id="app">
       <p>{{message}}</p>
       <input v-model="message">
    </div>
    
    new Vue({
       el:"#app",
       data:{
          message:'Hello Vue.js'
       }
    })
```
### Render a List(渲染列表)
```JavaScript
   <div id="app">
      <ul>
         <li v-for="todo in todos">
            {{todo.text}}
         </li>
      </ul>
   </div>
   
   
   new Vue({
      el:"app",
      data:{
        todos:[
          {text:'learn JavaScript'},
          {text:'learn Vue.js'},
          {text:'learn JavaScript'}
        ]
      }
   })
```
### Handle User Input(用户输入处理)

```JavaScript
    //  输出结果变为倒叙输出(点击按钮后触发)
   <div id="app">
       <p>{{message}}</p>
       <button v-on:click="reverseMessage">Reverse Message</button>
   </div>
   
   new Vue({
     el:'#app',
     data:{
       message:'hello Vue.js!'
     },
     methods:{
       reverseMessage:function(){
          this.message = this.message.split('').reverse().join('')
       }
     }
   })
   
   
   // 添加/删除操作
   <div class="main" id="app">
     <div class="list">
        <label for="" class="item item-input">
        <span class="input-label">姓名</span>
        <input type="text" v-model="name">
    </label>
        <label for="" class="item item-input">
            <span class="input-label">年龄</span>
            <input type="text" v-model="age">
        </label>
        <button class="button button-full button-positive" v-on:click="addFun">添加</button>
    </div>
    <div class="list">
        <a class="item" v-for="student in students">
            {{student.name}}(今年{{student.age}}岁)
            <button v-on:click="removeStudent($index)" style="float: right">X</button>
        </a>
    </div>
   </div>
    
    new Vue({
    el:'#app',
    data:{
        message:'hello Vue.js',
        students:[
            {name:"小明",age:18},
            {name:"小红",age:17},
            {name:"小强",age:19},
            {name:"tom",age:20}
        ]
    },
    methods:{
        addFun:function (e) {
            // alert(this.name);
            if(!!this.name){
                var obj={};
                obj.name=this.name;
                obj.age=this.age;
                this.students.push(obj);
            }
        },
        removeStudent:function (index) {
            this.students.splice(index,1);
        }
    }
  });
```
