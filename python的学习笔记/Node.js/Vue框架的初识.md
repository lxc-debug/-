# `Vue`框架的初识

#### 一、`Vue`的替换

##### 1.最基本的使用方法

```html
<div id= “box”>
	{{10+20}}
	{{myname}}
	<div v-html="myhtml">
	</div>	    //这里的v-html实际是自定义属性，vue中称为指令
</div>		

new Vue({
	el:"#box",
	data:{
		myname:"kerwin",
		isShow:true,
		isCreate:true
		}
})		//可以对{{}}中的内容进行替换
```

##### 2.动态绑定

###### 动态绑定后，双引号中的内容将会被当做`js`来执行

```html
<div :class="classobj"></div>//这里的:是动态绑定，也是Vue中的写法
<div :class="classarr"></div>
<div :style="classarr"></div>//这里的样式也是动态绑定的

data:{
	classobj:{
		a:true,		//这里的a，b都是css的样式
		b:true},
	classarr:["a","b"]	//使用数组可以添加删除，使用对象则只能删除（现在只能删除，以后会有解决办法）
}
```

##### 3.绑定方法

```html
<button @click="handleClick()">click</button>
methods:{
	handleClick(){
		this.isCreated=!this.isCreated}
}

@input事件	//input标签中的值每一次发生改变就会触发对应函数
@change		//失去焦点的时候就会触发函数
v-module	="mytest"	//双向数据绑定，input中的值会改变绑定的值

@click.stop		//事件修饰符，阻值冒泡
@click.prevent		//阻值默认行为
@click.self		//触发事件源不是自己就不执行，也可以阻值冒泡
@click.once		//事件只能触发一次
@keyup.enter		//只有摁下enter键的时候才会触发
@keyup.13		//对于这个还可以直接跟ASCII码值


```

##### 4.特殊标签

```html
v-show="isShow"		//控制显示和隐藏的指令	
v-if="isCreated"		//控制创建和删除
v-module	="mytest"	//双向数据绑定，input中的值会改变绑定的值
v-module.lazy		//失去焦点才会同步一次
v-module.trim		//除去前后的空格

<ul v-if="datalist.length">
<li v-for="(data,key) in datalist">
	{{data}}--{{key}}		//可以显示对象的数据和key值
</li>
</ul>

vue.set(xxx,"xx",x)		//某一个对象的属性进行修改或者添加，这里需要var一个Vue变量出来
```

##### 5.发请求

```javascript
有两个函数可以用来发请求，一个是es6中自带的fetch，一个是需要导入的axios
1.fetch
fetch("地址").then(res=>res.json()).then(res=>{console.log(res)})//发请求
//通过return res.json()就可以得到数据对象了
2.axios
axios的使用方法和fetch基本相同，只是在使用时需要return res.data(这里记不清需要变量还是函数了)
```

#### 二、组件