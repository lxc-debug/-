## 关于node.js的进阶使用

#### 1.express模块的使用

```javascript
1.安装
npm init -y
npm install -Save express		//npm已经升级了，可以不加-Save选项也可以进行存储
2.代码的编写
var express = require('express')

var app=express()		//示例化一个对象

app.get('/',function(req,res){		//不用作判断使代码美观
	res.end('hello world')	//不推荐，但是可以使用
	res.send('hello world')		//express模块更推荐使用这种方式
	
}

app.listen(3000,function(){		//绑定监听端口
    console.log('express app is running')

})
```

```javascript
3.nodemon
这是一个第三方工具包，每按一次ctrl+s就会重新启动服务。
通过nodemon启动的服务，他会监视你的文件变化，当文件发生变化的时候，会帮你自动重启服务。

4.创建基本路由
5.创建开放资源
app.use('/public/',express.static('./public/'))	//当检查到url以public开头的时候，就会到这个文件下去查找，公开了整个文件夹
当使用下面的方法时，a就相当于public的别名
app.use('/a/',express.static('./public/'))
	//这里的use是一个中间件，，后续的static函数是express自带的中间件的函数，后续还会使用到其他的中间件函数
```

#### 2.在express中配置使用art-template模板引擎

```javascript
1）安装art-template,express-art-template
npm install -S art-template
npm install -S express-art-template
2)进行配置
app.engine('art',require('express-art-template'))
//这里的第一个参数是确定待渲染文件的后缀名，一般用html
3)使用方法
res.render('html模板名',{模板数据})
//模板名的后缀名必须与engine中定义的后缀名相同
//第一个参数不能写路径，默认回去项目中的views目录去查找该模板文件
//也就是说Express有一个约定：开发人员把所有的视图文件都放到views中
app.set('views',render函数的默认路径）//这个函数可以更改默认的文件路径，但一般不会使用，就用默认的views就可以
```

+ ##### 使用的方式

```javascript
app.get('/pinglun',function(req,res){
	var comment = req.query
	comment.dataTime='2017-11-5 10:58:51'
	comments.unshift(comment)	//这里是数组的头插法
	res.redirect('/')	//这里是重定向到首页
//相当于下面两行代码
//	res.statusCode=302
//	res.setHeader('location','/')
})

```

#### 3.路由模块的创建与使用

+ ##### 在实际的工程中，我们为了使代码清晰简洁，通常会进行分模块编写，这样每个模块的功能就会更加的单一化，更方便与其他模块的调用。

```javascript
创建路由模块
1.创建一个新的文件
2.express提供了一个专门用来包装路由的方式
var express=require('express')
3.创建一个路由容器
var router = express.Router()
4.导出路由容器
module.exports=router
5.把路由挂载到router路由器容器中
把以前类似于app.get的方法改变成router.get
6.在起始文件中引入,把路由器挂载到app服务中
app.use(router)
//因为use中间件的调用方式，这里只能传入函数，所以这里的router个人推测应该是一个函数对象，里面封装了其他的函数。
```

#### 4.回调函数

+ ##### 因为在Node.js中程序的执行大多是异步的，所以为了让他们执行完在执行某一特定的函数，我们这里引入了回调函数

```javascript
创建回调函数
exports.find=function(callback){
	fs.readFile(dbPath,'utf8',function(err,data){
		if(err){
			return callback(err)
		}
		callback(null,JSON.parse(data).students)
	})
}
//在这里callback函数就是一个回调函数，调用这个find函数的时候穿的参数是一个匿名函数，这个方法就可以让异步执行的函数在执行完成之后调用这个函数来向主程序中进行参数传递
find(function(err,students){
    console.log(students);
})
//这里就是回调函数，在调用的时候定义函数，在方法定义的地方执行。上方定义，下方执行
```

#### 5.解析post请求所需要进行的配置

+ ##### 在对post请求进行解析的时候，我们需要引入一个中间件的配置

```javascript
创建解析post请求的配置
app.use(bodyParser.urlencoded({extended:false}))
app.use(bodyParser.json())

```

#### 6.对于数据库的操作，MongoDB

