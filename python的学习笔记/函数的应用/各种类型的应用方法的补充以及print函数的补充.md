### 各种类型的应用方法的补充

#### 1.str类型的补充

```python
str1='taiBai'
str1=str1.capitalize()		#将字符串首字母大写，且其他字母小写Taibai
str1=str1.swapcase()		#将字符串的大小写翻转
str1=str1.title()			#将字符串的每一个单词的开头大写，只要不是用字母连接就认为是下一								#个单词的开头
str1=str1.index('tai')		#在字符串中寻找字符串的位置,找不到会报错，字符串没有find()方法
str1=str1.center(40,'*')	#将字符串居中，不够的地方用‘*’填充
str1=str1.find('tai')		#找不到会返回-1不会报错
```

#### 2.list类型的补充

```pyhon
l1=[3,5,4,8,6,1,8,2,7]
l1.sort()			#对列表进行从小到大的排序
l1.sort(reverse=1)	#对列表进行从大到小的排序
l1.sort(8)			#查找元素，没有会报错
l1.reverse()		#直接翻转排序
l1=l1*3
l2=[666,8468]
l1+=l1				#列表可以直接相加或相乘
```

#### 3.tuple类型的补充

```python
tu1=(3,4,5,6,7)
tu1.count()
tu1.index()
```

#### 4.dict类型的补充

```python
dic={'name':'taibai','age':18,'sex':1}
dic.update(((1,666),('name','taibaijinxing')))
dic.update(1=666,name='taibaijinxing')
dic.update({1:666,'name':'taibaijinxing'})		#类似于创建元组的三种方法，有则改之，无则添加
dic.formkeys((1,2,3,4,5,6),666)	#{1: 666, 2: 666, 3: 666, 4: 666, 5: 666, 6: 666}
								#进行递归创建
```



##### 5.print函数的补充

##### \r将光标移至行首

##### print(flush=True)立即打印，每一次打印的内容不会因为打印过快而刷掉