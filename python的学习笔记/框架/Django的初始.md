## Django的初始

#### 1.Django的下载安装

```
下载：pip install django==1.119

创建项目
	django=admin startproject qingqing
	cd qingqing

启动项目
	python manage.py runserver 127.0.0.1:8000

创建app
	python manage.py startapp xiaoqing
需要在项目的配置文件setting.py中添加一个app配置
INSTALL_APPS[
	"xioaqing"
]
```

#### 2.两个框架模式

```
MVC
	M:models数据库相关
	V:views师徒逻辑相关
	C:controller控制器，URL分发，不同的路径找到不同的视图函数

MTV
	M:models数据库相关
	T:templates末班，HTML文件
	V:views视图逻辑相关
	+url控制器，不同的路径找到不同的视图函数
```

#### 3.URL配置

```
urls.py文件中卸载urlpatterns=[]中
简单的路由
from app01 import views
	url(r'^index/',views.index),
	
无名分组
	url(r'^index/(/d+)/',views.index)		--def index(reguest,n,m)位置参数
	
有名分组
	url(r'^index/(?P<month>/d+)/',views.index)	
					--def index(request,month)关键字参数
视图函数参数默认值(没匹配上会使用默认值)
url(r'^index/$',views.index),注意这个$的使用，否则后续正则可能匹配不上
url(r'^index/(?P<num>/d+)/',views.index)
	def index(request,num='1'):
		print(num)
```

