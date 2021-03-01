## jQuery使用方法

#### 1.创建方法

```
上网搜索jquery的代码，然后将整个代码拷贝下来，然后在python中创建一个js文件，将代码整个粘贴过去，最后通过html就可以将这个框架引入。
```

#### 2.jQuery对象和dom对象

```
jquery找到的标签对象时jQuery对象
原生js找到的标签对象时dom对象
dom对象和jQuery只能使用自己对应的方法，不能使用对方的方法

互相转换
$(dom对象)就可以将dom对象转化为jquery对象
$('#d1')[0]就可以将jquery对象转化为dom对象

说一点个人的理解：我人为js其实就是一个c，python，的整合版，这个jquery对象就好比一个数组，dom对象就是其中的元素，将其从数组中取出的时候就会发生类型的转变，比方int，而且字典在用for进行循环的时候，得到的是键值，而对于数组进行循环的时候，得到的是一个索引。
```

#### 3.jQuery的使用

```
$('#d1')		#使用的方法与css完全相同
$('div.c1')
```

#### 4.属性选择器

```
[attribute]

例子
$("input[type='checkbox']");
$("input[type!='text']")		#取类型不是text的input标签
```

#### 5.表单筛选器

```
找到的是type属性这个值的input标签中
:text
:password
:file
:radio
:checkbox
:submit
:reset
:button

$(':password')		#使用方法
```

#### 6.表单对象属性筛选器

```
:enbaled		#可用的标签
:diabled		#不可用的标签
:checked		#选中的input标签
:selected		#选中的option标签

$(':disabled')		#使用方法
```

#### 6.筛选器方法

```
下一个
	$('#l3').next()
	$('#l3').nextAll()
	$('#l3').nextUntil("#l5")		#找到满足条件的元素，并且不包含他

上一个
	$('#l3').prev()
	$('#l3').prevAll()
	$('#l3').prevUntil("#l2")
#########这两个都是同级查找

父亲元素
	$('#l3').parent()
	$('#l3').parents()		#查找当前元素的所有父辈元素
	$('#l3').parentUntil('body')		#查找当前元素的所有父辈元素，知道遇到匹配的那个元素为止，这里知道body标签，基本选择器都可以在这使用
	
儿子的兄弟元素
	$('#l3').children();
	$('#l3').children('#l3');		#找到符合标准的儿子标签
	
	$('#l3').siblings();
	$('#l3').siblings('#l3');		#找到符合后面这个选择器的兄弟标签
	
find
	$('#l3').find('#l5')		#相当于$('#l3 #l5')

filter过滤
	$('li').filter('#l3')
	
.first()		#获取匹配的第一个元素
.last()			#获取匹配的最后一个元素
.not()			#从匹配元素的集合中删除某些元素
.has()			#保留包含指定后代的元素
.eq()			#索引值等于指定值的标签
```

