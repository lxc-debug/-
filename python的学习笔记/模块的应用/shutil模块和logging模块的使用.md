### shutil模块和logging模块的使用

#### 1.shutil模块的使用

+ ##### shutil模块是一个功能十分强大的对文件和文件夹操作的模块

```python
import shutil
shutil.copy2("D:\python_22\day21\lianjia.html",
             "D:\python_22\day21\lianjia_1.html",)
		#一共需要两个参数，一个是源文件的名字，一个是目标文件的名字
shutil.copytree("D:\python_22","D:\python_21\python_22",
                ignore=shutil.ignore_patterns("*.txt",'*.mp4'))
		#一个是原目录的位置，一个是目标目录的位置，还可以添加一个不复制某种文件的参数
shutil.rmtree("D:\python_22",ignore_errors=True)
		#需要删除的目录的位置，可以设置忽略一些错误信息
shutil.move("D:\python_22\day21\lianjia.html",
            "D:\python_22\day21\lianjia_1.html",
            copy_function=shutil.copy2)	#系统默认就是copy2
		#源文件的位置和目标文件的位置
total,use,free=shutil.disk_usage(r'D:')
		#获得磁盘的使用量
print(f'当前磁盘共有{round(total/1024/1024/1024,2)}GB，'
      f'使用了{round(use/1024/1024/1024,2)}GB,'
      f'还剩余{round(free/1024/1024/1024,2)}GB.')
shutil.make_archive(r"666",'zip',
                    r'D:\认识Python\工程文件\bin')
		#打包后文件的名称和位置（这个例子中，没有加位置），打包方式，需要打包的文件
shutil.unpack_archive('666.zip','./text')
		#解包的名称，解包后的位置
```

#### 2.logging模块的使用

+ ##### logging模块是一个日志模块，在实际的开发过程中，以及投入使用后，都有着非常重要的作用

```python
import logging
logging.debug('debug information')
logging.info('info information')
logging.warning('warning information')
logging.error('error information')
logging.critical('critical information')
#以上为五种等级的日志信息，pycharm中默认显示后面三个等级的错误信息
fh=logging.FileHandler('tmp.log',encoding='utf-8')
	#这个是设置保存文件的编码方式
sh=logging.StreamHandler()
	#这个是设置在文件中写入的同时在屏幕上显示
from logging import handlers
rh=handlers.RotatingFileHandler('tmp.log',maxBytes=1024*1024*1024,backupCount=5)
	#这个还有下一个是文件的切片，当日志文件大于1M时就会再创建一个文件，上限是5个，当多于5个，新产生的文件，会把旧的文件顶替掉
th=handlers.TimedRotatingFileHandler(filename='tmp.log',when='s',interval=5,encoding='utf-8')
	#这个是按时间进行切分，每过5s产生一个新的文件
logging.basicConfig(
    format='%(asctime)s - %(name)s - %(levelname)s[line:%(lineno)d] -(module)s: %(message)s ',	#这个是日志的显示形式，每次使用复制即可
    datefmt='%Y-%m-%d %H:%S:%S',		#这个是日期的显示形式
    handlers=[fh,sh],			#这个是日志的显示形式，一般fh，sh一起用，rh，th各用各的
    level=logging.DEBUG			#这个是调整开始记录的等级，默认是warning
)
```

#### 3.递归函数

```python
import os


def func(path):
    size: int = 0
    name_list = os.listdir(path)
    print(name_list)
    for name in name_list:
        abs_path = os.path.join(path,name)
        if os.path.isfile(abs_path):
            size += os.path.getsize(abs_path)
        else:
            size+=func(abs_path)
    return size			#注意return的位置，在循环结束后再返回

ret=func(r'D:\认识Python\crawl_learning')
print(ret)			#显示文件夹的大小
```