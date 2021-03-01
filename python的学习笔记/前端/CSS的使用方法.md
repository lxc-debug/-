## CSS的使用方法

#### 1.概述

CSS选择器，css代码写法：h1{color：red；} 选择器{css属性：属性值}

css代码引入

```css
1.方式1：
	head标签里面写
	<style>
		div{
            background-cloor:red;
            height:100px;
            width:100px;
}
	</style>

2.方式2：
	内敛样式：
	<div style=' background-cloor:red;height:100px;width:100px;'></div>

3.方式3：
	head标签里写link标签
	<link rel='sylesheet' href='文件路径'>		#这种方式就需要提前也好一个css文件再导入html中
```

#### 2.基本选择器

```html
1.元素选择器
	div{	#标签名字
	color:red;
}

2.id选择器：id值不能重复
	<div id='xuefei'>
        雪飞大美女
</div>
	
	#xuefei{			#在要选择的id前加上#符号，就可以进行选中
	color:green
}

3.类选择器
类值可以重复
	<div id='dazhaung' class='c1'>
        大壮dsb
</div>
	<div id='xuefei' class='c1'>
        雪飞大美女
</div>

	.c1 {
	color:green;
}

	div.c1{				#这个是定义查找div标签下的c1类
	color:red;
}

4.通用选择器
*{		#找到所有的标签
	color：green;
}
```



#### 3.组合选择器

+ #### 后代选择器

```css
div a{		#找到div标签内部的所有的a标签，包括孙子类及以下类的
    color:red;
}
```



+ #### 儿子选择器

```css
div>a{	#仅找到div的儿子标签这一代的a标签
    color:red;
}
```



+ #### 毗邻选择器

```css
div+a{	#找到的是紧挨着div标签的下一个标签（兄弟标签）
    color:red
}
```



+ #### 弟弟选择器

```css
div~a{	#找到的是同级的后面的所有兄弟标签
    color:red;
}
```



#### 4.属性选择器

```html
#通过属性名来查找
[title]{		#找到所有含有title属性的标签
	color:red;
}

div[title]{		#含有title属性的div标签
	color:red;
}

#通过属性名对应的值来查找，当属性值的值为数字的时候，数字要加上引号[title='666']
input[type=text]{	#含有type属性，并且type属性的值为text的input标签
	backgroud-color:red
}
```



#### 5.分组 

```html
多个选择器的标签设置相同css样式的时候，就可以使用分组
div,p{		#div选择器和p选择器共同设置相同的样式，可以逗号分隔
	color:red;
}
```



#### 6.伪类选择器(针对a标签的选择器)

```css
a标签自带的效果：未访问过的时候是蓝色的字体颜色，访问过后是紫色的，自带下划线

a:link {	#未访问过的链接
    color:#FF0000
}

a:visited{	#已访问的链接
    color:#00FF00
}

a:hover{	#鼠标移动到链接上		这个用的比较多，可以应用在其他的标签上
    color:#FF00FF
}

a:active{	#鼠标选定的连接		就是鼠标点下去还没有抬起来的那个瞬间，可以让它变色
    color:#0000FF	
}

input:focous{	#input默认的有个样式，鼠标点进去就会按照指这个方式改变样式
    #outline:none;
    background-color:#eee
}
```



#### 7.伪元素选择器

```css
div:first-letter{	#默认的字体大小为16px比这个大就是放大，比这个小就是缩小
    color:red;
    font-size:20px
}

p:before{
    content:'?';
    color:green;
    font-size:100px
}

p:after{
    content:'哈哈！';
    color:pink;
}
```



#### 8.选择器的优先级

```css
优先级数字越大，越优先显示其效果，优先级相同的，显示后面定义的选择器对应的样式

1.继承的优先级是0
body{
    color:red;
}

2.元素选择器的优先级是1
div{
    color:orange
}

3.类选择器的优先级是10（包括伪类选择器以及属性选择器）
.c1{
    color:purple
}

4.id选择器的优先级是100
#d1{
    color:deepskyblue
}

5.内敛样式优先级为1000
<p class='cc3' style='color:red;'>我是cc3的p标签</p>

6.important的优先级最高，优于一切
.cc1 .cc3{	#这个是类cc1下的子（孙子类及以下）类的cc3类
    color:purple!important;
}

总结以下就是定位的方式越精准，那么的这个选择器的优先级就越高
还有属性可以叠加，当时不可以进位，比如.cc1 .cc3就是10+10，优先级为20
```



#### 9.css属性相关

###### 高度宽度的设置，注意：只有块级标签能够设置高度宽度，内敛标签不能设置高度宽度，它的高度宽度是有内容决定的

```css
div{
    width:100px;
    height:100px;
    background-color:pink;  
}
```

+ ###### 补充，a标签较为特殊，不能进行继承，字体颜色设置必须选中a标签才行

```css
.c1 a{
    color:red;
}
```



#### 10.字体属性

+ ##### 字体设置

```css
.c1{	#这样写的意思是一旦浏览器的内核不支持该字体就从第一个往下读，直到找到可以支持的字体
    font-family:'楷体','宋体','微软雅黑';
}
```



+ ##### 字体大小

```css
.c1{
    font-size:14px
}
```



+ ##### 字体颜色

```css
color:red;
```



+ ##### 字重，粗细

```css
.c1{
    font-weight:bold;
    font-weight:100;		#可以输入100~900，默认是400
}
normal	默认值，标准粗细
bold	粗体
bolder	更粗
lighter	更细
inherit 继承父元素字体的粗细值
```



+ ##### 颜色表示方式

```css
p{
    color:red;
    color:#78FFC9;
    color:rgb(123,199,255);
    color:rgba(123,,199,255,0.3);	#a这里是一个透明度的表示：0-1中间的一个数字
}
```



#### 11.文字属性

##### 文字对齐(text-align)

```css
div{
    width:200px;
    height:200px;
    background-color:yellow;
    text-align:right;	#这个是右对齐，还有center，以及left居中以及左对齐
        
}
```



##### 文字装饰(text-decoration)

```css
div a{
    text-decoration: none;
    text-decoration: line-through;
    text-decoration: overline;
    text-decoration: underline;
}
```



##### 首行缩进

```css
p {
    text-indent :32px;	#首航缩进两个字符，因为默认一个字是16px
}
```



#### 12.背景属性

```css
背景颜色
background-color: red;

div{
    width:600px;
    height:600px;
    background-image:url("");
    background-repeat:no-repeat;
    background-position:100px 50px；	#这个方位是相对图片的左上角说的
    background-attachment:fixed		#将图片根据位置属性，始终在屏幕上的某个位置显示
    background:url("") no-repeat left center;#这是一种简写 
        
}
简写方式，颜色 图片路径 是否平铺 图片位置
background:#ffffff url("") no-repeat right top;
```

