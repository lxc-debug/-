### re模块以及带参数的装饰器

#### re模块的应用

+ ##### `findall`（）与search（）方法的运用

```python
import re
meg='aoiwewnvlaid156846aelivj846816aeinvlaie'
print(re.findall('\w\d+\w',meg))	#会将匹配到的元素以列表返回
print(re.findall('\w(\d+)\w',meg))	#会将分组内的元素以列表返回
print(re.search('\w\d+\w',meg).group())	#仅匹配第一个元素，返回一个对象，通过group来显示
print(re.search('(\w)(\d+)(\w)',meg).group(1))	#通过group来显示，n是显示第几个，0是显示全部
print(re.search('(\w)(?:\d+)(\w)',meg).group(2))	#显示的结果是a，通过(?:)来取消匹配。findall中也可以这么使用
print(re.search('(\w)(?P<name>\d+)(\w)',meg).group('name'))	#有的时候要选择的内容非常多，竖起来很麻烦，可以用这种方法来进行起名并查找
meg='aoiwewnvlaid156846/delivj846816aeinvlaie'
print(re.findall('(?P<name>\w)\d+/(?P=name)',meg))	#返回结果为d，后面的结果匹配的内容必须与前面匹配的内容相同
re.findall('\d.\d',meg,flags=re.S)	#加了flags=re.S参数后，.可以匹配换行符
```

+ ##### compile与`finditer`方法的运用

```python
import re
meg='aoiwewnvlaid156846/delivj846816aeinvlaie'
a='\w\d+\w'
ret=re.compile(a)		#compile方法可以提前对正则表达式进行编译，所以对于相同的查找规则，并且对不同的字符串进行筛选，使用这个方法可以节省时间
print(ret.findall(meg))	#直接用编译出来的对象.方法进行操作
it=ret.finditer(meg)	#finditer方法会返回一个迭代器，从而可以节省空间
print(it)
for i in it:
    print(i.group())	#通过.group方法可以访问其中的内容
```

+ ##### split,sub,`subn`，match方法的运用

```python
print(re.split("\d\d\d",meg))		#按照正则表达式进行切片
			#['lxc', 'taibai', 'wusir', 'nvshen', 'alex']
print(re.split("\d(\d)\d",meg))		#正则表达式中的一部分也会作为切片内容
			#['lxc', '2', 'taibai', '5', 'wusir', '8', 'nvshen', '5', 'alex']
print(re.sub("\d(\d)\d",'H',meg,2))	#对匹配到的对象进行替换，可以指定替换几个，默认全替换
print(re.subn("\d(\d)\d",'H',meg))	#全部进行替换，并返还替换的个数
				#('lxcHtaibaiHwusirHnvshenHalex', 4)
print(re.match('\w+.*\w+$',meg).group())	#这个必须是开头就进行匹配才行，方法类似于search，相当于默认在正则表达式前加一个'^'，这个是用于匹配，search用于查找
```

#### 2.带参数的装饰器

+ ##### 我们已经学过了装饰器，其实带参数的装饰器就是在装饰器的外边再套一层函数

```python
import time
def logger(name):
    def func(f1):
        def inner(*args,**kwargs):
            tm=time.strftime("%y-%m-%d %H:%M:%S")
            with open(name,encoding='utf-8',mode='wt') as f:
                f.write(f'在{tm}，调用了{f1.__name__}函数')
            ret=f1(*args,**kwargs)
            return ret
        return inner
    return func
@logger('1.txt')	#这个语法糖相当于执行了ret=logger('1.txxt')  @ret
def login():
    print('这个函数被调用了')
login()		#利用最外层的函数可以向内部传递参数
```