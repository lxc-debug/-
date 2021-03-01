## HTML语言

#### 1.域名解析

```html
域名 -- IP地址 -- 192.168.1.10

https://192.168.1.10.80  -- www.jd.com  --DNS解析 {‘www.jd.com':'192.168.1.10'}
```



#### 2.请求和相应

```html
请求：浏览器socket客户端给服务端发送信息

相应：服务器socket给客户端回信息
```



#### 3.标签

```html
Html标签：超文本标记语言，就是标记用的
必须是封闭的
	自封闭		<meta>
	完全闭合	<h1></h1>
标签属性  id='xx'  value='xxx'
<h1 id='xx' value='xx'></h1>
```



#### 4.标签的分类

```html
两类
1.内敛标签
	不独占一行，内敛标签只能嵌套内敛标签		b\i\u\s\button\span\img\a
2.块级标签
	独占一行，可以嵌套内敛标签和某些块级标签		\h1~h6\br\hr\p\div
	<!--p和div的区别就是p的上下会用空行，而div没有,p和div的区别就是p的上下会用空行，而div没有-->
```



#### 5.head中的标签

```html
<title id='1'>22期皇家赌场</title>		定义网页的标题

<meta charset='utf-8'>	#定义网页信息\配置信息
```



#### 6.body标签中的基本标签

```html
<b></b>			加黑
<i></i>			斜体
<u></u>			下划线
<s></s>			中间加一条横线

<h1></h1>
<h2></h2>
<h3></h3>
<h4></h4>
<h5></h5>
<h6></h6>		不同的字体大小

<br>		<!--换行-->

<hr>		<!--换行，且在换行出加一整条横线-->

```



#### 7.img标签以及a超链接标签

```html
1.img标签
属性 src='图片路径'		图片路径可以使相对路径或者是网络地址中的绝对路径
示例：
	<img src='1.jpg' alt='这是个美女，请稍等' title='美女' width='200' heiget='200'>

2.a标签
属性
href:	超链接的地址
target='_blank'		点击超链接后会自动生成一个新的页面
target='_self'		会在原始页面打开超链接
示例：
	<a href='https://www.baidu.com' target='_blank'>百度页面</a>
	<!--百度页面就是在网页是显示的超链接的内容-->
```



#### 8.列表标签

```html
1.无序列表
<ul type='clrcle'>		<!--type还有square,none,以及一个默认的-->
    <li>太白</li>
    <li>景女神</li>
    <li>alexsb</li>
</ul>

2.有序列表
<ol type='1' start='1'>		<!--type可以决定使用数字，字母，还是罗马数字进行标号，									start决定是从几开始-->
    <li>太白</li>
    <li>景女神</li>
    <li>alexsb</li>
    
</ol>
```



#### 9.特殊字符

```html
&nbsp;	空格
&lt;	小于号
&gt;	大于号
&amp;	&符号
```



#### 10.表格标签

```html
table
	cellpadding:文字和内边框的距离
	cellspacing:内边框和外边框的距离
	border:边框宽度

<table border='1' cellpadding='10' cellspacing='20'>
    <thead>
    	<tr>
        	<th>姓名</th>
            <th>年龄</th>
            <th>爱好</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        	<tb>b哥</tb>
            <tb>40</tb>
            <tb>炒鸡蛋</tb>
        </tr>
        <tr>
        	<tb>大壮</tb>
            <tb>38</tb>
            <tb>抽烟喝酒烫头</tb>
        </tr>
    </tbody>
</table>
```



#### 11.form标签（重要）

+ ##### form标签是用来提交用户数据的

  ```html
  action:指定数据的提交路径
  input标签：
  	type标签：控制输入框的样式
  	name标签：分组，携带数据的key		key：value
  	value标签：选择框提交数据的时候的值，输入框的默认值
  
  <form action='http://127.0.0.1:8001'>
      用户名：<input type='text' name='username' value='dazhuang'>
      密码：<input type='password' name='password' value='111'>
      
      <input type='radio' name='sex' value='1'>男
      <input type='radio' name='sex' value='2'>女
      
      <input type='checkbox' name='hobby' value='a'>喝酒
      <input type='checkbox' name='hobby' value='b'>抽烟
      <input type='checkbox' name='hobby' value='c'>烫头
      <input type='submit'>
      <hr>
      <input type='date'>
      <input type='button' value='普通按钮'>
  </form>
  ```

  ```html
  几种特殊的input的type形式：
  date:日期的输入框
  reset:重置按钮，页面不会刷新，经所有输入的内容清空
  hidden:隐藏输入框
  file:文件选择框
  ```



#### 12.select标签   下拉选择框

```html
单选
	<select name='city'>
        <option value='1'>北京</option>
        <option value='2'>上海</option>
        <option value='3'>深圳</option>	#这个和radio不同，如果不写value会返回北京，上海以及深圳中的某一个值
</select>

多选
	<select name='city' multiple>
        <option value='1'>北京</option>
        <option value='2'>上海</option>
        <option value='3'>深圳</option>	#这个和radio不同，如果不写value会返回北京，上海以及深圳中的某一个值
</select>		#按住ctrl可以进行多选
```



#### 13.label标签

+ ##### 可以用来标识标签的功能

```html
方式1：for：执行对哪个标签进行标识
效果：电机label标签中的文字，就能让标识的标签获得光标
<label for ='username'>用户名</label>
<input type='text' id='username' name='username' value='dazhuang'>
#id属性是for的标识符

方式2：
		<label>
				密码：<input type='password' name='password' value='111' disabled>
		</label>
```



#### 14.textarea多行文本

```html
<textarea name='memo' id='memo' cols='30' rows='10'>
默认内容
</textarea>
name：名称
rows：行数，对文本框的高度进行设置
cols：列数，对文本框的长度进行设置
disabled:禁用
readonly：只读，针对的是输入框，text，password。设置了readonly的标签，它的数据可以被提交到后台，蛇者了disabled的数据，不能被提交到后台。
```



#### 15.列表标签

```html
<dl>
   <dt>计算机</dt>
   <dd>用来计算的仪器 ... ...</dd>
   <dt>显示器</dt>
   <dd>以视觉方式显示信息的装置 ... ...</dd>
</dl>
```