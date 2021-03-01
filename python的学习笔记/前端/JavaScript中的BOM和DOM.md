## JavaScript中的BOM和DOM

#### 1.BOM

```
window对象
location.href;		获取当前窗口的url
location.href='http://www.xiaohuar.com';		跳转到指定的网址
location.reload()	刷新页面


计时器
var a=setTimeOut(function(){...},毫秒);		一段时间后做什么事情
clearTimeOut(a)
var a=setInterval(function(){...},毫秒);		重复的在一段时间后做某些事情
clearInterval(a)							
```





#### 2.DOM

```
document.getElementById('d1');
document.getElementByClassName('c1');
document.getElementByTagName('标签名');

间接查找
	var a=document.getElementById('d1');
	a.parentElement
	a.children
	firstEnementChild
	lastElementChild
	nextElementsibling
	previousElementSibling
```

+ #### 节点操作

```
创建节点
	var a=document.createElement('标签名')
	
添加节点
	父级节点.appendChild(a);
	父级节点.insertBefore(a.某个儿子节点)
删除节点
	父级节点.removeChild(某个节点)
替换
	父级节点.replaceChild(新节点，被替换的那个节点)
```

+ #### 文本操作

```
innerText
innerHtml		识别标签

innerText='xx'
innerHtml=‘xx
```

+ #### 属性操作

```
设置属性setAttribute(属性，值)
查看属性getAttribute(属性)
删除属性removeAttribute(属性)

属性自带标签：（使用上面的方式也可以，但是下面的方法更加的简单）
标签对象.属性;
标签对象.属性='xxx'

```

+ #### 值操作

  + ##### 简单来说，就是对于自闭的标签，使用value来取值，对于闭合标签使用innerText来取值

```
input select textarea
标签.value='xx';		修改
标签.value;		查看

select标签.value
select标签.value=option标签中的value属性的值，这个标签就被选中了
```

+ #### class操作

```
获取class的值
标签对象.classList;
标签对象.classList.add('值');
标签对象.classList.remove('值');
标签对象.classList.contains('值');	判断
标签对象classList.toggle('值');		#class中没有这个值就添加，有这个值就删除
```

+ #### `css`操作

```
标签对象.style.css属性='值'；
background-color--->backgroundColor
```

+ #### 事件

```

<script>
    var a=getElementById('d1');
    a.onclick=function (){	}
</script>

onclick			#点击
onfocus			#选中
onblur			#从选中状态退出
onchange		#改变选项
```

