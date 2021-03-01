## scrapy模块的使用

#### 1.图像的存储

```python
在pipelines.py文件中，重写ImagesPipeline这个类

import scrapy
from scrapy.pipelines.images import ImagesPipeline
class ImgproPipeline(ImagesPipeline):
    def get_media_requests(self,item,info):
        yield scrapy.Request(item['img_src'])	#这个函数是给图片的地址发请求
        
    def file_path(self,request,response=None,info=None):
        return request.url.split('/')[-1]	#这个函数是在给文件命名
    
    def item_completed(self,results,item,info):
        return item		#这个函数是吧存储内容再一次弹出，让其他存储函数可以访问
    
    
#######注意事项#########
在使用这个方法的时候，记得在配置文件中加上
IMAGES_STORE='./imgLibs'
```

```python
crawlspider的使用
1.创建一个文件
	新建一个工程
    cd 工程
    新建一个文件 scrapy genspider -t crawl 文件名 www.xxx.com

2.爬虫文件的编写
	class SunSpider(CrawlSpider):
        name='sun'
        strat_urls="www.xxx.com"
        #实例化了一个链接提取器对象
        #作用：根据指定规则（allow="正则表达式"）进行指定链接的提取
        link=LinkExtractor(allow=r'type=4&page=\d+')
        link_detail=LinkExtractor(allow=r'question/\d+/\d+\.shtml')#这里的.需要转义
        rules=(
            #将link作用到Rule的构造方法参数1中
            #将链接提取器提取到的链接进行请求发送并且根据指定的规则对请求到的参数进行数据解析
        	Rule(link,callback='parse_item',follow=False)
            Rule(link_detail,callback='parse_item_detail',follow=False)
        )

 3.管道存储
#因为用两个链接器对象，所以会有两个解析函数，而且是通过rule来进行的请求发送，不是手动的请求，所以不能用meta来进行item的参数传递，所以会有两种item类型
class SuncrawlproPipeline(object):
    def process_item(self,item,spider):
        if item.__class__.__name__=="Detail_item":
            return item
        else:
            return item
```

#### 2.分布式

```python
-原生的scrapy框架不可以实现分布式
	-因为调度器不可以被共享
    -管道不可以被共享
-如何实现分布式
	-scrapy+scrapy_redis实现分布式
-scrapy_redis组件的作用是什么
	-可以提供被共享的调度器和管道
    -特性：数据只可以存到redis数据库中
-分布式的实现流程
	1.pip install scrapy-redis
    2.创建工程
    3.cd 工程目录
    4.创建爬虫文件（a.创建爱你基于spide的爬虫文件 b.常见基于crawlspider的爬虫文件
    5.修改爬虫类
    	-导入包：from scrapy_redis.spiders import RedisCrawlSpider
        -修改当前爬虫类的父类为：RedisCrawlSpider
        -allowed_domains和start_urls删除
        -添加一个新属性:redis_key='fbsQueue',表示的是可以被共享的调度器队列的名称
        -编写爬虫类的其他操作（常规操作）
        -这里不进行pipline的编写，使用scrapy_redis提供的pipline
    6.settings配置文件的配置
    	-UA伪装
        -Robots
        -管道的指定
        	ITEM_PIPELINES={
                'scrapy_redis.pipelines.RedisPipeline':400
            }
        -指定调度器
        	#增加了一个去重容器类的配置，作用是使用Redis的set集合来存储请求的指纹数据，从而实现请求去重的持久化
            DUPEFILTER_CLASS="scrapy_redis.dupefilter.RFPDupeFilter"
            #使用scrapy_redis组件自己的调度器
            SCHEDULER="scrapy_redis.scheduler.Scheduler"
            #配置调度器是否要持久化，也就是当爬虫结束了，是否要清空Redis中请求队列和去重指纹的set，如果是true就表示要持久化存储，不清空数据，否则就会清空数据
            SCHEDULER.PERSIST=True
            
            
        -指定Redis数据库
        	REDIS_HOST='Redis服务的ip地址'
            REDIS_PORT=6379
            
        -Redis的配置文件进行配置redis.windows.conf:#这是一个文件，用pycharm打开
            -关闭默认绑定：56line:#bind 127.0.0.1
            -关闭保护模式：75line:protectd-mode no
                
        -启动Redis的服务端和客户端：
        	-redis-server.exe redis.windows.conf	#需要带着配置文件启动
            -redis-cli
            
        -启动程序：
        	scrapy runspider xxx.py		#需要cd到这个文件的目录下（一般是两个cd）
            
        -向调度器的队列中扔入一个其实的url：
        	-队列是存在于Redis中
            -开启Redis的客户端：
            	lpush fbsQueue 首页的网址
```

