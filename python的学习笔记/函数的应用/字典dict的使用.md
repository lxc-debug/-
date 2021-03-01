### 字典dict的使用

字典相比于列表list，其中内容的关联度更高，并且查找的速度更快，但是所耗费的空间更多。

##### 1.字典的创建

```python
dic=dict((('one',1),('two',2),('three',3)))			#通过元组的解包进行创建(一个大元组														#套了三个小元组)
dic=dict(one=1,two=2,three=3)					#类似于format的赋值
dic=dict({'one':1,'two':2,'three':3})			#字典中最正常的创建方式
dic={'one':1,'two':2,'three':3}					#字典中最为常用的创建方式
```

##### 2.字典的增删改查

+ 增

```python
dic={'one':1,'two':2,'three':3}	
dic['four']=4				#若字典中没有该键值，则在字典中新添加一个键值对
dic['four']=5				#若字典中已经含有该键值，那么是对该键值对的修改
dic.setdefault('four',4)	#若不加逗号后的值，则默认值为NONE。
dic.setdefault('four',100)	#若该键值已经存在，则不会进行改动
```

+ 删

相比于del（）函数，pop（）方法的功能更为强大，所以应尽量使用pop（），而且pop会返回值

```python
dic={'one':1,'two':2,'three':3}
dic.pop('one')        			#可以根据键值进行删除
dic.pop('four','此键值不存在')	#当所输入的键值不存在的时候可以返回逗号后的内容，不报错
del(dic['one'])					#可以根据键值进行删除，但是键值不存在时会报错
```

+ 改

  没有特殊方法，找到键值进行修改即可

+ 查

```python
dic={'one':1,'two':2,'three':3}
for i in dic:
    print(i)		#利用for循环进行遍历，输出所有的值
print(dic['one'])	#直接按照键值进行查看
print(dic.get('one','键值不存在'))		#使用get（）方法进行访问，而且当键值不存在时不会报错,更为安全
```

##### 3.其他的一些方法

```python
print(dic.get('one'，'键值不存在'))
print(dic.keys())							#可以通过list（）函数进行转化
print(dic.values())							#可以通过list（）函数进行转化
print(dic.items())					#可以通过list（）函数进行转化，每个元素都是一个元组
```

