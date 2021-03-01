## 关于BOM对象的使用

#### 1.一些小的方法

+ ##### script标签要写到body标签的下面，使用window对象后可以写在前面

+ ##### 对于button标签的disabled=true这个button标签就被禁用了

+ ##### `href=javascript:void(0);`	//这样a标签就会去申请原URL了

+ ##### `console.dir()`		//打印返回的元素对象，更好的查看

+ ##### `document.write('<div>123</div>')`	//如果页面文档流加载完毕，会造成页面重绘，这是三种创建元素的方式的其中之一，通过create创建的元素然后挂载这种修改方式不会影响原页面，所以这个也很少用。

+ ##### 在字符串中使用某一个值：'+this.src+'  	//使用这个方法来进行使用，这个非常重要

#### 2.对元素进行操作

+ ##### 获取元素

```javascript
document.getElementById()		//通过id来获取一个完整的标签

document.getElementsByTagName()	//获得所有匹配的标签对象，以伪数组的形式显示，缺少了一些方法，例如pop,push.没有元素返回一个空的伪数组，除了使用document,前面还可以是一个父类标签

document.getElementByClassName()	//获得类标签对象，也是伪数组

document.querySelector('.box')	//类选择器，只能得到第一个，这个可以是任何选择器。('#nav')id选择器 ('li')标签选择器

document.querySelectorAll('.box')	//可以得到所有的，也是所有的选择器都能使用

document.body			//body对象
document.documentElement		//HTML元素对象
```

+ ##### 增删改查

```JavaScript
操作元素(都是属性)
element.innerText=''	//改变标签的内容，不识别HTML标签，读取时会将HTML格式去掉，会自动删除空格和换行
element.innerHTML=''	//也能改变标签内容，可以识别HTML标签，读取时保留HTML标签，保留空格和换行，这个后续更常用

element.value=''		//表单中的内容通过value值来进行修改
btn.disabled=true;		//禁用某个按钮
this.disabled=true;		//使用this也行，指向的是事件函数的调用者

操作属性的样式
this.style.backgroundColor='purple'	//可以对样式进行操作
box.style.dispaly='none'/'block'	//对样式进行操作，进行隐藏和显示
this/element.className=''		//当需要改变的样式很多时，可以通过改变类名进行操作,会将原来的类名覆盖掉，所以可以用多类名的形式，改为'原类名 新添加类名'


element.getAttribute('')	//获取属性，可以得到自定义属性,element.这种方式不能得到自定义属性
element.setAttribute(属性，值)	//可以修改自定义属性
element.removeAttribute(属性)//可以移除属性

//自定义属性一般是data-xxx的格式，是一种规范
//H5新增的获取自定义属性的方法
element.dataset.xxx		//dataset可以获得所有以data开头的自定义属性，后面可以加具体的属性，不加data-了，如果自定义属性有多个-连接的单词，我们获取时用驼峰命名法。
eg:div.getAttribute('data-list-name'),div.datalist.listName,div.datalist['listName']
```

+ ##### 节点操作

```javascript
对节点进行操作
element.parentNode	//获得父节点，离元素最近的父节点，找不到返回null
element.children		//获取所有的子元素节点
element.firstElementChild	//返回第一个子元素节点
element.lastElementChild	//返回最后一个元素节点
element.nextElementSibling	//获得下一个兄弟元素节点
element.previousElementSibling //获得上一个兄弟元素节点，没有返回null

增加节点
document.createElement('li')
node.appendChild(child)	// node父级,child子级
node.insertBefore(child,位置)
               		 //eg:ul.insertBefore(lili,ul.children[0]);
删除节点
node.removeChild(ul.children[0]);

节点复制
node.cloneNode()		//只复制标签，浅拷贝
node.cloneNode(true)	//复制标签，复制内容，这个只是克隆，还得挂载

```

+ ##### 事件操作

```javascript
事件基础
事件三要素：事件源，事件类型，事件处理程序
事件源：事件被触发的对象
事件类型：怎么被触发，例如：鼠标点击（onclick）
事件处理程序:通过一个函数赋值的方式完成

btn.onclick=function(){}	//点击事件
onfocus			//获得焦点事件
onblur			//失去焦点事件
onmousevoer		//鼠标经过
onmousehead		//鼠标离开
```

