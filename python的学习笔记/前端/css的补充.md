## css的补充

#### 1.边框

```css
border-style:solid;		#还有potted虚的点，以及dashed虚线
border-width:1px;
border-color:red;

border:1px dotted red;		#这是边框的简写

border-top-style:solid;
border-top:1px dotted red;

border-radius:50%		#50%及以上就是一个完整的圆
```

#### 2.display

```css
display的值：
none:隐藏标签，不占空间---visibility:hidden;隐藏标签，占用空间
inline：将标签做成内敛的样式
inline-block：同时具备两种标签的一些特点，能够设置高度宽度，并且不独占一行
block：将标签做成块级样式
```

#### 3.盒子模型

```css
content:内容
padding：内边距，内容与边框之间的距离，padding:10px 20px;上下，左右  padding:10px 0 						20px 30px 上右下左
border：边框
margin：外边距 与其他标签的距离

margin-left:10px
margin-top:20px		#当有两个盒子都设置了左边距和右边距，则这两个盒子的距离左右两个距离的距离的和，如果两个盒子都设置了上下的距离，那么两个盒子的距离是这两个距离的最大值
```

#### 4.float浮动

```css
布局用的，设置了浮动的标签会脱离正常文档流，会造成父级标签塌陷的问题
float:left;
float:right;

解决塌陷
1.父级标签设置行高
2.伪元素选择器清除浮动
.clearfix:after{
    content:'';
    display:block;
    clear:both;
}
父级标签class='clearfix'
```

#### 5.overflow溢出

```css
overflow:auto;	出现滚动条
overflow:hidden;	隐藏内容
```

#### 6.position定位

```css
position:relative;	相对定位，保留原来的位置空间，相对自己原来的位置移动
position:absolute;	绝对定位，不保留原来的未知空间，相对于祖上级有定位relative的现在位置进行移动（会跟着那个标签一起走），如果找不到，就按照body标签的位置进行移动
position:fixed;		固定定位，根据浏览器窗口位置来定位
position:static;	默认就是他，不定位
```

#### 7.z-index控制层级

```css
z-index的值谁大，谁在最上层被渲染
```

#### 8.透明度opacity

```css
opacity	标签的透明度
rgba(255,0,0,0.3)	单独设置背景颜色或者字体颜色的透明度
```

#### 9.锚点

```css
设置
	<a name='top'>顶部</a>
	<div id='top'>顶部</div>		#上面两种写法都是锚点

<a herf='#top'>点击回到顶部</a>
```

#### 10.做一个锚点的练习

```css
.ccc{
    display: block;
    height: 40px;
    width: 80px;
    text-decoration: none;
    background-color: aquamarine;
    line-height: 40px;
    position: fixed;
}
.cc1{
    left: 20px;
    bottom: 10px;
    position: fixed;
}

<div class="cc1">
        <a href="#d1" class="ccc">回到顶部</a>
</div>
<div id="d1">
让我看一下，拜托了
</div>
```