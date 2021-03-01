## js的基础部分

#### 1.js的基础语法

+ #####  三个内置的函数

```javascript
prompt（'请输入您的年龄'）		//让用户输入
xxx instanceof Array		//判断xxx是不是数组
Array.isArray(xxx)		//判断是不是数组
```

+ ##### 关于事件对象的使用

```javascript
new +Date()		//返还当前的时间戳
Date.now()		//返回当前的时间戳 
```

+ ##### 关于数组的一些操作

```javascript
arr.push()		//返回新数组的常数，尾插法
arr.pop()		//删除最后一个元素，返回删除的元素
arr.unshift()	//头插法，返回值为数组长度
arr.shift()		//删除第一个元素，返回删除的元素

arr.reverse()	//翻转数组
arr.sort()		//按最左边的数进行排序
arr.sort(function(a,b){
	return a-b;})	//按照升序进行排列
arr.indexOf(xxx)	//返回从左到右的第一个匹配的索引号，找不到返回-1
arr.lastIndexOf(xxx)	//从右往左进行查找

arr.toString()	//转换为字符串
arr.join('-')	//默认用','进行连接
```

+ ##### 关于字符串的一些操作

```javascript
str.indexOf('xxx',3)	//从第三个开始查找
str.charAt(x)			//输出对应位置的字符
str.charCodeAt(x)		//返回对应字符的ASCII码
str[index]				//h5新增的方法

str.concat(xxx)			//拼接字符串，直接连接
str.substr(截取的起始位置,取几个)
str.replace(被替换的字符串,要替换成什么)	//只会替换第一个
str.split('&')			//分割
```