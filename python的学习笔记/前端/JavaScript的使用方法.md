## JavaScript的使用方法

#### 1.js代码的引入

```javascript
方式1：
	<script>
    var a1=100;
	</script>
方式2：
	<script src='js文件路径'></script>
```

#### 2.变量声明

```html
var a=10;
```

#### 3.基础数据类型

+ ##### 数值类型Numbre

```html
整数，浮点数，NaN
```

+ ##### 字符串

```
var s1='hello';
var s2='world';
var ss=s1+s2;
```

+ ##### 字符串的常用方法

```
var s='hello';
var s2='world'
s.length	长度
s.trim()	清除两端的空白		s.trimLeft()		s.trimRight()
s.concat()	字符串的拼接		s.concat(s2)
s.indexOf()	通过元素找索引		s.indexOf('e')
s.charAt()	通过索引找元素		s.charAt(1)
s.slice()	切片			s.slice(1,3)
s.split()	分隔			s.split('e',2)
s.toLowerCase()		全部变小写
s.toUpperCase()		全部变大写
```

+ ##### 布尔值

```
var a=true;
var b=false;
空的数值类型也是false，'',0,NaN,undefined
```

+ ##### null和undefined

```
null		空值，一般用来清空一个变量值来用
undefined		var a;	声明了变量，还没有赋值，此时这个变量为undefined
```

+ ##### 类型转换

```
parseInt('111');
parseFloat('1.11');
```

+ ##### 复杂数据类型

```
var a=[11,22,33];
var a=new Array([11,22,33])
typeof a;	--object类型
```

+ ##### 数组常用方法

```
a[1];
a.length
a.push()
a.pop()
a.shift()		头部删除
a.unshift()		头部追加
a.sort()
	function sortnum(a,b){return a-b;}	升序	a.sort(sortnum)

a.slice()	切片
a.splice()	删除元素	a.splice(索引，删除几个，新值)	a.splice(1,2.'aa','bb')
a.reverse()
a.join('+')
a.concat()
	var b=['aa','bb'];
	a.concat(b);	--类似于python中的extend方法
```

+ ##### 自定义对象

```
var a={'name':'chao',age:18}
a['name']

for (var i in a){
	console.log(i,a[i]);
}
```

#### 4.运算符

+ ##### 算数运算符

+ ##### 比较运算符

```
===		强等于，比较地址
!==		强不等于，比较地址
```

+ ##### 逻辑运算符

```
&& || !			与或非
```

+ ##### 流程控制

```
1.if
var a=10;
if(a>5){
console.log(11)
}
else if(a=5){
	...
}
else{
	...
}

2.switch	切换
var a=10;
switch(a){
case 10:
	...
	break
case 11:
	...
	break
default :
	...
}

```

+ ##### while

```
var a=0;
while (a<10){
	console.log(a);
	a++;
}
```

+ ##### 三元运算符

```
var a=10;
var b=20;
var c=a>b?a:b;
```

+ ##### for

```
for (var i=0;i<10;i++){
...
}
var d=[...]
for (var i in d){
	console.log(d[i]);		与python不同，这个拿到的是索引，不是值
}
```

#### 5.函数

```html
function f1(){
	console.log('!');
}


function.f1(a,b){
	console.log('!');
	return 666;
}
f1(1,2)			#执行

var sum=function(a,...){
	console.log('');
}
sum(1,...)

自执行函数
(function(a,...){...})(1...);
```

#### 6.闭包

```html
function outer(){
	var o=10;
	function inner(){
		console.log(o);
}
	return inner;
}
var ret=outer();
ret()
```

#### 7.面向对象

```html
function Person(a,b){
	this.a=a;
	this.b=b;
}
Person.prototype.f1=function (c,d){return c+d;}		#在类中加入一个函数

var p=new Person('aa','bb')


p.a;
p.f1(1,2);		#调用
```

#### 8.Date对象

```html
var d=new Date();		当前日期对象
d.toLocalString();		显示对象
var d = new Date('2019/7/2 12:00');
d.toLocalString();


Date对象的常用方法
d.getDate()
d.getDay()
//getMonth()
//getFullYear()
//getHours()
//getMinutes()
//getSeconds()
//getMilliseconds()
//getTime()			#返回一个毫秒数，时间戳
```

#### 9.json对象

```
序列化
var d={'xx':'xx'};
var dstr=JSON.stringify(d)

反序列化
var d='{"''"xx"''":"''"xx"}';
var dd=JSON.parse(d)
```

#### 10.正则

```
var s='hello';
var s2='alex';
var a=/^a/;
a.test(s);		--false
a.test(s2);		--true

s2.match(/a/g)	--['a','a']
s2.split(/a/g)	字符分割，写不写g都行
s2.replace(/a/gi,'sss');	--i是忽略大小写
s2.search(/a/) 	--找索引位置
```

#### 11.Math内置模块

```html
Math.abs(-1);
epx(x)		返回e的指数
floor(x)	小数部分直接去掉
log(x)		返回对数
max(x,y)	
min(x,y)
pow(x,y)
random()	返回0~1之间的随机数
round(x)	把数四舍五入到最接近的整数
sin(x)
sqrt(x)
tan(x)
```

