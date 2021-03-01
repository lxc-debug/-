#### str的函数的用法

1. ##### str的切片

   ```python
   meg='lxc非常帅'			#切片的过程顾头不顾腚（去左不取右）
   s1=meg[1:2]
   s2=meg[::2]					#2为步长，也就是每隔一个数取一个数
   s3=meg[0:-1]				#str可以从0开始从左向右数，也可以从-1开始从右往左数
   s4=meg[:]					#从开头取或者是取到结尾就可以什么都不加
   ```

   ##### 2.str的各种方法的用法

   + ###### strip的用法

   ```python
   meg=' /nlxc非常帅/t'
   s1=meg.strip()					#strip这个方法默认可以清楚字符串两端的空字符，包含											‘ ’，’/t','/n'
   meg='aeivialxc非常帅eninvisj'
   s2=meg.strip('aeivnsj')			#strip方法可以自定义要去除的字符，但是本例中有一个小									#bug，不能去除含有l的子串，不然想要打印的内容也会
   									#被减去
   ```

   + split的用法

   ```python
   meg="lxc lxc lxc lxc"
   s2=meg.split()			#split是一个切片的方法，通过空格将字符串分割成为列表进行存储
   						#分割后s2中存储的数据为['lxc', 'lxc', 'lxc', 'lxc']
   meg="lxc:lxc:lxc:lxc"
   s2=meg.split(':')		#split方法还可以自定义分隔符
   s3=meg.split(':',2)		#split方法还可以自定义对前面的几个分隔符进行分割
   
   ```

   + format输出

   ```python
   meg='我的名字是{}，我的年龄是{}，我的性别是{}'.format('lxc',18,'male')
   
   meg='我的名字是{0}，我的年龄是{1}，我的性别是{2}'.format('lxc',18,'male')
   
   meg='我的名字是{name}，我的年龄是{age}，我的性别是{sex}'.format(age=8,sex='male'，name='lxc')					#format()方法的三种用法
   ```
   
   + join

   ```python
s1='+'
   s2=["lxc",'lxc','lxc','lxc']
   s1=s1.join(s2)		#输出结果为lxc+lxc+lxc+lxc <class 'str'>
   ```

   

   + replace

   ```python
meg="xxx非常厉害，xxx非常帅，xxx人缘很好"
   s1=meg.replace("xxx","lxc")			#对字符串进行替换

   s1=meg.replace("xxx","lxc",2)		#还可以规定要替换的个数
   ```
   
   
   
   + str的一些其他方法
   
   ```python
   meg="QWer"
   s1=meg.upper()					#将字符串全部变为大写，中文跳过
   s2=meg.lower()					#将字符串全部变为小写，中文跳过
   meg.isalnum()					#判断字符串是否只由数字和字母组成
   meg.isalpha()					#判断字符串是否只由字母组成
   meg.isdecimal()					#判断字符串是否只由十进制数字组成（decimal是十进制的									#意思）
   meg.count('q')					#判断自定义的字符在字符串中出现的次数，区分大小写
   meg.startwith('Q')
   meg.endwith('r')				#判断字符串是否以某一个字符串开头或者结尾
   ```
   
   + 一个非常好用的内置函数
   
   ```python
   len()				#这个函数可以用来判断各种结构中的元素的个数
   ```
   
   + 三元运算符
   
     python中的三元运算符与c不同，需要注意一下
   
   ```python
   a if a>b else b
   ```
   
   
   
   
   
   
   
   
   
   
   
   