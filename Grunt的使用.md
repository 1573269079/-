1. npm install -g grunt-cli
上述命令执行完后，grunt 命令就被加入到你的系统路径中了，以后就可以在任何目录下执行此命令了。
2. npm init命令创建一个基本的package.json文件。
安装以下插件,可以根据需要做补充;
     ```
     "grunt": "~0.4.5",
    "grunt-contrib-jshint": "~0.10.0",
    "grunt-contrib-nodeunit": "~0.4.1",
    "grunt-contrib-uglify": "~0.5.0"
    如果以上的4个存在package.json文件中,则只需要在命令窗口输入: npm install  安装存在于package.json文件中的所有依赖项
    也可以在命令行输入以下命令安装所需要的插件:
    npm install grunt  --save
    npm install grunt-contrib-jshint  --save
    npm install grunt-contrib-nodeunit  --save
    npm install grunt-contrib-uglify   --save
     ```
3. 新建Gruntfile.js文件,和package.json文件在同一目录层级
     以下为Gruntfile.js文件的内容
     ```
     module.exports = function (grunt) {

     grunt.initConfig({
        pkg: grunt.file.readJSON('package.json'),
        /////代码合并
        concat:{
            foo:{
                files:[
                    //需要合并的文件:合并后的文件  
                    {src:['src/index.js','src/login.js'],dest:'build/build-login.js'},
                    {src:['src/index.js','src/reg.js'],dest:'build/build-reg.js'}
                ]
            }
            
        },
        uglify: {
            options: {
                // 此处定义的banner注释将插入到输出文件的顶部
                banner: '/*! <%= pkg.name %> <%= grunt.template.today("dd-mm-yyyy") %> */\n',
                ////是否生成min.js.map
                sourceMap: true,
                footer: '\n/*这是一个grunt的demo，压缩后的底部*/',
                mangle:true, ////是否混淆变量名
                preserveComments:true /////是否删除注释
            },
            dist: {
              
                // 此处对多个js文件进行压缩，用数组表示,
                //对象数组的第一个参数是压缩后的文件名
                //对象数组的第二个参数是需要压缩的文件名
                files:[
                    {'build/build-login.min.js':'build/build-login.js'},
                    {'build/build-reg.min.js':'build/build-reg.js'}
                ]
            }
        },
        jshint: {
            options: {
                /////代码中使用的一些第三方插件
                //循环或者条件语句必须使用花括号包围
                curly:true,
                //////兼容低级浏览器
                es3: false,
                /////禁止重写原生对象的原型如Date,Array
                freeze: true,
                ////禁止定义之前使用变量，忽略 function 函数声明
                latedef: "nofunc",
                //////构造器函数首字母大写
                newcap: true,
                /////为 true 时，禁止单引号和双引号混用
                "quotmark": false,
                /////变量未定义
                "undef": false,
                /////变量未使用
                "unused": false,
                globals: {
                    //jQuery: true
                }
            },
            ////需要测试的代码
            files: ['Gruntfile.js', 'src/*.js']
        },
        cssmin:{
            target: {
                files: {
                    ///// 目标文件 : 源文件数组 
                'build/css/build.css': ['src/css/login.css', 'src/css/reg.css']
                }
            }
        },
        watch:{
			 // 监视一组文件，当文件变化时执行相应的动作或任务
            scripts: {
                // 被监视的文件  
                files: ['Gruntfile.js', 'package.json', 'src/*.js','src/css/*.css'],
                // 当文件变化时要执行任务
                tasks: ['default']
            }
		}	
    });

    ////注册一个代码测试的任务
    grunt.loadNpmTasks('grunt-contrib-jshint');

    ////注册一个合并代码的任务
    grunt.loadNpmTasks('grunt-contrib-concat');

    /////对代码进行压缩
    grunt.loadNpmTasks('grunt-contrib-uglify');

    /////压缩css文件
    grunt.loadNpmTasks('grunt-contrib-cssmin');

    ////watch插件
    grunt.loadNpmTasks('grunt-contrib-watch');

    // 默认被执行的任务列表。
    grunt.registerTask('default', ['jshint', 'concat', 'uglify','cssmin','watch']);

};
     ```