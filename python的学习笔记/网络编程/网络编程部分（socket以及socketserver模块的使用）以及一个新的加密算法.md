### 网络编程部分（socket以及`socketserver`模块的使用）以及一个新的加密算法

#### 1.socket模块的使用

##### socket模块是python内置的用于网络传输的模块，在这个网络编程的模块中，我们都会讲程序分为server端以及client端进行使用，首先进行最简单的socket模块的使用

+ ##### client端

```python
import socket
sk=socket.socket()		#实例化一个socket对象
sk.connect(('127.0.0.1',9001))		#通过ip地址以及端口号对server端进行连接

meg=sk.recv(1024)		#从server端接收信息
print(meg)
sk.send(b'byebye')		#向server端发送信息


sk.close()		#关闭一个client端的服务
```



+ ##### server端

```python
import socket
sk=socket.socket()		#实例化一个socket对象
sk.bind(('127.0.0.1',9001))		#进行ip地址的以及端口的绑定，端口被占用会报错
sk.listen()		#进行监听，看是否有client端接入

coon,addr=sk.accept()		#对接入的client短的对象进行接收，得到一个对象和一个地址
coon.send(b'hello')		#向client端发送信息
meg=coon.recv(1024)		#按字节数从client端接收信息
print(meg)
coon.close()		#关闭一个服务


sk.close()		#关闭服务器
```

#### 2.udp协议的使用

##### 在进行socket对象的创建时，我们默认的是进行`tcp`协议的连接，如果使用`udp`协议的话，需要在server端进行实例化的时候传入特定的参数（client端的代码和`tcp`协议下的代码基本一模一样）

+ ##### client端

```python
import socket
sk=socket.socket(type=socket.SOCK_DGRAM)	#这里是将协议改为udp协议
	
sever=('127.0.0.1',9000)		#这里是得到一个服务的元组
sk.sendto(b'info',sever)		#因为没有进行连接，所以需要用sendto函数
```

+ ##### server端

```python
import socket
sk=socket.socket(type=socket.SOCK_DGRAM)
sk.bind(('127.0.0.1',9000))		#这里依旧需要进行端口以及ip地址的绑定


meg,addr=sk.recvfrom(1024)		#通过recvfrom函数得到内容以及地址的信息
print(meg)
sk.sendto(meg,addr)		#使用sendto函数进行内容的发送
```

#### 3.socket的高级应用

##### 内容的上传

+ ##### client端

```python
import socket
import os
import struct
import json

sk=socket.socket()
sk.connect(('127.0.0.1',9000))

abs_path=r'E:\Adobe Premiere Pro CC 2018 SP\树莓派自动投放地面测试.mp4'
length=os.path.getsize(abs_path)	#获得文件的大小
name=os.path.basename(abs_path)		#获得文件的名字
dic={'name':name,'length':length}	#先通过字典得到一个名字和文件的大小
js=json.dumps(dic)			#使用json将字典转化为字符串
ms=js.encode('utf-8')		#对字符串进行编码
size=struct.pack('i',len(ms))		#struct这个类中的pack可以将一个int大小的数转化为四个字节的二进制码，后面的参数是*args所以可以传入多个值来进行打包，接收端收到的是一个元组，可以通过这个方法来避免粘包的现象产生
sk.send(size)	#先进行大小的发送
sk.send(ms)		#再将字典进行发送

with open(abs_path,mode='rb') as f:
    while length>0:
        sk.send(f.read(1024))
        length-=1024		#发送文件的内容

sk.close()
```

+ ##### server端

```python
import socket
import json
import struct

sk=socket.socket()
sk.bind(('127.0.0.1',9000))
sk.listen()

conn,_=sk.accept()
num=struct.unpack('i',conn.recv(4))[0]	#使用unpack得到一个元组，第一个元素就是传输的大小的二进制码，其实这个元组中就一个元素。
dic=conn.recv(num).decode('utf-8')	#解码
dic=json.loads(dic)
length=dic['length']
name=dic['name']
with open(name,mode='wb') as f:
    while length>0:
        res=conn.recv(1024)		#进行接收
        f.write(res)
        length-=len(res)		#每次最多收1024字节，但是每一次不一定会接收到1024字节，所以length应该减的是收到的字节，而不是最大字节数

conn.close()

sk.close()
```

#### 4.socketserver的使用

##### `socketserver`是一个可以使用并发的模块，通过这个模块可以使用`tcp`协议并且连接多个client端

+ ##### server端

```python
import socketserver
import time

class myserver(socketserver.BaseRequestHandler):	#创建一个类，并继承特定的类
    def handle(self):		#重写特定的函数
        conn = self.request		#这里的request中存的就是conn的信息
        while True:
            try:
                conn.send(b'hello')
                time.sleep(0.5)
            except ConnectionResetError:break	#这里写需要执行的代码

sk = socketserver.ThreadingTCPServer(('127.0.0.1', 9000), myserver)	#实例化
sk.serve_forever()		#让server端始终运行
```

+ ##### client端（与socket中`tcp`协议的client端的代码完全相同）

```python
import socket

sk=socket.socket()

sk.connect(('127.0.0.1',9000))
while True:
    meg = sk.recv(1024)
    print(meg.decode('utf-8'))
```

##### 5.传输过程中的加密方法

```python
import os
import hashlib
ret=os.urandom(32)    #创建一个32位的随机字符串（bytes类型）

sha=hashlib.sha1(b'alex_sb')
sha.update(ret)
res=sha.hexdigest()


#或者
import os
import hmac

h=hmac.new(b'alex_nb',os.urandom(32))  #盐和字符串
ret=h.digest() 
#直接就是一个二进制了，不用在转了，相较于hashlib模块更加的方便
```