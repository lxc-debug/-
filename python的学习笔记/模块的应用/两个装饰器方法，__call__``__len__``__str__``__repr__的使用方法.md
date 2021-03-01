### 两个装饰器方法，`__call__``__len__``__str__``__repr__`的使用方法

#### 1.两个装饰器的使用方法

+ ```python
  class price:
      discount=0.8
      @classmethod
      def ch_dis(cls,num):
          cls.discount=num
      @staticmethod
      def func():
          print(666)
  #classmethod是将一个方法转化为类方法，适用于函数内部仅对于类内的静态变量进行操作，不对对象的变量进行操作的情况
  #staticmethod用于将一个方法转换为静态方法，适用于既不操作类内的静态变量，有不对对象内部的变量进行操作的情况，这种函数可以放在类的外部，但是有时为了进行封装，而将这个函数放到类中，用的情况不是很多。
  
  ```

+ ```python
  #这是一个非常经典的使用类函数的例子
  import time
  class get_time:
      def __init__(self,year,month,day):
          self.year=year
          self.month=month
          self.day=day
      @classmethod
      def get_localtime(cls):
          tm=time.localtime()
          year=tm.tm_year
          month=tm.tm_mon
          day=tm.tm_mday
          ti=cls(year,month,day)
          return ti
  ti=get_time.get_localtime()
  print(ti.year)
  print(ti.month)
  print(ti.day)
  ```

##### 2.各式各样的内部方法的使用

+ ##### `__call__`的使用

```python
class get_time:
    def __call__(self, *args, **kwargs):
        pass
print(callable(get_time))
#这个方法的作用是让类以及该类实例化的对象都可以加（）后进行调用，调用的内容就是给方法内部的内容
```

+ ##### `__new__`的使用

```python
class Child:
    __instence=None
    def __new__(cls, *args, **kwargs):
        if cls.__instence==None:
            cls.__instence=super().__new__(cls)	#这里与绑定函数不同，需要手动加上cls
            return cls.__instence
    def __init__(self):
        print(666)
       #这是一个非常经典的单例的模型，每一次示例话的对象所使用的空间都是相同的
```

+ `__len__``__str__``__repr__`的使用

##### 这是哪个方法，分别对应于取长度以及调用print函数时所打印的内容，当内部有`__str__`时就会调用这个方法，没有时就会调用`__repr__`这个方法，都没有就会默认打印地址