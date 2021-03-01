# node.js的初始

#### 1.对于一些核心模块的初识

```javascript
hello word中的代码
fs是file-system的简写，就是文件系统的意思
在Node中如果想要对文件进行操作，就必须引入fs这个核心模块
在fs这个核心模块中，就提供了所有的文件操作相关的API

```

```javascript
对于fs模块的使用：
1.读文件
var fs=require('fs')
fs.readFile("./test.html",function (error,data) {
    console.log(data.toString())
})
对于readFile中的参数的说明：
第一个参数：文件路径
第二个参数：文件内容
第三个参数：回调函数

2.写文件
fs.writeFile('./你好.md','大家好，我是node.js',function (error) {
console.log('文件写入成功')
    console.log(error)
})
```

+ ##### 在这里说明一下，对于node.js来说，回调函数是一个非常重要的内容，基本每一个内容都需要添加回调函数，个人理解就是node.js是异步执行的，而且封装的比较好，所以我们就提供了回调函数这个借口来让我们能够实现自己的内容

#### 2.使用node来实现一个web服务器

```javascript
// 接下来使用node构建一个web服务器
// 在node中专门提供了一个核心模块：http
// 这个模块的职责就是帮你常见编写服务器的
// 1.加载http核心模块
var http=require("http")
// 2.使用http.createServer()方法常见一个web服务器
// 返回一个server实例
var server=http.createServer()
// 3.服务器的作用
// 提供服务：对数据的服务
// 发请求
// 接收请求
// 处理请求
// 给反馈(发送响应)
注册request请求时间
// 当客户端请求过来，就会自动触发服务器的request请求时间，然后执行第二个参数：回调处理函数
server.on('request',function (request,response) {
    // request请求对象，可以用来获取客户端的一些请求信息，比如路径
    // response响应对象，可以用来给客户端发送响应信息
    console.log('收到客户端的请求了'+request.url)
    // response对象有一个方法：write可以用来给客户端发送响应数据
    // write可以多次使用，但是最后一定要使用end来结束响应，否则客户端会一直等待
    response.write('hello')
    response.write(' node.js')
    response.end()  //告诉客户端我的话说完了
    response.end(' node.js')//或者用这种方式，直接发送完就结束了
})
// 绑定端口号，启动服务器
server.listen(3000,function () {
    console.log('服务器启动成功了，可以通过http://127.0.0.1:3000/来进行访问')

})
```

#### 3.对于node中的文件（或者说是模块的理解）

##### 模块使用过require方法来进行加载和执行的

```javascript
require方法有两个作用：
1.加载文件模块并执行里面的代码
2.拿到被加载文件模块导出的接口对象
```

##### 但是因为node的内部封装，仅仅使用require会使得模块中的代码会得到执行，但是外部模块无法访问到内部模块，同样内部模块也无法访问到外部模块，所以我们使用对象exports来解决这个问题

```javascript
//在每个文件中都有一个对象exports
exports默认是一个空对象（{}）
//你要做的就是把所有需要被外部访问的成员手动挂载到这个对象中
exports.foo='hello'
exports.add=function(x,y){return x+y}
```

#### 4.对于字符串的编码以及各式转换的一些问题

```javascript
JSON.stringify()       //实现一个json,将字符串转换为json
JSON.parse()        //解析json，将json转化为字符串

在数据流传输的时候需要指定编码的格式

res.setHeader('Content-type' , 'text/plain;charset=utf-8')
根据不同格式的文件来选择不同的Content-type，只有文本类型的文件需要指定编码的格式
下面是一个jpg格式的文件的指定方式
res.setHeader('Content-type','image/jpeg')
其他格式用到的可以直接上网查
```

