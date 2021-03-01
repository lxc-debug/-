### property装饰器以及反射的应用

#### 1.property装饰器

+ ##### 这个装饰器用在雷内的绑定方法上，用于在类外访问时可以用类似访问变量的方式访问

  ##### 还有setter和`deleter`两种使用方式

  ```python
  class price:
      discont=0.8
      def __init__(self,price):
          self.__price=price
      @property
      def getprice(self):
          return self.__price*self.discont
  apple=price(8)
  print(apple.getprice)	
  #这就是第一种使用方法，在绑定函数的上方加上@property将方法伪装成一个变量
  
  ```

  ```python
  class price:
      discont=0.8
      def __init__(self,price):
          self.__price=price
      @property
      def getprice(self):
          return self.__price*self.discont
      @getprice.setter
      def getprice(self,num):
          self.__price=num
  
  apple=price(8)
  print(apple.getprice)
  apple.getprice=10
  print(apple.getprice)
  #这是第二种使用方法，使用要求是定义的三个getprice必须相同，相当于c++中的重构，对于加了
  ```

  ```python
  setter的函数，可以多传一个参数，也就是调用的时候可以用=赋值
  class price:
      discont=0.8
      def __init__(self,price):
          self.__price=price
          self.ppap=666
      @property
      def getprice(self):
          return self.__price*self.discont
      @getprice.setter
      def getprice(self,num):
          self.__price=num
      @getprice.deleter
      def getprice(self):
          print('这个函数被调用了')
          del self.__price
          del self.ppap
  
  
  apple=price(8)
  print(apple.getprice)
  apple.getprice=10
  print(apple.getprice)
  del apple.getprice
  print(apple.ppap)		
  #这个用法不常用，就相当于c++中的析构函数，使用这个以后再外部对对象调用del就会调用类内的这个函数
  ```

#### 2.反射的应用

+ ##### 反射是一个功能十分强大的使用方法，可以大大的所见程序员的代码量

```python
class cat:
    def __init__(self,name,kind):
        self.name=name
        self.kind=kind
    def get_name(self):
        print(self.name)
    def get_kind(self):
        print(self.kind)
xiaobai=cat('小白','英短')
print(xiaobai.name)
print(getattr(xiaobai,'name'))
print(xiaobai.get_name)
print(getattr(xiaobai,'get_name'))
xiaobai.get_kind()
getattr(xiaobai,'get_kind')()
#使用getattr，第一个参数是类名，或者模块的名字，第二个参数必须是一个字符串，通过这个方法，与使用.得到的结果都是一致的，这个用法很强大。
```

+ 反射的高阶用法

  + 第一个

  ```python
  class cat:
      def __init__(self,name,kind):
          self.name=name
          self.kind=kind
      def get_name(self):
          print(self.name)
      def get_kind(self):
          print(self.kind)
  import sys
  a=getattr(sys.modules['__main__'],'cat')
  xiaobai=a('小白','英短')
  print(xiaobai.name)	
  #这里是吧自己模块内的类进行反射
  ```

  

  + 第二种情况

  ```python
  import sys
  import text
  if hasattr(sys.modules['text'],'p_li'):
  	a=getattr(sys.modules['text'],'p_li')
  	a()
  #这里是对外部导入的拨快进行反射,使用hasattr以及getattr
  ```

  + 第三种情况
```python
class option1:
    li=[('登录','login'),('注册','register')]
      def login(self):
          print('login')
      def register(self):
          print('register')
      def run(self):
          while 1:
              print('请输入要进行的操作：')
              for i,option in enumerate(self.li):
                  print(i,':',self.li[int(i)][0])
              sel=input('您要进行的操作：')
              if sel.upper() =='Q':
                  break
              else:
                  a=self.li[int(sel)][1]
                  getattr(self,a)()
  
  a=option1()
  a.run()
```

  