+ ##### 对于MongoDB的初识，定义

  ```javascript
  MongoDB是长得最像关系型数据库的非关系数据库
  
  数据库=》数据库
  数据表=》集合（数组）
  表记录=》文档对象
  
  MongoDB不需要设计表结构
  也就是可以任意往里面存数据，没有结构性这么一说
  ```

+ ##### 对于MongoDB的操作流程

  ```javascript
  //设计Schema发布module
  var mongoose = require('mongoose')
  
  var Schema=mongoose.Schema
  
  mongoose.connect('mongodb://locolhost/itcast')//这个是连本机的MongoDB，连接itcast这个库
  
  var userSchema=new Schema({	//创建表的样式
  	username:{
  		type:String,
  		required:true},
  	password:{
  		type:String,
  		required:true},
  	email:{
  		type:String}
  })			//这里的操作就像是在MySQL中的建表操作
  /*
  mongoose.model方法就是用来将一个架构发布为model
  第一个参数：传入一个大写名词单数字符串用来表示你的数据库名后这时
  	mongoose会自动将大写名词的字符串生成小写复数的集合名称
  	例如这里的User最终会变成users集合名称
  第二个参数：架构Schena
  返回值：模型构造函数
  */
  var User = mongoose.model('User',userSchema)	
  //这里的User就可以直接调用函数了
  //直接导出模型构造函数
  module.exports=mongoose.model('Student',studentSchema)
  //第一个参数是集合的名字
  ```

+ #### 对于MongoDB的操作，增删改查

  ```javascript
  //增加数据
  
  var admin = new User({
  	username:'admin',
  	password:'123456',
  	email:'admin@admin.com'
  })
  
  admin.save(function(err,ret){
  	if(err){
  	console.log('save err')}
  	else{
  	console.log('save success')}
  
  
  //查询数据(这里是进行整张表的查找)
  User.find(function(err,ret){
  	if(err){
  		console.log('查询失败')}
  	else{
  		console.log(ret)}
  })
  //根据参数进行查找
  User.find({username:'zs'}
  	,function(err,ret){
  	if(err){
  		console.log('查询失败')}
  	else{
  		console.log(ret)}
  })
  //查找单个
  User.findOne({username:'zs'}
  	,function(err,ret){
  	if(err){
  		console.log('查询失败')}
  	else{
  		console.log(ret)}
  })
  
  
  //
  User.remove({username:'zs'}
  	,function(err,ret){
  	if(err){
  		console.log('删除失败')}
  	else{
  		console.log(ret)}
  })
  
  //更新
  User.findByIdAndUpdate(这里是id值,{password:'123'},
  	function(err,ret){
  		if(err){
  		console.log('更新失败')}
  		else{
  		console.log('更新成功')}
  }）
  ```

  

#### 7.Node.js对于MySQL数据库的操作

##### 以下是使用方法

```javascript
var mysql=require('mysql')		

var connection=mysql.createConnection({		//创建连接
host:'localhost',
user:'me',
password:'secret',
database:'my_db'
})

connection.connect()	//连接数据库

connection.query('sql语句',function(err,results,fields){		//执行数据操作
	if(err)throw err;
	console.log('The solution is:',results)
})

connection.end()		//关闭连接
```

#### 8.path模块

+ ##### 类似于python中的path模块是用来对于路径进行的操作

```javascript
path模块
//专门用来操作路径
path.basename()	//获取文件的名字
path.dirname()	//获取目录的名字
path.extname()	//获取扩展名
path.isAbsolute()	//判断是不是绝对路径
path.parse()	//解析路径
path.join('','')	//路径的拼接

__dirname	//当前文件夹的绝对路径
__filename	//当前文件的绝对路径
//不受执行node命令所属路径影响的
//文件路径会受node命令位置的影响，模块就是相对于文件路径的，所以不受影响

```

#### 9.HTML的复用

```javascript
{{include './header.html'}}	//可以对其他html文件进行引用，公共的头部和公共的尾部

{{block 'content'}}
<h1>默认内容</h1>
{{/block}}			//挖一个坑

{{extend 'layout.html'}}	//继承上方模板
{{block 'content'}}
<h1>更新内容</h1>
{{/block}}
孩子可以通过改写block来进行重写（填坑）

使用md5进行加密
在GitHub上找包
```

