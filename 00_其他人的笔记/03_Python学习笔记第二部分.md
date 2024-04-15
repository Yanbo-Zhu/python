
## 0.1 第八章 网络编程

网络编程：http://www.cnblogs.com/Eva-J/articles/8244551.html

### 0.1.1 网络基础

- 网络应用开发架构

  - C/S  有客户端软件
    - client  客户端
    - server  服务端
  - B/S   没有客户端的
    - browser   浏览器
    - server    服务端
  - B/C是特殊的C/S架构

- 计算机相关知识：

  - 网卡：是一个实际存在在计算机中的硬件

  - mac地址：每一个网卡上都有一个全球唯一的mac地址

  - 交换机：是连接多台机器并帮助通讯的物理设备，只认识mac地址（通讯方式有单播、组播、广播）

  - 协议 ：两台物理设备之间对于要发送的内容，长度，顺序的一些约定

  - ip地址

    - ip地址可以在网络上定位一台机器
    - ipv4
    - ipv6
  
    ```python
    ipv4协议 4位的点分十进制  32位2进制表示
  0.0.0.0 - 255.255.255.255
    ipv6协议 6位的冒分十六进制 128位2进制表示
  0:0:0:0:0:0-FFFF:FFFF:FFFF:FFFF:FFFF:FFFF
    ```

  - 公网ip：每一个ip地址要想被所有人访问到，那么这个ip地址必须是你申请的
  
  - 内网ip
  
  ```python
192.168.0.0 - 192.168.255.255
  172.16.0.0 - 172.31.255.255
  10.0.0.0 - 10.255.255.255
  ```
  
  - 交换机实现arp协议：
    - 通过ip地址获取一台机器的mac地址
    - 通过交换机完成
    - 广播  单播
  - 网管 ip：一个局域网的网络出口，访问局域网之外的区域都需要经过路由器和网关
  - 网段：指一个地址段
  - 子网掩码：判断机器是否在同一个网段内
  - port端口：0-65535  ip+port确认一台机器上的一个应用
  - 路由器 ： 完成局域网与局域网直接的联系
    - 能识别ip地址
    - 网段
    - 网关ip（访问局域网外部服务的一个出口ip）

### 0.1.2 解决tcp协议和udp协议的socket

TCP与UDP的各自应用场景

- TCP  文件的上传下载（发送邮件、网盘、缓存电影）
- UDP  及时通信类（qq、微信、飞秋）

#### 0.1.2.1 TCP/ip协议

- TCP/IP协议的特点
  - 流式的、可靠、慢、全双工通信（又称为双向同时*通信*，即*通信*的双方可以同时发送和接收信息的信息交互方式）
  - 建立连接的时候：三次握手
  - 端口连接的时候：四次挥手
  - 建立起连接之后
    - 发送的每一层信息都有回执
    - 为了保证数据完整性，有重传机制
  - 长连接：会一直占用双方的端口
  - IO（input，output）操作，输入和输出是相对内存来说的
    - write send -  output
    - read  recv  -  input
  - 对传输的数据长度机会没有限制
  - 应用场景
- 三次握手  svn ack
  - accept接受过程中等待客户端的链接
  - connect客户端发起一个svn链接请求
    - 如果得到了server端相应ack的同时还会再收到一个由server端发来的svn链接请求。
    - client端进行回复ack之后，就建立起了一个tcp协议的链接
    - 三次握手的过程在代码中是由accept和connect共同完成的，具体细节在socket中没有体现出来。
- 四次挥手  fin ack
  - server和client端对应的正在代码中都有close方法，每一段发起的close操作都是一次fin的断开请求，得到断开确认ack之后就可以结束一端的数据发送，如果两端都发起close，那么就是两次请求和两次回复，共四次操作，之后就可以结束两端的数据发送，表示连接断开了。
  - 区别：三次握手把一个回复和请求连接的两条信息合并成了一条，四次挥手是由于一方断开连接之后，可能另一方还有数据没有传递完，所以不能立即断开，故挥手的时候不能合并信息。

#### 0.1.2.2 UDP协议

- UDP协议的特点：面向数据、无连接、不可靠、快、数据长度小、多方传输的高效通信协议。

```python
#client 端
import socket

sk = socket.socket(type=socket.SOCK_DGRAM)
while True:
    inp = input('>>>').encode('utf-8')
    sk.sendto(inp,('127.0.0.1',9000))
    ret = sk.recv(1024)
    print(ret)
sk.close()
#server 端
import socket
sk = socket.socket(type = socket.SOCK_DGRAM)
sk.bind(('127.0.0.1',9000))
while True:
    msg,client_addr = sk.recvfrom(1024)
    print(msg.decode('utf-8'))
    msg = input('>>>').encode('utf-8')
    sk.sendto(msg,client_addr)
sk.close()
```



#### 0.1.2.3 osi七层模型

- osi七层模型
  - 应用层
  - 表示层
  - 会话层
  - 传输层
  - 网络层
  - 数据链路层
  - 物理层
- osi五层协议          协议                  物理设备
  - 应用层    http https ftp smtp
  - 传输层     tcp/udp协议  端口     四层交换机、四层路由器
  - 网络层     ipv4/ipv6协议            路由器、三层交换机
  - 数据链路层  mac地址  arp协议    网卡、交换机
  - 物理层

- 每一次的物理设备
- 每一层的常见协议



8.2.4   socket代码部分

- socket（套接字）（英文直译为插座，表示不同的插座提供不同的服务功能）

  ![`CYD601}A~E0ILH0RH8CZ9C](E:\视频及作业\day28\讲课截图\`CYD601}A~E0ILH0RH8CZ9C.png)

  - python中socket模块

  - 工作在应用层和传输层直接的抽象层

    - 帮助我们完成所有信息的组织和拼接

  - socket对于程序员来说已经是网络操作的底层

  - socket历史

    - 同一台机器上的两个服务直接的通信

      - 基于文件
- 基于网络
      

- 使用socket完成tcp协议的web通信

- 使用socket完成udp协议的web通信

### 0.1.3 解决tcp协议的粘包问题

粘包现象（本质是由于tcp协议接收信息的边界不清晰）：

- 发生在发送端的粘包：由于两个数据的发送时间间隔短以及数据长度小，所以由于tcp的优化机制将两条信息作为一条信息发送出去了。（为了减少tcp协议中的‘确认收到’的网络延迟时间）
- 发生在接收端的粘包：由于tcp传输的数据无边界，所以来不及接收多条信息时数据会在接收方的内核缓存段粘在一起。

- struct模块
  - 首先发送报头，报头长度4个字节，报头内容及发送的报文的字节长度。（struct模块的pack能够把所有的数字都固定的转换成4字节）

```python
import struct
ret = struct.pack('i',1000)
```

```python
#server端
import struct
import socket
sk = socket.socket()
sk.bind(('127.0.0.1',9000))
sk.listen()
conn,_ = sk.accept()
byte_len = conn.recv(4)
size = struct.unpack('i',byte_len)[0]
msg1 = conn.recv(size).decode('gbk')
msg = conn.recv(1024)
print(byte_len,msg1,msg)
conn.close()
sk.close()
#client端
import socket
import struct
sk = socket.socket()
sk.connect(('127.0.0.1',9000))
info = '还会哈速递啊圣诞节哦和空间大声道'.encode('gbk')
info_len = struct.pack('i',len(info))
sk.send(info_len)
sk.send(info)
sk.send(b'aaaaaaa')
sk.send(b'bbbbbbbb')

sk.close()
```

- 自定义协议2
  - 自定义的专门用来做文件发送解决粘包问题的协议
  - 先发送报头字典的字节长度
  - 再发送字典（字典中包含文件的名字、大小等内容）
  - 再发送文件的内容

### 0.1.4 并发问题

#### 0.1.4.1 socket 阻塞和非阻塞 tcp协议可以并发通信的socketserver

- 非阻塞io模型

```python
#server端
import socket
sk = socket.socket()
sk.bind(('192.168.12.60',6666))
sk.setblocking(False)
sk.listen()
conn_l = []
del_l = []
while True:
    try:
        conn,addr = sk.accept()   # 阻塞，直到有一个客户端来连我
        print(conn)
        conn_l.append(conn)
    except BlockingIOError:
        for c in conn_l:
            try:
                msg = c.recv(1024).decode('utf-8')
                if not msg:
                    del_l.append(c)
                    continue
                print('-->',[msg])
                c.send(msg.upper().encode('utf-8'))
            except BlockingIOError:pass
        for c in del_l:
            conn_l.remove(c)
        del_l.clear()
sk.close()
#socket的非阻塞io模型+io多路复用实现的，虽然非阻塞，提高了cup的利用率，但是耗费cpu做了很多无用功。
#client端
import socket
import time
sk = socket.socket()
sk.connect(('127.0.0.1',9000))
while True:
    sk.send(b'wusir')
    msg = sk.recv(1024)
    print(msg)
    time.sleep(0.2)
sk.close()
```



#### 0.1.4.2 验证客户端的合法性--自动化开发

- 验证客户端的合法性一

```python
#server端
import os
import hashlib
import socket

def get_md5(secret_key,randseq):
    md5 = hashlib.md5(secret_key)
    md5.update(randseq)
    res = md5.hexdigest()
    return res

def chat(conn):
    while True:
        msg = conn.recv(1024).decode('utf-8')
        print(msg)
        conn.send(msg.upper().encode('utf-8'))

sk = socket.socket()
sk.bind(('127.0.0.1',9000))
sk.listen()

secret_key = b'alexsb'
while True:
    conn,addr = sk.accept()
    randseq = os.urandom(32)
    conn.send(randseq)
    md5code = get_md5(secret_key,randseq)
    ret = conn.recv(32).decode('utf-8')
    print(ret)
    if ret == md5code:
        print('是合法的客户端')
        chat(conn)
    else:
        print('不是合法的客户端')
        conn.close()
sk.close()
#client端
import hashlib
import socket
import time

def get_md5(secret_key,randseq):
    md5 = hashlib.md5(secret_key)
    md5.update(randseq)
    res = md5.hexdigest()
    return res
def chat(sk):
    while True:
        sk.send(b'hello')
        msg = sk.recv(1024).decode('utf-8')
        print(msg)
        time.sleep(0.5)
sk = socket.socket()
sk.connect(('127.0.0.1',9000))

secret_key = b'alexsb'
randseq = sk.recv(32)
md5code = get_md5(secret_key,randseq)

sk.send(md5code.encode('utf-8'))
chat(sk)

sk.close()
```

- 验证客户端的合法性二

```python
#server端
import os
import hmac
import socket

def get_md5(secret_key,randseq):
    h = hmac.new(secret_key,randseq)
    res = h.digest()
    return res

def chat(conn):
    while True:
        msg = conn.recv(1024).decode('utf-8')
        print(msg)
        conn.send(msg.upper().encode('utf-8'))

sk = socket.socket()
sk.bind(('127.0.0.1',9000))
sk.listen()

secret_key = b'alexsb'
while True:
    conn,addr = sk.accept()
    randseq = os.urandom(32)
    conn.send(randseq)
    hmaccode = get_md5(secret_key,randseq)
    ret = conn.recv(16)
    print(ret)
    if ret == hmaccode:
        print('是合法的客户端')
        chat(conn)
    else:
        print('不是合法的客户端')
        conn.close()
sk.close()
#client端
import socket
import time
import hmac

def get_md5(secret_key,randseq):
    h = hmac.new(secret_key,randseq)
    res = h.digest()
    return res
def chat(sk):
    while True:
        sk.send(b'hello')
        msg = sk.recv(1024).decode('utf-8')
        print(msg)
        time.sleep(0.5)

sk = socket.socket()
sk.connect(('127.0.0.1',9000))

secret_key = b'alexsb'
randseq = sk.recv(32)
hmaccode = get_md5(secret_key,randseq)

sk.send(hmaccode)
chat(sk)

sk.close()
```



#### 0.1.4.3 socketserver模块  直接实现tcp协议可并发的server端

```python
#server端
import socketserver

class Myserver(socketserver.BaseRequestHandler):
    def handle(self):  # 自动触发了handle方法，并且self.request == conn
        msg = self.request.recv(1024).decode('utf-8')
        self.request.send('1'.encode('utf-8'))
        msg = self.request.recv(1024).decode('utf-8')
        self.request.send('2'.encode('utf-8'))
        msg = self.request.recv(1024).decode('utf-8')
        self.request.send('3'.encode('utf-8'))

server = socketserver.ThreadingTCPServer(('127.0.0.1',9000),Myserver)
server.serve_forever()
#client端
import socket
import time
sk = socket.socket()
sk.connect(('127.0.0.1',9000))
for i in range(3):
    sk.send(b'hello,wusir')
    msg = sk.recv(1024)
    print(msg)
    time.sleep(1)

sk.close()
```



## 0.2 第九章 并发编程

- 操作系统
  - 计算机中所有的资源都是由操作系统分配的
  - 操作系统调度任务：时间分片、多道机制
  - cpu的利用率是我们努力的指标
- 并发
  - 进程：开销大、数据隔离、资源分配单位 cpython下可以利用多核
    - 进程的三状态：就绪 运行 阻塞
    - multiprocessing模块
      - Process-开启进程
      - Lock--互斥锁
      - Queue
      - Manager
  - 线程：开销小 数据共享 cpu调度单位 cpython不能利用多核

### 0.2.1 操作系统的基础知识

- 操作系统的发展史
  
  - 操作系统负责什么：
    
    - 调度进程先后执行的顺序 控制执行的时间等
    - 资源的分配
    
  - 人机矛盾：cou利用率低
  
  - 磁带存储+批处理
    - 降低数据的读取时间
    - 提高cpu利用率
  
  - 多道操作系统--在一个任务遇到io的时候主动让出cpu
    - 数据隔离
    - 时空复用
    - 能够在一个任务遇到io操作的时候主动把cpu让出来，给其他的任务使用
      - 切换会占用时间
      - 切换是操作系统在做
  
  - 分时操作系统 -- 给时间分片，让多个任务轮流使用cpu
    - cpu轮转
    - 每一个程序分配一个时间片
    - 切换时也会占用时间因而降低了cpu的利用率
    - 但是也提高了用户体验
    
  - 实时操作系统
  
  - 分时操作系统+多道操作系统+实时操作系统
    - 多个程序一起在计算机中执行
    - 一个程序如果遇到了io操作，却出去让出cpu
    - 一个程序没有遇到io，但是时间片到时间了切出去让出cpu
  - 网络操作系统
    - 分布式操作系统
- IO操作：
  - i input向内存输入input  read  recv recvfrom accept close
  - o output内存输出print write send sendto accept connect close

### 0.2.2 进程

#### 0.2.2.1 进程的概念

- 进程：运行中的程序。进程是计算机中最小的资源分配单位
- 程序和进程直接的区别：程序只是一个文件，进程是这个文件被cpu运行起来了。
- 在操作系统中唯一的标识符：pid
- 操作系统调度进程的算法：1.短作业优先 2.先来优先 3. 时间片轮转 4.多级反馈算法
- 进程的三状态图：就绪、运行、阻塞

![%N~U1FRI25TX4ZHIF80J~}9](E:\视频及作业\day31\讲课图片\%N~U1FRI25TX4ZHIF80J~}9.png)

- 创建进程和销毁进程或进程直接的切换时间开销都比较大

- 并发和并行
  - 并行：两个程序，两个cpu分别运行，虽是同时进行，实际每个都在同时间各自执行
  - 并发：两个程序一个cpu，每个程序交替在一个cpu上执行，看起来是同时执行，实际上仍串行。

- 阻塞和非阻塞
  - 阻塞：cpu不工作
  - 非阻塞：cpu工作

- 同步和异步
  - 同步：执行A的同时来了任务B，停下了A任务执行B任务之后再执行A任务。
  - 异步：AB任务同时执行。
  - 同步阻塞：conn.recv    socket 阻塞的tcp协议的时候
  - 同步非阻塞：1.没有io操作 2.非阻塞的tcp协议的时候  3.调用函数（这个函数内部不存在io操作）
  - 异步非阻塞：1.把func扔到其他任务里去执行  2.本身任务各自执行，没有io操作
  - 异步阻塞

#### 0.2.2.2 进程processing类

- 子进程、父进程：在父进程中创建子进程

- pycharm中启动的所有py程序都是pycharm的子进程

- 获得进程pid（process id）和ppid（parent process id）

  ```python
  import os
  import time
  print('start')
  time.sleep(2)
  print(os.getpid(),os.getppid(),'end')#第一个当前进程的pid，第二个是python的pid。
  ```

  ```python
  import os
  import time
  from multiprocessing import Process
  def func():
      print('start',os.getpid())
      time.sleep(1)
      print('end',os.getpid())
  if __name__ == '__main__':
      p = Process(target=func)
      p.start()#异步 调用开启进程的方法，但是并不等待这个进程真的开启。
      print('main',os.getpid())
  ```

  ```python
  import os
  import time
  from multiprocessing import Process
  def eat():
      print('start eating',os.getpid())
      time.sleep(1)
      print('end eating',os.getpid)
  def sleep():
      print('start sleeping',os.getpid())
      time.sleep(1)
      print('end sleeping',os.getpid())
  if __name__ =='__main__':
      p1 = Process(target=eat)#创建一个即将要执行eat函数的进程对象
      p1.start()#开启进程
      p2 = Process(target=sleep)#开启一个即将要执行sleep函数的进程对象
      p2.start()#开启进程
      print('main:',os.getpid())
      
  ```

  ```python
  import os
  import time
  from multiprocessing import Process
  def func():
      print('start',os.getpid())
      time.sleep(1)
      print('end',os.getpid())
  if __name__ == '__main__':
      p = Process(target=func)
      p.start()
      print('main:',os.getpid())
  ```

9.2.3   操作系统创建进程的方式不同

- windows操作系统执行开启进程的代码
  - 实际上新的子进程需要通过import父进程的代码来完成数据的导入工作
  - 所以有一些内容我们只希望在父进程中完成，就写在if __ name __ = '__ main __' 下面
- ios Linux操作系统创建进程 fork

9.2.4   主进程和子进程之间的关系

- 如何创建一个进程对象
  - 对象和进程直接的关系
    - 进程对象和进程并没有直接关系
    - 只是存储了一些和进程相关的内容
    - 此时此刻，操作系统还没有接到创建进程的指令
- 开启一个进程
  - 函数名（参数1，参数2）
  - from multiprocessing import Process
  - p = Process(target=函数名,args=(参数1，参数2))
  - p.start()
- 父进程和子进程
- 父进程会等待所有的子进程结束之后才结束
  - 为了回收资源
- 进程开启的过程中Windows和Linux/iOS之间的区别
  - Windows开启进程的过程需要将if __ name __ =='__ main __' 下，除了放在 __ if  __  __ name __ =='__ main __' 下的代码从头到尾执行了一遍。
  - Linux中不需要执行代码，直接执行调用的func函数
- join方法
  - 把一个进程的结束事件封装成一个join方法
  - 执行join方法的效果就是阻塞知道这个子进程执行结束就结束阻塞
  - 在多个进程中使用join方法

```python
pv = []
for i in range(10):
    p = Process(target=func,args=(canshu1,canshu2))
    p.start()
    pv.append(p)
    for p in pv:p.join()
    所有子进程都结束之后要执行的代码写在这里
```



```python
import os
import time
from multprocessing import Process
def func():
    print('start',os.getpid())
    time.sleep(10)
    print('end',os.getpid())
if __name__ =='__main__':
    p = Process(target=func)
    p.start()#异步 调用开启进程的方法 但是并不灯带这个进程真的开启
    print('main:',os.getpid())
```

- 主进程没有结束：等待子进程结束
- 主进程负责回收子进程的资源
- 如果子进程执行结束，父进程没有回收资源，那么这个子进程会变成一个僵尸进程
- 主进程的结束逻辑
  - 主进程的代码结束
  - 所有的子进程结束
  - 给子进程回收资源
  - 主进程结束
- 主进程怎么知道进程结束了？
  - 基础网络、文件
- join方法：阻塞，直到子进程结束就结束

```python
import time
from multiprocessing import Process
def send():
    time.sleep(3)
    print('send email successful')
if __name__ == '__main__':
    p = Process(target=send)
    p.start()#异步 非阻塞
    time.sleep(5)
    print('join start')
    p.join()#同步 阻塞 直到p对应的进程结束之后才结束阻塞
    print('the end')
```

- 开启10个进程，给公司的5000个人发邮件，发送完邮件之后，打印消息’5000封邮件已发送‘

```python
import time
import random
from multiprocessing import Process
def send_mail(a):
    time.sleep(random.random())
    print('发送了一封邮件',a)
if __name__ == '__main__':
    l = []
    for i in range(10):
        p = Process(target=send_mail,args=(i,))
        p.start()
        l.append(p)
    print(l)
    for p in l:p.join()
    print(l)
    # 阻塞 直到上面的十个进程都结束
    print('5000封邮件已发送完毕')

```

#### 0.2.2.3 守护进程

- 有一个参数可以把一个子进程设置为一个守护进程
- 守护进程是随着主进程的代码结束而结束的
  - 生产者消费者模型的时候
  - 和守护线程做对比的时候
- 所有的子进程都必须在主进程结束之前结束，由主进程来负责回收资源
- 开启进程的方式
  - 面向函数
    - def 函数名：要在子进程中执行的代码
    - p = Process(target=函数名，args=(参数1，))
  - 面向对象
    - class类名(Process):
      - def __ init __ (self,a，b)：
        - self.a = a
        - self.b = b
        - super(). __ init __ ()
      - def run(self):
        - 要在子进程中执行的代码
    - p = 类名(参数1，参数2)
  - Process提供的操作进程的方法
    - p.start() 开启进程     异步非阻塞
    - p.terminate() 结束进程   异步非阻塞
    - p.join()    同步阻塞
    - p.isalive() 获取当前进程的状态
    - daemon = True   设置为守护进程，守护进程永远在主进程的代码结束之后自动结束

```python
import time
from multiprocessing import Process
def son1(a,b):
    while True:
        print('is alive')
        time.sleep(0.5)
def son2():
    for i in range(5):
        print('in son2')
        time.sleep(1)
if __name__ == '__main__':
    p = Process(target=son1,args=(1,2))
    p.daemon = True
    p.start()      # 把p子进程设置成了一个守护进程
    p2 = Process(target=son2)
    p2.start()
    time.sleep(2)
```

- terminate() 终止程序

```python
import time
from multiprocessing import Process

def son1():
    while True:
        print('is alive')
        time.sleep(0.5)

if __name__ == '__main__':
    p = Process(target=son1)
    p.start()      # 异步 非阻塞
    print(p.is_alive())
    time.sleep(1)
    p.terminate()   # 异步的 非阻塞
    print(p.is_alive())   # 进程还活着 因为操作系统还没来得及关闭进程
    time.sleep(0.01)
    print(p.is_alive())   # 操作系统已经响应了我们要关闭进程的需求，再去检测的时候，得到的结果是进程已经结束了
```

- 面向对象方式

```python
import os
import time
from multiprocessing import Process
class MyProcecss2(Process):
    def run(self):
        while True:
            print('is alive')
            time.sleep(0.5)
class MyProcecss1(Process):
    def __init__(self,x,y):
        self.x = x
        self.y = y
        super().__init__()
    def run(self):
        print(time.time(),1)
        print(self.x,self.y,os.getpid())
        for i in range(5):
            print('in son2')
            time.sleep(1)
if __name__ == '__main__':
    mp = MyProcecss1(1,2)
    mp.daemon = True
    mp.start()
    print(time.time(),2)
    print(mp.is_alive())
    mp.terminate()
    mp2 = MyProcecss2()
    mp2.start()
    print('main :',os.getpid())
    time.sleep(1)
```



#### 0.2.2.4 锁的概念

- 进程池和线程池都有锁
  - 所有在线程中能工作的基本都不能在进程中工作
  - 在进程中能够使用的基本在线程中也可以使用

##### 0.2.2.4.1 进程锁

- 如果在一个并发的场景下，涉及到某部分内容
  - 是需要修改一些所有进程共享数据资源
  - 需要加锁来维护数据的安全
- 在数据的安全基础上才考虑效率问题
- 同步存在的意义：数据的安全性
- 在主进程中实例化 lock = Lock()
- 把这个锁传递给子进程
- 在子进程中对需要枷锁的代码进行 with lock:
  - with lock 相当于lock.acquire()和lock.release()
- 在进程中需要加锁的场景
  - 共享数据资源（文件、数据库）
  - 对资源进行修改、删除操作
- 加锁之后能够保证数据的安全性，但也降低了程序的执行效率
- 实现能够相应多个client端的server的抢票系统

```python
import time
import json
from multiprocessing import Process,Lock
def search_ticket(user):
    with open('ticket_count') as f:
        dic = json.load(f)
        print('%s查询结果  : %s张余票'%(user,dic['count']))
def buy_ticket(user,lock):
    # with lock:
    # lock.acquire()   # 给这段代码加上一把锁
        time.sleep(0.02)
        with open('ticket_count') as f:
            dic = json.load(f)
        if dic['count'] > 0:
            print('%s买到票了'%(user))
            dic['count'] -= 1
        else:
            print('%s没买到票' % (user))
        time.sleep(0.02)
        with open('ticket_count','w') as f:
            json.dump(dic,f)
    # lock.release()   # 给这段代码解锁
def task(user, lock):
    search_ticket(user)
    with lock:
        buy_ticket(user, lock)
if __name__ == '__main__':
    lock = Lock()
    for i in range(10):
        p = Process(target=task,args=('user%s'%i,lock))
        p.start()
```

##### 0.2.2.4.2 线程锁

- 为什么要用锁

  - 由于线程中的数据共享，以及线程的并发机制，和cpu时间片轮转机制，所以导致有可能某线程未全部运行完毕，导致线程切换导致数据的混乱。
  - dis.dis(函数) 查看函数执行代码数
  - 不加锁可能会出现数据混乱

  ```python
  from threading import Thread
  a = 0
  def ad():
      global a
      for i in range(1000):
          a +=1
  def su():
      global a
      for i in range(1000):
          a -= 1
  ta = Thread(target = ad)
  ts = Thread(target = su)
  ta.start()
  ts.start()
  ta.join()
  ts.join()
  print(a)
  
  ```

  - 加锁虽然会降低执行效率，但是保证了数据的稳定性和安全性

  ```python
  a = 0
  def add_f(lock):
      global a
      for i in range(200000):
          with lock:
              a += 1
  
  def sub_f(lock):
      global a
      for i in range(200000):
          with lock:
              a -= 1
  
  from threading import Thread,Lock
  lock = Lock()
  t1 = Thread(target=add_f,args=(lock,))
  t1.start()
  t2 = Thread(target=sub_f,args=(lock,))
  t2.start()
  t1.join()
  t2.join()
  print(a)
  ```

- 互斥锁也是锁的一种：在同一个线程中，不能连续acquire多次，效率高，产生死锁的几率高

```python
from threading import Lock
lock = Lock()
lock.acquire()
print('*'*20)
lock.release()
lock.acquire()
print('-'*20)
lock.release()
```

- 单列模式

```python
import time
from threading import Lock
class A:
    __instance = None
    lock = Lock()
    def __new__(cls, *args, **kwargs):
        with cls.lock:
            if not cls.__instance:
                time.sleep(0.1)
                cls.__instance = super().__new__(cls)
        return cls.__instance
    def __init__(self,name,age):
        self.name = name
        self.age = age

def func():
    a = A('alex', 84)
    print(a)

from threading import Thread
for i in range(10):
    t = Thread(target=func)
    t.start()
```

- 使用互斥锁产生的一个死锁现象
  - 在一个线程中连续多次acquire会死锁

```python
import time
from threading import Thread,Lock
noodle_lock = Lock()
fork_lock = Lock()
def eat1(name,noodle_lock,fork_lock):
    noodle_lock.acquire()
    print('%s抢到面了'%name)
    fork_lock.acquire()
    print('%s抢到叉子了' % name)
    print('%s吃了一口面'%name)
    time.sleep(0.1)
    fork_lock.release()
    print('%s放下叉子了' % name)
    noodle_lock.release()
    print('%s放下面了' % name)

def eat2(name,noodle_lock,fork_lock):
    fork_lock.acquire()
    print('%s抢到叉子了' % name)
    noodle_lock.acquire()
    print('%s抢到面了'%name)
    print('%s吃了一口面'%name)
    time.sleep(0.1)
    noodle_lock.release()
    print('%s放下面了' % name)
    fork_lock.release()
    print('%s放下叉子了' % name)

lst = ['alex','wusir','taibai','yuan']
Thread(target=eat1,args=(lst[0],noodle_lock,fork_lock)).start()
Thread(target=eat2,args=(lst[1],noodle_lock,fork_lock)).start()
Thread(target=eat1,args=(lst[2],noodle_lock,fork_lock)).start()
Thread(target=eat2,args=(lst[3],noodle_lock,fork_lock)).start()
```

- 递归锁
  - 在一个线程中连续多次acquire，效率低，一把锁永远不会产生死锁。
- 死锁现象
  - 有多把锁
  - 多把锁交替使用
- 死锁解决方案
  - 递归锁--把多把互斥锁编程一把递归锁
    - 可以快速解决问题
    - 效率较差
  - 递归锁也会发生死锁现象，多把锁交替使用的时候
  - 优化代码逻辑
    - 可以使用互斥锁解决问题
    - 效率相对好
    - 解决问题的效率相对低
- 互斥锁解决死锁

```python
import time
from threading import Lock,Thread
lock = Lock()
def eat1(name,noodle_lock,fork_lock):
    # lock.acquire()
    with noodle_lock:
        print('%s抢到面了'%name)
        with fork_lock:
            print('%s抢到叉子了' % name)
            print('%s吃了一口面'%name)
            time.sleep(0.1)
            print('%s放下叉子了' % name)
            print('%s放下面了' % name)
    # lock.release()

def eat2(name,noodle_lock,fork_lock):
    # lock.acquire()
    with noodle_lock:
        print('%s抢到叉子了' % name)
        with fork_lock:
            print('%s抢到面了'%name)
            print('%s吃了一口面'%name)
            time.sleep(0.1)
            print('%s放下面了' % name)
            print('%s放下叉子了' % name)
        # lock.release()

lst = ['alex','wusir','taibai','yuan']
noodle_lock = Lock()
fork_lock = Lock()
Thread(target=eat1,args=(lst[0],noodle_lock,fork_lock)).start()
Thread(target=eat2,args=(lst[1],noodle_lock,fork_lock)).start()
Thread(target=eat1,args=(lst[2],noodle_lock,fork_lock)).start()
Thread(target=eat2,args=(lst[3],noodle_lock,fork_lock)).start()
```

- 递归锁
  - 在同一个线程中，可以连续acquire多次不会被锁住
  - 优点：在同一个进程中多次acquire也不会发生阻塞
  - 缺点：占用了更多资源

```python
from threading import RLock
rlock = RLock()
rlock.acquire()
print('*'*20)
rlock.acquire()
print('-'*20)
rlock.acquire()
print('*'*20)
```

```ptyhon
import time
from threading import RLock,Thread
# noodle_lock = RLock()
# fork_lock = RLock()
noodle_lock = fork_lock = RLock()
print(noodle_lock,fork_lock)
def eat1(name,noodle_lock,fork_lock):
    noodle_lock.acquire()
    print('%s抢到面了'%name)
    fork_lock.acquire()
    print('%s抢到叉子了' % name)
    print('%s吃了一口面'%name)
    time.sleep(0.1)
    fork_lock.release()
    print('%s放下叉子了' % name)
    noodle_lock.release()
    print('%s放下面了' % name)

def eat2(name,noodle_lock,fork_lock):
    fork_lock.acquire()
    print('%s抢到叉子了' % name)
    noodle_lock.acquire()
    print('%s抢到面了'%name)
    print('%s吃了一口面'%name)
    time.sleep(0.1)
    noodle_lock.release()
    print('%s放下面了' % name)
    fork_lock.release()
    print('%s放下叉子了' % name)

lst = ['alex','wusir','taibai','yuan']
Thread(target=eat1,args=(lst[0],noodle_lock,fork_lock)).start()
Thread(target=eat2,args=(lst[1],noodle_lock,fork_lock)).start()
Thread(target=eat1,args=(lst[2],noodle_lock,fork_lock)).start()
Thread(target=eat2,args=(lst[3],noodle_lock,fork_lock)).start()
```

- 线程队列
  - 先进先出Queue

```python
from queue import Queue  # 先进先出队列
q = Queue(5)
q.put(0)
q.put(1)
q.put(2)
q.put(3)
q.put(4)
print('444444')

print(q.get())
print(q.get())
print(q.get())
print(q.get())
print(q.get())
print(q.get())
```

- 后进先出LifoQueue

```python
from queue import LifoQueue  # 后进先出队列
# last in first out 栈
lfq = LifoQueue(4)
lfq.put(1)
lfq.put(3)
lfq.put(2)
print(lfq.get())
print(lfq.get())
print(lfq.get())
```

- 优先级队列PriorityQueue

```python
from queue import PriorityQueue
pq = PriorityQueue()
pq.put((10,'alex'))
pq.put((6,'wusir'))
pq.put((20,'yuan'))
print(pq.get())
print(pq.get())
print(pq.get())
```

- 线程直接的通信 线程安全

- 池 concurrent.futrues
  - 进程池、线程池

#### 0.2.2.5 进程直接的通信

- 进程直接的数据隔离

```python
from multiprocessing import Process
n = 100
def func():
    global n
    n -= 1

if __name__ == '__main__':
    p_l = []
    for i in range(10):
        p = Process(target=func)
        p.start()
        p_l.append(p)
    for p in p_l:p.join()
    print(n)
```

- 通信
  - 进程之间通信- - IPC（inter process communication）
  - 内置模块（基于文件）：
    - Queue基于天生就是数据安全的
      - 文件家族的socket pickle lock
    - pipe管道（不安全）=文件加减的socket pickle
  - 队列 = 管道 + 锁
  - 第三方工具（软件）提供给我们的IPC机制（基于网络）：
    - Redis   memcache  kafka  rabbitmq
    - 并发需求、高可用、断电保存数据、解耦

```python
import queue

from multiprocessing import Queue
q = Queue(5)
q.put(1)
q.put(2)
q.put(3)
q.put(4)
q.put(5)   # 当队列为满的时候再向队列中放数据 队列会阻塞
print('5555555')
try:
    q.put_nowait(6)  # 当队列为满的时候再向队列中放数据 会报错并且会丢失数据
except queue.Full:
    pass
print('6666666')

print(q.get())
print(q.get())
print(q.get())   # 在队列为空的时候会发生阻塞
print(q.get())   # 在队列为空的时候会发生阻塞
print(q.get())   # 在队列为空的时候会发生阻塞
try:
    print(q.get_nowait())   # 在队列为空的时候 直接报错
except queue.Empty:pass
```

### 0.2.3 线程的概念

- 线程：
  - 线程是进程中的一部分，每一个进程中至少有一个线程
  - 进程是计算机中最小的资源分配单位（负责圈资源）
  - 线程是计算机中能被cpu调度的最小单位（线程负责执行具体代码）
  - 线程的创建也需要一些开销（一个存储局部变量的结构，记录状态）；创建、销毁、切换远远小于进程。
- python中的线程比较特殊，所以进程也有可能被用到。
- 进程：数据隔离 开销大 同时执行几段代码（目前项目不常用）
- 线程：数据共享 开销小 同时执行几段代码（爬虫、前段）
- 协程：异步的框架 异步爬虫模块
- 初始线程
  - 锁：GIL 全局解释器锁
    - 保证了整个python程序中只能有一个线程被CPU执行
    - 原因：cpython解释器中特殊的垃圾回收机制
    - GIL锁导致了在同一个进程中多个线程不能并行，可以并发
  - 所以使用线程并不影响高io型操作
  - 只会对高计算型的程序有效率上的影响
  - 遇到高计算：多进程 + 多线程        （分布式）
  - cpython   pypy    jpython    iron   python 
  - python解释器当中的线程问题
    - cpython解释器 不能实现多线程利用多核
  - python操作线程
    - 代码

多线程实现并发通信

```python
#server
import socket
from multiprocessing import Process
def chat(conn):
    while True:
        try:
            ret = conn.recv(1024).decode('utf-8')
            conn.send(ret.upper().encode('utf-8'))
        except ConnectionResetError:
            break

if __name__ == '__main__':
    sk = socket.socket()
    sk.bind(('127.0.0.1', 9000))
    sk.listen()
    while True:
        conn,_ = sk.accept()
        Process(target=chat,args=(conn,)).start()
 #client
import socket

sk = socket.socket()
sk.connect(('127.0.0.1',9000))
while True:
    sk.send(b'hello')
    msg = sk.recv(1024)
    print(msg)
```



### 0.2.4 生产者消费者模型

什么是生产者消费者模型：把一个生产数据并且处理数据的过程解耦，让生产数据的过程和处理数据的过程达到一个工作效率上的平衡，中间容器，在多进程中我们使用对着或者可被join的队列，做到控制数据的量，当数据过剩的时候，队列的大小会控制生产者的行为，当数据严重不足的时候，队列会控制消费者的行为，并且我们还可以通过定期检查队列中元素的个数来调节生产者消费者的个数。

- 爬虫
  - 请求网页的平均时间是0.3s
  - 处理网页代码的时间是0.003s
  - 根据差距可启动一个线程来处理数据，一百个线程生产数据
- web程序的server端
  - 一个服务每秒只能处理2000条
  - 先写一个web程序，只负责一件事情，就是接受请求，然后把请求放到队列中
  - 在写多个server端，从队列中获取请求然后处理，然后返回结果

- 解耦：方便修改、复用、可读性好（把卸载一起的大的功能分开多个小的功能处理）
- 进程
  - 一个进程就是一个生产者
  - 一个进程就是消费者
- 队列
  - 生产者和消费者之间的容器就是队列（容器有的也称为仓库）

```python
import time
import random
from multiprocessing import Process,Queue

def producer(q,name,food):
    for i in range(10):
        time.sleep(random.random())
        fd = '%s%s'%(food,i)
        q.put(fd)
        print('%s生产了一个%s'%(name,food))

def consumer(q,name):
    while True:
        food = q.get()
        if not food:break
        time.sleep(random.randint(1,3))
        print('%s吃了%s'%(name,food))


def cp(c_count,p_count):
    q = Queue(10)
    for i in range(c_count):
        Process(target=consumer, args=(q, 'alex')).start()
    p_l = []
    for i in range(p_count):
        p1 = Process(target=producer, args=(q, 'wusir', '烧饼'))
        p1.start()
        p_l.append(p1)
    for p in p_l:p.join()
    for i in range(c_count):
        q.put(None)
if __name__ == '__main__':
    cp(2,3)
```

```python
from multiprocessing import Process,Queue
import requests

import re
import json
def producer(q,url):
    response = requests.get(url)
    q.put(response.text)

def consumer(q):
    while True:
        s = q.get()
        if not s:break
        com = re.compile(
            '<div class="item">.*?<div class="pic">.*?<em .*?>(?P<id>\d+).*?<span class="title">(?P<title>.*?)</span>'
            '.*?<span class="rating_num" .*?>(?P<rating_num>.*?)</span>.*?<span>(?P<comment_num>.*?)评价</span>', re.S)
        ret = com.finditer(s)
        for i in ret:
            print({
                "id": i.group("id"),
                "title": i.group("title"),
                "rating_num": i.group("rating_num"),
                "comment_num": i.group("comment_num")}
            )

if __name__ == '__main__':
    count = 0
    q = Queue(3)
    p_l = []
    for i in range(10):
        url = 'https://movie.douban.com/top250?start=%s&filter='%count
        count+=25
        p = Process(target=producer,args=(q,url,)).start()
        p_l.append(p)
    p = Process(target=consumer, args=(q,)).start()
    for p in p_l:p.join()
    q.put(None)
```

joinablequeue的使用

```python
import time
import random
from  multiprocessing import JoinableQueue,Process

def producer(q,name,food):
    for i in range(10):
        time.sleep(random.random())
        fd = '%s%s'%(food,i)
        q.put(fd)
        print('%s生产了一个%s'%(name,food))
    q.join()

def consumer(q,name):
    while True:
        food = q.get()
        time.sleep(random.random())
        print('%s吃了%s'%(name,food))
        q.task_done()

if __name__ == '__main__':
    jq = JoinableQueue()
    p =Process(target=producer,args=(jq,'wusir','烧饼'))
    p.start()
    c = Process(target=consumer,args=(jq,'alex'))
    c.daemon = True
    c.start()
    p.join()
```

进程之间的数据共享

- multiprocessing中有一个manager类，封装了所有和进程相关的数据共享、数据传递，相关数据类型，但是对于字典、列表这一类的数据操作的时候会产生数据不安全，需要加锁解决问题，并且需要尽量少的使用这种方式，因为加锁会降低程序的运行效率。

```python
from multiprocessing import Manager,Process,Lock

def func(dic,lock):
    with lock:
        dic['count'] -= 1

if __name__ == '__main__':
    # m = Manager()
    with Manager() as m:
        l = Lock()
        dic = m.dict({'count':100})
        p_l = []
        for i in range(100):
            p = Process(target=func,args=(dic,l))
            p.start()
            p_l.append(p)
        for p in p_l:p.join()
        print(dic)
```

### 0.2.5 线程threading类

- 主线程等待所有子线程结束之后才结束
- 主线程如果结束了，主进程也就结束了
- 守护线程t.daemon =True 等待所有的非守护子线程都结束之后才结束
  - 非守护线程不结束，主线程也不结束
  - 主线程结束了，主进程也跟着结束
  - 结束顺序：非守护线程结束》》主线程结束》》子进程结束》》主进程结束》》守护线程也结束
- 开启多个子线程

```python
import os
import time
from threading import Thread
# multiprocessing 是完全仿照这threading的类写的
def func():
    print('start son thread')
    time.sleep(1)
    print('end son thread',os.getpid())
# 启动线程 start
Thread(target=func).start()
print('start',os.getpid())
time.sleep(0.5)
print('end',os.getpid())
```

- 线程的单例模式

```
import time
from threading import Lock
class A:
    __instance = None
    lock = Lock()
    def __new__(cls, *args, **kwargs):
        with cls.lock:
            if not cls.__instance:
                time.sleep(0.1)
                cls.__instance = super().__new__(cls)
        return cls.__instance
    def __init__(self,name,age):
        self.name = name
        self.age = age

def func():
    a = A('alex', 84)
    print(a)

from threading import Thread
for i in range(10):
    t = Thread(target=func)
    t.start()
```

```python
def func(i):
    print('start son thread',i)
    time.sleep(1)
    print('end son thread',i,os.getpid())

for i in range(10):
    Thread(target=func,args=(i,)).start()
print('main')
```

- join方法  阻塞 直到子线程执行结束

```python
def func(i):
    print('start son thread',i)
    time.sleep(1)
    print('end son thread',i,os.getpid())
t_l = []
for i in range(10):
    t = Thread(target=func,args=(i,))
    t.start()
    t_l.append(t)
for t in t_l:t.join()
print('子线程执行完毕')
```

- 面向对象的方式启动线程

```python
class MyThread(Thread):
    def __init__(self,i):
        self.i = i
        super().__init__()
    def run(self):
        print('start',self.i,self.ident)
        time.sleep(1)
        print('end',self.i)

for i in range(10):
    t = MyThread(i)
    t.start()
    print(t.ident)
```

- current_thread（在哪个线程中被调用得到当前线程的信息）
- enumerate（活跃的线程，返回列表）
- active_count(活跃的线程数)方法

```python
from threading import current_thread,enumerate,active_count
def func(i):
    t = current_thread()
    print('start son thread',i,t.ident)
    time.sleep(1)
    print('end son thread',i,os.getpid())

t = Thread(target=func,args=(1,))
t.start()
print(t.ident)
print(current_thread().ident)   # 水性杨花 在哪一个线程里，current_thread()得到的就是这个当前线程的信息
print(enumerate())
print(active_count())   # =====len(enumerate())
```

- 线程中不能从主线程结束一个子线程
- 进程和线程的效率对比（由于线程的数据共享的所以效率较高）

```python
def func(a,b):
    c = a+b
import time
from multiprocessing import Process
from threading import Thread
if __name__ == '__main__':
    start = time.time()
    p_l = []
    for  i in range(500):
        p = Process(target=func,args=(i,i*2))
        p.start()
        p_l.append(p)
    for p in p_l:p.join()
    print('process :',time.time() - start)

    start = time.time()
    p_l = []
    for i in range(500):
        p = Thread(target=func, args=(i, i * 2))
        p.start()
        p_l.append(p)
    for p in p_l: p.join()
    print('thread :',time.time() - start)
```

- 线程中主线程跟子线程是数据共享的

```python
from threading import Thread
n = 100
def func():
    global n    # 不要在子线程里随便修改全局变量
    n-=1
t_l = []
for i in range(100):
    t = Thread(target=func)
    t_l.append(t)
    t.start()
for t in t_l:t.join()
print(n)
```

- 守护线程一直等到所有非守护线程都结束之后才结束
- 除了守护主线程的代码外也会守护子线程

```python
import time
from threading import Thread
def son1():
    while True:
        time.sleep(0.5)
        print('in son1')
def son2():
    for i in range(5):
        time.sleep(1)
        print('in son2')
t =Thread(target=son1)
t.daemon = True
t.start()
Thread(target=son2).start()
time.sleep(3)
```

### 0.2.6 池

- 进程池
- 特点：开销大，进程池的任务个数限制了我们程序的并发个数。
- 池的概念：预先的开启固定个数的进程数，当任务来临的时候，直接提交给已经开好的进程，让这个进程去执行就可以了，节省了进程，线程的开启、关闭、切换都需要时间，并且减轻了操作系统跳读的负担。
- concurrent.futures
- submit(提交任务)  +  shutdown

```python
import os
import time
import random
from concurrent.futures import ProcessPoolExecutor
def func():
    print('start',os.getpid())
    time.sleep(random.randint(1,3))
    print('end',os.getpid())
if __name__ == '__main__':
    p = ProcessPoolExecutor(5)
    for i in range(10):
        p.submit(func)
    p.shutdown()
    print('main:',os.getpid())
    
```

- 任务的参数 + 返回值

```python
def func(i,name):
    print('start',os.getpid())
    time.sleep(random.randint(1,3))
    print('end', os.getpid())
    return '%s * %s'%(i,os.getpid())
if __name__ == '__main__':
    p = ProcessPoolExecutor(5)
    ret_l = []
    for i in range(10):
        ret = p.submit(func,i,'alex')
        ret_l.append(ret)
    for ret in ret_l:
        print('ret-->',ret.result())  # ret.result() 同步阻塞
    print('main',os.getpid())
```

- 线程池
  - 创建一个线程池
  - tp = ThreadPoolExcutor(池中线程/进程的个数)
  - 异步提交任务
  - ret = tp.submit(函数,参数1,参数2....)
  - 获取返回值
  - ret.result()
  - 在异步的执行完所有任务之后，主线程/主进程才开始执行代码
  - tp.shutdown()阻塞直到所有的任务都执行完毕
  - map方法
  - ret = tp.map(func,iterable)迭代获取iterable中的内容，作为func的参数，让子线程来执行对应的任务。
  - for i in ret:每一个都是任务的返回值
  - 回调函数
  - ret.add_done_callback(函数名)
  - 要在ret对应的任务执行完毕之后，直接执行add_done_callback绑定的函数中的内容，并且ret的结果会作为参数返回给绑定的函数
- 创建一个线程池

```python
from concurrent.futures import ThreadPoolExecutor
def func(i):
    print('start', os.getpid())
    time.sleep(random.randint(1,3))
    print('end', os.getpid())
    return '%s * %s'%(i,os.getpid())
tp = ThreadPoolExecutor(20)
ret_l = []
for i in range(10):
    ret = tp.submit(func,i)
    ret_l.append(ret)
tp.shutdown()
print('main')
for ret in ret_l:
    print('------>',ret.result())
```

- ret = map(需要在子线程执行的函数名，iterable)
  - 迭代ret，总是能得到所有的返回值

```python
from concurrent.futures import ThreadPoolExecutor
def func(i):
    print('start', os.getpid())
    time.sleep(random.randint(1,3))
    print('end', os.getpid())
    return '%s * %s'%(i,os.getpid())
tp = ThreadPoolExecutor(20)
ret = tp.map(func,range(20))
for i in ret:
    print(i)
ret_l = []
for i in range(10):
    ret = tp.submit(func,i)
    ret_l.append(ret)
tp.shutdown()
print('main')
```

- tp = ThreadPoolExecutor(cpu*5)
- obj = submit(需要在子线程执行的函数名，参数)
- 可以用obj.result()获取返回值，是一个阻塞方法
- 绑定回调函数 obj.add_done_callback(子线程执行完毕之后要执行的代码对应的函数)
- 回调函数
  - 执行完子线程任务之后直接调用对应的回调函数
  - 爬取网页 需要等待数据传输和网络上的响应高io的—子线程
  - 分析网页 没有io操作—这个操作没必要在子线程完成，交给回调函数
- tp.shutdown()

```python
from concurrent.futrues import ThreadPoolExecutor
import time
def son():
    print(123)
    time.sleep(3)
    return 123
def call_back(num):
	print(num)
    print(num.result())
t = ThreadPoolExecutor(20)
obj = t.submit(son)
print('main:',obj)
obj.add_done_callback(call_back)
```

- 回调函数add_done_callback(函数)

```python
import time 
from concurrent.futures import ThreadPoolExecutor
def son():
    print(123)
    time.sleep(1)
    return 123
def call_back(num):
    print(num.result())
t = ThreadPoolExecutor(20)
obj = t.submit(son)
obj.add_done_callback(call_back)
```



```python
import requests
from concurrent.futures import ThreadPoolExecutor
def get_page(url):
    res = requests.get(url)
    return {'url':url,'content':res.text}

def parserpage(ret):
    dic = ret.result()
    print(dic['url'])
tp = ThreadPoolExecutor(5)
url_lst = [
    'http://www.baidu.com',   # 3
    'http://www.cnblogs.com', # 1
    'http://www.douban.com',  # 1
    'http://www.tencent.com',
    'http://www.cnblogs.com/Eva-J/articles/8306047.html',
    'http://www.cnblogs.com/Eva-J/articles/7206498.html',
]
ret_l = []
for url in url_lst:
    ret = tp.submit(get_page,url)
    ret_l.append(ret)
    ret.add_done_callback(parserpage)
```

- 是单独开启线程还是池？
- 如果只是开启一个子线程做一件事情，就可以单独开线程
- 如果有大量的任务等待程序去执行，达到了一定并发数，开启线程池
- 根据你程序的io操作也可以判断使用池还是不用池
  - socket 大量的io阻塞  recv  recvfrom  socketserver 可以不用池
  - 爬虫的时候  可以根据获得信息的速度是否用池

### 0.2.7 协程

- 协程
  - 什么是协程：多个任务在一条线程上来回切换。
  - 在一条线程上最大限度的提高cpu的使用率，在一个任务中遇到io就切换到其他任务。
  - 特点：开销小，用户级别操作，由我们自己写的python代码来控制切换（只能感知从用户级别感知的io操作），不能利用多核，数据共享，数据安全。
  - 由操作系统切换，不可见
- 在cpython解释器下-协程和线程都不能利用多核
  - 由于多线程本身就不能利用多核
  - 所以即便是开启了多个线程也只能轮流在一个cpu上执行
  - 协程如果把所有的任务的io操作都规避掉，只剩下需要cpu的操作就意味着协程可以做到提高cpu利用率的效率
- 多线程和协程
  - 线程 切换需要操作系统，开销大，操作系统不可控，给操作系统的压力大
  - 协程  切换需要python代码，开销小，用户操作可控，完全不会增加操作系统的压力。
- 协程的切换方式：能够在一个线程下的多个任务之间来回切换，那么每一个任务都是一个协程
- 两种切换方式：
  - 原生python完成  yield  asyncio
  - C语言完成的python模块  greenlet   gevent
- 语法
  - await 阻塞  协程函数这里要切换出去，还能保证一会再切换回来
  - await 必须卸载async函数里，async函数是协程函数
  - loop 事件循环
  - 所有的协程的执行 调度 都离不开loop
- greenlet模块

```python
import time
from greenlet import greenlet
def eat():
    print('wusir is eating')
    time.sleep(0.5)
    g2.switch()
    print('wusir finished eat')

def sleep():
    print('小马哥 is sleeping')
    time.sleep(0.5)
    print('小马哥 finished sleep')
    g1.switch()

g1 = greenlet(eat)
g2 = greenlet(sleep)
g1.switch()
```

- gevent模块（gevent基于greenlet切换）
- 分辨gevent是否识别了我们写的代码中的io操作的方法:
  - 在patchall之前打印一下涉及到io操作的函数地址
  - 在patchall之后打印下涉及到io操作的函数地址
  - 如果两个地址一直说明gevent没有识别这个io，

```python
import time
print('-->',time.sleep)
import gevent
from gevent import monkey
monkey.patch_all()
def eat():
    print('wusir is eating')
    print('in eat: ',time.sleep)
    time.sleep(3)
    print('wusir finished eat')

def sleep():
    print('小马哥 is sleeping')
    time.sleep(1)
    print('小马哥 finished sleep')

g1 = gevent.spawn(eat)  # 创造一个协程任务
g2 = gevent.spawn(sleep)  # 创造一个协程任务
g1.join()   # 阻塞 直到g1任务完成为止
g2.join()   # 阻塞 直到g1任务完成为止
```

- 协程实现并发

```python
import time
import gevent
from gevent import monkey
monkey.patch_all()
def eat():
    print('wusir is eating')
    time.sleep(3)
    print('wusir finished eat')

def sleep():
    print('小马哥 is sleeping')
    time.sleep(1)
    print('小马哥 finished sleep')
#
g1 = gevent.spawn(eat)  # 创造一个协程任务
g3 = gevent.spawn(eat)  # 创造一个协程任务
g2 = gevent.spawn(sleep)  # 创造一个协程任务
g1.join()   # 阻塞 直到g1任务完成为止
g2.join()   # 阻塞 直到g1任务完成为止
gevent.joinall([g1,g2,g3])
g_l = []
for i in range(10):
    g = gevent.spawn(eat)
    g_l.append(g)
gevent.joinall(g_l)
```

- 协程返回值

```python
import time
import gevent
from gevent import monkey
monkey.patch_all()
def eat():
    print('wusir is eating')
    time.sleep(1)
    print('wusir finished eat')
    return 'wusir***'

def sleep():
    print('小马哥 is sleeping')
    time.sleep(1)
    print('小马哥 finished sleep')
    return '小马哥666'

g1 = gevent.spawn(eat)
g2 = gevent.spawn(sleep)
gevent.joinall([g1,g2])
print(g1.value)
print(g2.value)
```

- asyncio模块 （基于yield机制切换）
- async标识一个协程函数
- await 后跟着一个asyncio模块提供的io操作的函数
- loop 事件循环，负责在多个任务之间进程切换的最简单的函数操作

```python
#起一个任务
async def demo():#协程方法
    print('start')
    await asyncio.sleep(1)#阻塞
    print('end')
loop = asyncio.get_event_loop()#创建一个时间循环
loop.run_until_complete(demo())#把demo任务丢到事件循环中去执行
```

- 启动多个任务，并没有返回值

```python
async def demo():   # 协程方法
    print('start')
    await asyncio.sleep(1)  # 阻塞
    print('end')

loop = asyncio.get_event_loop()  # 创建一个事件循环
wait_obj = asyncio.wait([demo(),demo(),demo()])
loop.run_until_complete(wait_obj)
```

- 启动多个任务并且有返回值

```python
async def demo():   # 协程方法
    print('start')
    await asyncio.sleep(1)  # 阻塞
    print('end')
    return 123

loop = asyncio.get_event_loop()
t1 = loop.create_task(demo())
t2 = loop.create_task(demo())
tasks = [t1,t2]
wait_obj = asyncio.wait([t1,t2])
loop.run_until_complete(wait_obj)
for t in tasks:
    print(t.result())
```

- 谁先来先取谁的结果

```python
import asyncio
async def demo(i):   # 协程方法
    print('start')
    await asyncio.sleep(10-i)  # 阻塞
    print('end')
    return i,123

async def main():
    task_l = []
    for i in range(10):
        task = asyncio.ensure_future(demo(i))
        task_l.append(task)
    for ret in asyncio.as_completed(task_l):
        res = await ret
        print(res)

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
```

- 原生爬取网页

```python
import asyncio

async def get_url():
    reader,writer = await asyncio.open_connection('www.baidu.com',80)
    writer.write(b'GET / HTTP/1.1\r\nHOST:www.baidu.com\r\nConnection:close\r\n\r\n')
    all_lines = []
    async for line in reader:
        data = line.decode()
        all_lines.append(data)
    html = '\n'.join(all_lines)
    return html

async def main():
    tasks = []
    for url in range(20):
        tasks.append(asyncio.ensure_future(get_url()))
    for res in asyncio.as_completed(tasks):
        result = await res
        print(result)


if __name__ == '__main__':
    loop = asyncio.get_event_loop()
    loop.run_until_complete(main())  # 处理一个任务
```

线程：开销大 数据隔离  能利用多核 数据不安全 操作系统级别

线程：开销中 数据共享  才cpython解释器下不能利用多核 数据不安全 操作系统控制

协程：开销小 数据共享  不能利用多核 数据安全 用户控制

在哪些地方用到了线程和协程：

- 自己用线程、协程完成爬虫任务
- 但是后来有了比较丰富的爬虫框架
  
  - 了解到scrapy beautyful soup aiogttp爬虫框架
- web框架中的并发是如何实现的：
  - 传统框架：django 多线程
  - flask 优先选用协程，其次使用线程
  - socket server：多线程
  - 异步的框架：tornado，sanic底层都是协程
  
    

## 0.3 第十章 数据库（5）

问答题：

用什么数据库：MySQL，版本是什么：5.6  ，为什么是这个版本：解释5.6版本以上的优势，储存引擎：innodb；为什么是这个存储引擎：支持事务、支持外键、支持行级锁、能够更好的处理并发问题。

### 0.3.1 数据库

- 很多功能如果只是通过操作文件来改变数据是非常繁琐的
- 对于多台机器或者多个进程操作一份数据
  - 程序员自己解决并发问题比较麻烦
- 自己处理一些数据备份，容错的措施
- 相关语言
  - ddl 定义语言
    - 创建用户
      - create user 'name'@'ip'
    - 创建库
      - create database name
    - 创建表
      - create table name(字段名,数据类型（长度）,字段名 数据类型(长度))
  - dml 操作语言
    - 数据的
    - 增 insert into
    - 删 delete from
    - 改 update
    - 查 select
      - select user()；查看当前用户
      - select database();查看当前所在数据库
    - show
      - show database;查看当前的数据库有哪些
      - show tables;查看当前的库中有哪些表
    - desc 表名；查看表结构
    - use 库名；切换到这个库下
  - dcl 控制语言
    - 给用户授权
    - grant select on 库名.*  to  'user'@'ip地址/段' identified by ‘pwd'
    - grant select,insert
    - grant all

### 0.3.2 C/S架构的操作数据文件的一个管理软件

- 帮助我们解决并发问题
- 能够帮助我们用更简单更快的方式完成数据的增删改查
- 能够给我们提供一些容错、高可用机器
- 权限的认证

### 0.3.3 数据管理系统

- 专门用来管理数据文件，帮助用户更简洁的操作数据的软件DBMS
- 数据 data 
- 文件
- 文件夹 ---数据库database db
- 数据管理员 -----DBA

### 0.3.4 数据库管理系统

- 关系型数据库
  - sql server
  - Oracle  收费、比较严谨、安全性比较高（甲骨文）
    - 国企  事业单位
    - 银行  金融行业
  - MySQL  开源的
    - 小公司
    - 互联网公司
  - sqllite
- 非关系型数据库
  - Redis
  - MongoDB

### 0.3.5 MySQL的cs架构

- MySQL install 安装数据库服务
- net start mysql 启动数据库的server端
  - net stop mysql  停止server
- 客户端可以是python代码，也可是一个特殊的程序
  - MySQL.exe是一个客户端
  - MySQL -u用户名 -p密码
- MySQL中的用户和权限
  - 在安装数据库之后，有一个最高权限的root用户
  - MySQL 192.168.12.87 name/pwd
    - mysql -h192.168.12.87 -uroot -p123
- 我们的MySQL客户端不仅可以连接本地的数据库，也可以连接网络上的server端
- mysql>select user(); #查看当前用户是谁
- MySQL》set password = password('密码')；
- 数据库方法
  - database(),user(),now(),concat(),password()
- 创建用户
  - create user 'name'@'% '   表示网络可以通行的所有ip地址都可以使用这个用户名
  - create user 'name'@'192.168.12.% 'IDENTIFIED BY网段内可以访问
  - create user 'name'@'192.168.12.% '表示只有一个ip地址可以访问
  - mysql> -us21 -p123 -h192.168.12.87
- 查看文件夹
  - show databases；
- 创建文件夹
  - create database day37；
  - use 库名;#切换到数据库（文件夹）下
- 授权
  - grant all on day37.* to 's21'@'192.168.12.%';
  - flush privilegess; #刷新
  - 授权并创建用户
  - grant all on day37.* to 'alex'@'%' identified by '123';
  - grant select on 库名.* to '用户名'@'ip地址/段' identitified by '密码'
- 库 表  数据
  - 创建库、创建表  DDL数据库定义语言
  - 存数据，删除数据，修改数据，查看数据  DML数据库操纵语句
  - grant  revoke	 DCL控制权限 
- 库
  - create database 数据库名；  #创建库
  - show databases ;查看当前有多少个数据库
  - 切换到文件夹下  use 文件名  select database();查看当前所在的数据库
  - drop database  数据库名字  删库
- 表操作
  - 创建表
    - create table 表名字(id int,name char(4));
  - 删除表
    - drop table staudent;  #删表
  - 查看表结构
    - desc 表名；
  - 修改表
- 操作表中的数据
  - 数据增加
    - insert into 表名字 values （1，’alex')；
    - insert into 表名字 values （2，’haha')
  - 数据的查看
    - select * from 表名；
  - 修改数据
    - update 表 set 字段名=值 where 条件;
    - update student set name = 'yuan' where id = 2;
  - 删除数据
    - delete from 表名字； #整个表删除
    - delete from 表名字 where id=1；

### 0.3.6 表的储存方式

- 存储方式1：MyISAM 5.5以下默认存储方式
  - 存储的文件个数：表结构、表中的数据、索引
  - 支持表级锁
  - 不支持行级锁 不支持事物 不支持外键
- 存储方式2：InnoDB 5.6以上 默认存储方式
  - 存储的文件个数：表结构、表中的数据
  - 支持行级锁、支持表锁
  - 支持事物
  - 支持外键
- 存储方式3：MEMORY 内存
  - 存储的文件个数：表结构
  - 优势：增删改查都很快
  - 劣势：重启数据消失、容量有限
- 索引 - 数据库的目录
  - show variables like '%name%';
- 创建表
  - create table t1(id int,name char(4));
  - create table t2(id int,name char(4)) engine=myisam;
  - create table t3(id int,name char(4)) engine=memory;
- 查看表的结构
  - show create table 表名;能够看到和这张表相关的所有信息
  - desc 表名    只能查看表的字段的基础信息
  - describe 表名
- 整数 int
  - create table t4(id1 int(4),id2 int(11));
  - int 默认是有符号的
  - 他能表示的数字的范围不被宽度约束
  - 他只能约束数字的显示宽度
  - create table t5(id1 int unsigned,id2 int);
- 小数 float
  - create table t6(f1 float(5,2),d1 double(5,2));
  - create table t7(f1 float,d1 double);
  - create table t8(f1 decimal,d1 decimal(25,20));
- 类型
  - year  年
  - date   年月日
  - time    时分秒
  - datetime、timestamp 年月日时分秒

```python
create table t9(y year,d date,dt datetime NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP ts timestamp)
```

```python
mysql> create table t8 (dt datetime);
Query OK, 0 rows affected (0.01 sec)

mysql> insert into t8 values ('2018-9-26 12:20:10');
Query OK, 1 row affected (0.01 sec)

mysql> insert into t8 values ('2018/9/26 12+20+10');
Query OK, 1 row affected (0.00 sec)

mysql> insert into t8 values ('20180926122010');
Query OK, 1 row affected (0.00 sec)

mysql> insert into t8 values (20180926122010);
Query OK, 1 row affected (0.00 sec)

mysql> select * from t8;
+---------------------+
| dt                  |
+---------------------+
| 2018-09-26 12:20:10 |
| 2018-09-26 12:20:10 |
| 2018-09-26 12:20:10 |
| 2018-09-26 12:20:10 |
+---------------------+
rows in set (0.00 sec)

datetime示例
```

```python
mysql> create table t7 (y year);
Query OK, 0 rows affected (0.02 sec)

mysql> insert into t7 values (2018);
Query OK, 1 row affected (0.00 sec)

mysql> select * from t7;
+------+
| y    |
+------+
| 2018 |
+------+
row in set (0.00 sec)

year示例
```

```python
mysql> create table t6 (t1 timestamp);
Query OK, 0 rows affected (0.02 sec)

mysql> desc t6;
+-------+-----------+------+-----+-------------------+-----------------------------+
| Field | Type      | Null | Key | Default           | Extra                       |
+-------+-----------+------+-----+-------------------+-----------------------------+
| t1    | timestamp | NO   |     | CURRENT_TIMESTAMP | on update CURRENT_TIMESTAMP |
+-------+-----------+------+-----+-------------------+-----------------------------+
row in set (0.01 sec)

mysql> insert into t6 values (19700101080001);
Query OK, 1 row affected (0.00 sec)

mysql> select * from t6;
+---------------------+
| t1                  |
+---------------------+
| 1970-01-01 08:00:01 |
+---------------------+
row in set (0.00 sec)
# timestamp时间的下限是19700101080001
mysql> insert into t6 values (19700101080000);
ERROR 1292 (22007): Incorrect datetime value: '19700101080000' for column 't1' at row 1

mysql> insert into t6 values ('2038-01-19 11:14:07');
Query OK, 1 row affected (0.00 sec)
# timestamp时间的上限是2038-01-19 11:14:07
mysql> insert into t6 values ('2038-01-19 11:14:08');
ERROR 1292 (22007): Incorrect datetime value: '2038-01-19 11:14:08' for column 't1' at row 1
mysql> 

timestamp示例2
```

```python
mysql> create table t5 (id1 timestamp);
Query OK, 0 rows affected (0.02 sec)

mysql> desc t5;
+-------+-----------+------+-----+-------------------+-----------------------------+
| Field | Type      | Null | Key | Default           | Extra                       |
+-------+-----------+------+-----+-------------------+-----------------------------+
| id1   | timestamp | NO   |     | CURRENT_TIMESTAMP | on update CURRENT_TIMESTAMP |
+-------+-----------+------+-----+-------------------+-----------------------------+
row in set (0.00 sec)

# 插入数据null，会自动插入当前时间的时间
mysql> insert into t5 values (null);
Query OK, 1 row affected (0.00 sec)

mysql> select * from t5;
+---------------------+
| id1                 |
+---------------------+
| 2018-09-21 14:56:50 |
+---------------------+
row in set (0.00 sec)

#添加一列 默认值是'0000-00-00 00:00:00'
mysql> alter table t5 add id2 timestamp;
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> show create table t5 \G;
*************************** 1. row ***************************
       Table: t5
Create Table: CREATE TABLE `t5` (
  `id1` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  `id2` timestamp NOT NULL DEFAULT '0000-00-00 00:00:00'
) ENGINE=InnoDB DEFAULT CHARSET=utf8
row in set (0.00 sec)

ERROR: 
No query specified

# 手动修改新的列默认值为当前时间
mysql> alter table t5 modify id2 timestamp default current_timestamp;
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> show create table t5 \G;
*************************** 1. row ***************************
       Table: t5
Create Table: CREATE TABLE `t5` (
  `id1` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  `id2` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP
) ENGINE=InnoDB DEFAULT CHARSET=utf8
row in set (0.00 sec)

ERROR: 
No query specified

mysql> insert into t5 values (null,null);
Query OK, 1 row affected (0.01 sec)

mysql> select * from t5;
+---------------------+---------------------+
| id1                 | id2                 |
+---------------------+---------------------+
| 2018-09-21 14:56:50 | 0000-00-00 00:00:00 |
| 2018-09-21 14:59:31 | 2018-09-21 14:59:31 |
+---------------------+---------------------+
rows in set (0.00 sec)

timestamp示例
```

```python
mysql> create table t4 (d date,t time,dt datetime);
Query OK, 0 rows affected (0.02 sec)

mysql> desc t4;
+-------+----------+------+-----+---------+-------+
| Field | Type     | Null | Key | Default | Extra |
+-------+----------+------+-----+---------+-------+
| d     | date     | YES  |     | NULL    |       |
| t     | time     | YES  |     | NULL    |       |
| dt    | datetime | YES  |     | NULL    |       |
+-------+----------+------+-----+---------+-------+
rows in set (0.01 sec)

mysql> insert into t4 values (now(),now(),now());
Query OK, 1 row affected, 1 warning (0.01 sec)

mysql> select * from t4;
+------------+----------+---------------------+
| d          | t        | dt                  |
+------------+----------+---------------------+
| 2018-09-21 | 14:51:51 | 2018-09-21 14:51:51 |
+------------+----------+---------------------+
row in set (0.00 sec)

mysql> insert into t4 values (null,null,null);
Query OK, 1 row affected (0.01 sec)

mysql> select * from t4;
+------------+----------+---------------------+
| d          | t        | dt                  |
+------------+----------+---------------------+
| 2018-09-21 | 14:51:51 | 2018-09-21 14:51:51 |
| NULL       | NULL     | NULL                |
+------------+----------+---------------------+
rows in set (0.00 sec)

date/time/datetime示例
```

```python
# 创建表的三个字段分别为float，double和decimal参数表示一共显示5位，小数部分占2位
mysql> create table t2 (id1 float(5,2),id2 double(5,2),id3 decimal(5,2));
Query OK, 0 rows affected (0.02 sec)

# 向表中插入1.23，结果正常
mysql> insert into t2 values (1.23,1.23,1.23);
Query OK, 1 row affected (0.00 sec)

mysql> select * from t2;
+------+------+------+
| id1  | id2  | id3  |
+------+------+------+
| 1.23 | 1.23 | 1.23 |
+------+------+------+
row in set (0.00 sec)

# 向表中插入1.234，会发现4都被截断了
mysql> insert into t2 values (1.234,1.234,1.234);
Query OK, 1 row affected, 1 warning (0.00 sec)

mysql> select * from t2;
+------+------+------+
| id1  | id2  | id3  |
+------+------+------+
| 1.23 | 1.23 | 1.23 |
| 1.23 | 1.23 | 1.23 |
+------+------+------+
rows in set (0.00 sec)

# 向表中插入1.235发现数据虽然被截断，但是遵循了四舍五入的规则
mysql> insert into t2 values (1.235,1.235,1.235);
Query OK, 1 row affected, 1 warning (0.00 sec)

mysql> select * from t2;
+------+------+------+
| id1  | id2  | id3  |
+------+------+------+
| 1.23 | 1.23 | 1.23 |
| 1.23 | 1.23 | 1.23 |
| 1.24 | 1.24 | 1.24 |
+------+------+------+
rows in set (0.00 sec)

# 建新表去掉参数约束
mysql> create table t3 (id1 float,id2 double,id3 decimal);
Query OK, 0 rows affected (0.02 sec)

# 分别插入1.234
mysql> insert into t3 values (1.234,1.234,1.234);
Query OK, 1 row affected, 1 warning (0.00 sec)

# 发现decimal默认值是(10,0)的整数
mysql> select * from t3;
+-------+-------+------+
| id1   | id2   | id3  |
+-------+-------+------+
| 1.234 | 1.234 |    1 |
+-------+-------+------+
row in set (0.00 sec)

# 当对小数位没有约束的时候，输入超长的小数，会发现float和double的区别
mysql> insert into t3 values (1.2355555555555555555,1.2355555555555555555,1.2355555555555555555555);
Query OK, 1 row affected, 1 warning (0.00 sec)

mysql> select * from t3;
+---------+--------------------+------+
| id1     | id2                | id3  |
+---------+--------------------+------+
|   1.234 |              1.234 |    1 |
| 1.23556 | 1.2355555555555555 |    1 |
+---------+--------------------+------+
rows in set (0.00 sec)

小数示例
```

```python
# 创建表一个是默认宽度的int，一个是指定宽度的int(5)
mysql> create table t1 (id1 int,id2 int(5));
Query OK, 0 rows affected (0.02 sec)

# 像t1中插入数据1，1
mysql> insert into t1 values (1,1);
Query OK, 1 row affected (0.01 sec)

# 可以看出结果上并没有异常
mysql> select * from t1;
+------+------+
| id1  | id2  |
+------+------+
|    1 |    1 |
+------+------+
row in set (0.00 sec)

# 那么当我们插入了比宽度更大的值，会不会发生报错呢？
mysql> insert into t1 values (111111,111111);
Query OK, 1 row affected (0.00 sec)

# 答案是否定的，id2仍然显示了正确的数值，没有受到宽度限制的影响
mysql> select * from t1;
+------------+--------+
| id1        | id2    |
+------------+--------+
| 0000000001 |  00001 |
| 0000111111 | 111111 |
+------------+--------+
rows in set (0.00 sec)

# 修改id1字段 给字段添加一个unsigned表示无符号
mysql> alter table t1 modify id1 int unsigned;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc t1;
+-------+------------------+------+-----+---------+-------+
| Field | Type             | Null | Key | Default | Extra |
+-------+------------------+------+-----+---------+-------+
| id1   | int(10) unsigned | YES  |     | NULL    |       |
| id2   | int(5)           | YES  |     | NULL    |       |
+-------+------------------+------+-----+---------+-------+
rows in set (0.01 sec)

# 当给id1添加的数据大于214748364时，可以顺利插入
mysql> insert into t1 values (2147483648,2147483647);
Query OK, 1 row affected (0.00 sec)

# 当给id2添加的数据大于214748364时，会报错
mysql> insert into t1 values (2147483647,2147483648);
ERROR 1264 (22003): Out of range value for column 'id2' at row 1

int整数示例
```



- char(15) 定长的单位，存储快，占内存
- varchar(15) 变长的单位，省内存，存储慢
- 两种方式对比：
  - varchar:节省空间、存取效率相对低
  - char:浪费空间，存取效率相对高 长度变化校
- 手机号、身份证、用户、密码 char
- 评论、微博、说说、微信状态 varchar
- create table t11(name1 char(5),name2 varchar(5));
- ENUM和set  枚举类型
  - create table t12(name char(12),gender ENUM('male','female'),hobby set('抽烟','喝酒','烫头'))
  - insert into t12 values('alex','buxiang','抽烟,喝酒')；

### 0.3.7 约束

- unsigned  设置某一个数字无符号

- not null 某一个字段不能为空(严格模式会影响非空设置的效果)

  ```python
  create table t1(id int not null,name char(12) not null,age int)
  ```

- default  给某个字段设置默认值

```python
create table t2(id int not null,name char(12) not null,age int deffault 18,gender enum('male','female') not null default 'male');
```

- unique  设置某一个字段不能重复

```python
creat table t3(id int unique,username char(12) unique,age int deffault 18,gender enum('male','female') not null default 'male');
```

```python
#联合唯一
unique(字段1,字段2)
```

- auto_increment  设置某一个int类型的字段 自动增加

```python
#设置自增字段必须是数字且必须是唯一的,自带非空效果
create table t5(id int unique auto_increment,username char(10),password char(18))
desc t5;
insert into t5(username,password) values('alex','pwd')
```

- primary key  设置某一个字段非空且不能重复

```python
create table t5(id int not null unique,name char(12) not unique)#指定的第一个非空且唯一的字段会被定义成一个主键，主键只能有一个。
desc t5;
```

```python
#联合主键
primary key(字段1,字段2)
```

- foreign key   外键

```python
#涉及到两张表
#id age gender salary hir_date postname postid post_comment post_mail post_phone
#员工表
create table staff(id int primary key auto_increment,age int,psot_id int primary key,foreign key(psot_id）refereces post(pid))
#部门表
create talbe psot(pid,postname char(10) not null unique primary_key,comment varchar(255),phone_num char(11))
#级联操作：on update cascade on delete cascade           
```

```python
#create table class(cid int primary key auto_increment,caption char(18));
insert into class(caption) values('三年二班'),('一年三班'),('三年一班');
#create table student(sid int primary key auto_increment,sname char(18),gender enum('男','女'),class_id int not null,foreign key(class_id) references class(cid));
insert into student(sname,gender,class_id) values('钢蛋','女',1),('铁蛋','女',1),('炮弹','男',2);
#create table teacher(tid int primary key auto_increment,tname char(18));
insert into teacher(tname) values('藏獒'),('黑背'),('金茂');
#create table course(cid int primary key auto_increment,cname varchar(20),teacher_id int not null,foreign key(teacher_id) references teacher(tid));
insert into course(cname,teacher_id) values('生物',1),('体育',1),('物理',2);
#create table score(sid int primary key auto_increment,student_id int not null,foreign key(student_id) references student(sid),corse_id int not null,foreign key(corse_id) references course(cid));

insert into score(student_id,corse_id,number) values(1,1,60),(1,2,59),(2,2,100);
```



```python
create table staff2(id int primary key auto_increment,age int,gender enum('male','female'),salary float(8,2),hire_date date,post_id int,foreign key(post_id) references post(pid) on update cascade on delete set null)
```

### 0.3.8 表操作、表关系、数据操作

- 表操作
  - alter table 表名 add 添加字段
  - alter table 表名 drop 删除字段
  - alter table 表名 modify 修改意见存在的字段的类型 宽度 约束
  - alter table 表名 change 修改意见存在的字段的类型 宽度 约束 和字段名字
  - alter table 表名 add 字段名 数据类型（宽度） 约束 first/after  name
  - alter table 表名 drop 字段名
  - alter table 表名 modify name varchar(12) not null
  - alter table 表名 change name new_name varchr(12) not null
  - 调换顺序 id name age
  - alter table 表名 modify age int not null after id;
  - alter table 表名 modify age int not null first;
- 表关系（两张表中的数据之间的关系）
  - 多对一 foreign key 永远是在多的那张表中设置外键
  - 一对一  foreign key +unique 后出现的后一张表中的数据作为外键
    - 客户关系表：手机号 招生老师 上次联系的时间 备注信息
    - 学生表：姓名 入学日期 缴费日期 结业
  - 多对多 产生三张表，把两个关联关系的字段作为第三张表的外键
    - 书-出版社        /          出版社/书
- 数据操作
  - 增加insert
    - insert into 表名 values（值）#所有的在这个表中的字段都需要按照顺序被填写在这里
    - insert into 表名（字段名，字段名...） values（值...）#所有在字典位置填写了名字的字段和后面的值必须是一一对应
    - insert into 表名（字段名，字段名...） values（值...），（值...）#所有在字段位置填写了名字的字段和后面的值必须是一一对应
  - value 单数一次写入一行数据      values 复数一次写入多行数据
    - insert into t1 value(1,'alex',83)
    - insert into t1 values(1,'alex',83),(2,'wusir',74)
    - insert into t1(name,age)  values('alex',83),('wusir',74)
    - insert into t1(name,age)  value('alex',83)
  - 第一个角度
    - insert into 表名 values(值...)
    - insert into 表名 values(值...),(值...),(值...)
  - 第二个角度
    - 是把这一行所有的内容都写入
    - insert into 表名 values(值...)
    - 指定字段写入
    - insert into 表名(字段1，字段2) values(值1，值2)
  - 删除 delete
    - delete from 表 where 条件
  - 更新 update
    - update 表 set 字段=新的值 where 条件
  - 查询 select语句
    - select * from 表
    - select 字段，字段... from 表
    - select distinct 字段，字段.. from 表 #按照查出来的字段去重
    - select 字段*5 from 表 #查出来的字段统一处理
    - select 字段 as 新名字，字段 as 新名字 from 表 #按照查出来的字段更名
    - select 字段 新名字 from 表 #更名

### 0.3.9 单表查

- where 语句
  - 比较运算 > < = >= <= != <>
  - 范围筛选
    - 多选一 字段名 in (值1,值2,值3)
    - select * from employee where salary in (20000,30000,3000)
    - 在一个模糊的范围里  between 10000 and 20000
      - 在一个数值区间  1w-2w之间的所有人的名字
      - elect emp_name from employee where salary between 10000 and 20000;
      - 字符串的模糊查询 like
      - 通配符 % 匹配任意长度的任意内容
      - 通配符 _ 匹配一个字符长度的任意内容
      - 正则匹配 regexp  更加细粒度的匹配的时候
      - select * from 表 where 字段 regexp 正则表达式
      - select * from employee where emp_name regexp '^j[a-z]{5}'
  - 逻辑运算-条件拼接 与and  或or 非not
    - select * from employee where salary not in (18000,17000)
  - 身份运算--关于null is null    is not null
    - 查看岗位描述不为null的员工信息
    - select * from employee where post_comment is not null;
  - 查看岗位是teacher且名字是jin开头的员工姓名、年薪
    - select emp_name,salary*12 from employee where post='teacher' and emp_name like 'jin%'
    - select emp_name,salary*12 from employee where post='teacher' and emp_name regexp '^jin.*'

### 0.3.10 分组聚合

- 分组  group by
  - select * from 表 group by name;
  - 会把在group by后面的这个字段，也就是post字段中的每一个不同的项都保留下来，并且把值是这一项的所有行归为一组
- 聚合  把很多行的一个字段进行一些统计，最终得到一个结果
  - count(字段)  统计这个字段有多少项
  - sum(字段)  统计这个字段对应的数值的和
  - avg(字段)  统计这个字段对应的数值的平均数
  - min(字段)   最小
  - max(字段)  最大
- 分组聚合
  - 求各个部门的人数
  - select count(*) from employee group by 部门;
  - 求个部门最小的
  - select post,min(age) from employee group by post
- having 条件 #过滤 组
  - 部门人数大于3
  - select 部门 from 表 group by post having count(*) > 3
  - 平均薪资大于10000的部门
  - select post from 表 group by post having avg(salary) > 10000
  - select * from employee having age>18
- order by 
  - order by 某一个字段 asc;默认是升序asc 从小到大
  - order by 某一个字段 desc;指定降序排列desc 从大到小
  - order by 第一个字段 asc,第二个字段 desc;
    - 指定先根据第一个字段升序排列，在第一个字段相同的情况下，再根据第二个字段排列
- limit 
  - 提取前n个  limit n = limit 0,n
  - 分页   limit m,n 从m+1开始取n个
  - limit n offset m == limit m,n 从m+1开始取n个
- select distinct 需要显示的列 from 表 where 条件 group by 分组 having 过滤组条件 order by 排序 limit 前n条
- pymysql模块

```python
import pymysql
#
conn = pymysql.connect(host='127.0.0.1', user='root', password="123",
                 database='day40')
cur = conn.cursor()   # 数据库操作符 游标
cur.execute('insert into employee(emp_name,sex,age,hire_date) '
            'values ("郭凯丰","male",40,20190808)')
cur.execute('delete from employee where id = 18')
conn.commit()
conn.close()


conn = pymysql.connect(host='127.0.0.1', user='root', password="123",
                 database='day40')
cur = conn.cursor(pymysql.cursors.DictCursor)   # 数据库操作符 游标
cur.execute('select * from employee '
            'where id > 10')
ret = cur.fetchone()
print(ret['emp_name'])
ret = cur.fetchmany(5)
ret = cur.fetchall()
print(ret)
conn.close()
```

### 0.3.11 多表查询

-  select * from emp,department;把两张表连在一起查

  - 内连接 inner join 两张表条件不匹配的项不会出现在结果中

    - select * from emp inner join department on emp.dep_id = department.id;

  - 外连接

    - 左外连接 left join 永远显示全量的左表中的数据
    - select * from emp left join department on emp.dep_id = department.id;
    - 右外连接 right join永远显示全量的右表中的数据
    - select * from emp right join department on emp.dep_id = department.id;
    - 全外连接 union会去掉相同的记录，union不会
    - select * from emp left join department on emp.dep_id = department.id union select * from emp right join department on emp.dep_id = department.id;
  - select employee.id,employee.name,sex,age,department.name from employee left join department on employee.dep_id = department.id
      union
  - select employee.id,employee.name,sex,age,department.name from employee right join department on employee.dep_id = department.id
      ;
  
  - 子查询
  
  - 找技术部门的所有人的姓名，先找到部门表技术部门的部门id
    
    - select id from department where name = '技术';
  - 再找到emp表中部门id=200
    - select name from emp where dep_id = (select id from department where name = '技术');
  
    
  
    - 先找到技术部门和销售部门所有人的姓名，找到技术部门和销售哦部门的部门id。
  - select id from department where name = '技术' or name='销售';
    
    - 找到emp表中部门id=200或者202的人名
  - select name from emp where dep_id in (select id from department where name = '技术' or name='销售');
    
  - select emp.name from emp inner join department on emp.dep_id = department.id where department.name in ('技术','销售');
    
  - 连接的语法 优先使用连表查询，因为连表查询的效率高
  
    - select 字段 from 表1 xxx join 表2 on 表1.字段 = 表2.字段;
    - 找技术部门的所有人的姓名
    - select * from emp inner join department on emp.dep_id = department.id;
    - select * from emp inner join department on emp.dep_id = department.id where department.name = '技术'
    - select emp.name from emp inner join department d on emp.dep_id = d.id where d.name = '技术'
  - 找出年龄大于25岁的员工以及员工所在的部门名称
    
    - select emp.name,d.name from emp inner join department as d on emp.dep_id = d.id where age>25;
  - 根据age的升序顺序来连表查询emp和department
    
  - select * from emp inner join department as d on emp.dep_id = d.id order by age;
    
  - 相关练习
  
    - 查询平均年龄在25岁以上的部门名
    - 部门名 department表
    - select name from department where id in (select dep_id from emp froup by dep_id having avg(age)>25);
    - 员工表
    - select dep_id,avg(age) from emp group by dep_id;
    - select dep_id from emp group by dep_id having avg(age)>25;
    - 查看不足1人的部门名（子查询得到的是所有人的部门id）
    - 查emp表中有哪些id
    - select dep_id from emp group by dep_id;
    - 再看department表中
    - select * from department where id not in (???)
    - select * from department where id not in (select dep_id from emp group by dep_id);
    - 查询大于所有人平均年龄的员工名与年龄
    - select * from emp where age>(select avg(age) from emp);
    - 查询大于部门内平均年龄的员工名、年龄
    - select dep_id,avg(age) from emp group by dep_id;
    - select * from emp inner join (select dep_id,avg(age) avg_age from emp group by dep_id) as d on emp.dep_id = d.dep_id where emp.age > d.avg_age;

### 0.3.12 索引

#### 0.3.12.1 索引原理

- 什么是索引--目录
  - 就是建立起的一个在存储表阶段
  - 就有一个存储的结构能在查询的时候加锁
- 索引的重要性
  - 读写比例：10:1 所以读（查询）的速度至关重要
- 索引的原理
  - block 磁盘预读原理
    - 比如for line in f ，一个block块4096个字节
  - 度硬盘的io操作的时间非常的长，比cpu的执行指令的时间长很多，所以要尽量的减少io次数才是读写数据的主要解决的问题。
  - 数据库的存储方式
    - 新的数据结构--树
    - 平衡树  balance tree --b树
    - 在b树的基础上进行了改良---b+树
      - 1.分支节点和根节点都不在存储实际的数据了，让分支和根节点能存储更多的索引的信息，就降低了树的高度，所有的书籍数据都存储在叶子节点中，
      - 2.在叶子节点之间假如了双向的链式结构
        - 方便在查询中的范围条件
    - MySQL当中所有的b+树索引的高度都基本控制在3成
      - 1.io操作的次数非常稳定
      - 2.有利于通过范围查询
    - 什么会影响索引的效率---树的高度
      - 1.对那一块创建索引，选择尽量短的列做索引
      - 2.对区分高度的列建索引，重复率超过了10%就不合适创建索引
- 聚集索引和辅助索引
  - 在innodb中 聚集索引和辅助索引并存的
    - 聚集索引 - 主键 更快
      - 数据直接存储在树结构的叶子节点
    - 辅助索引- 除了主键之外所有的索引都是辅助索引稍慢
      - 数据不直接存储的树中
  - 在myisam中 只有辅助索引，没有聚集索引
- 索引的种类
  - primary key 主键 聚集索引 约束的作用：非空+唯一
    - 联合主键
  - unique 自带索引 辅助索引 约束的作用:唯一
    - 联合唯一
  - index 辅助索引 没有约束作用
    - 联合索引
- 看下如何创建索引、创建索引之后的变化
  - create index 索引名 on 表(字段)；
  - drop index 索引名 on 表名；
- 索引是如何发挥作用的
  - select * from 表 where id = xxxx
    - 在id字段没有索引的时候效率低
    - 在id字段有索引之后效率高

#### 0.3.12.2 正确使用索引

- 以email为条件查询
  - 不添加索引的时候肯定慢
  - 查询的字段不是索引字段也慢
- 以id为条件的时候
  - 不加索引速度慢
  - 加了索引速度快
- 索引不生效的原因
  - 要查询的数据的范围大
  - '> < >= >= !='
  - between and 
    - select * from 表order by age limit 0,5;
    - select * from 表 where id between 100000 and 200000；
  - like
    - 结果的范围大 索引不生效
    - 如果 abc% 索引生效，%abd索引不生效
  - 如果一列内容的区分度不高，索引也不生效
    - 如name列
  - 索引列不能再条件中参与计算
    - select * from s1 where id*10 = 100000;索引不生效
  - 对两列内容进行条件查询
    - and and条件两端的内容，优先选择一个由索引的，并且树形结构更好的来进行查询。
      - 两个条件都成列才能完成where条件，先完成范围校的缩小后面条件的压力
      - select * from s1 where id=1000 and email='xxxxx'；
    - or or条件的，不会进行优化，只是根据条件从左到右依次筛选
      - 条件中带有or的想要命中索引，这些条件中所有的列都是索引列
      - select * from s1 where id=1000 or email='xxxxx';
- 联合索引  #create index ind_mix on s1(id,name,email)
  - select * from s1 where id=10000 and email='xxxxx'; 可以命中
  - 在联合索引中如果使用了or条件索引就不能生效
    - select * from s1 where id=100 or email='xxxx'; 不能命中
  - 在左前缀原则：在联合索引中，条件必须含有在创建索引的时候第一个索引列
    - select * from s1 where id=1000;可以命中索引
    - select * from s1 where email='xxxx';不能命中索引
    - (a,b,c,d) #以a开头的所有组合都可命中
  - 在整个条件中，从开始出现模糊匹配的那一刻，索引就失效了
    - select * from s1 where id>1000 and email='xxxxx';
    - select * from s1 where id=100000 and email like 'eva%';
- 什么时候用联合索引
  - 只对a对abc条件进行索引而不会对b，对c进行单例的索引
- 单列索引
  - 选择一个区分度高的列监理索引，条件中的列不要参与计算，条件的范围尽量小，使用and作为条件的连接符
- 使用or来连接多个条件
  - 在满上上述条件的基础上
  - 对or相关的所有列分别创建索引
- 覆盖索引
  - 如果我们使用索引作为条件查询，查询完毕之后不需要回表查，覆盖索引
  - explain select id from s1 where id=1000;
  - explain select count(id)  from s1 where id>10000;
- 合并索引
  - 对两个字段分别创建索引，由于sql的条件让两个索引同时生效了，那么这个时候这两个索引就成为了合并索引
- 执行计划：如果你想在执行sql之前就知道sql语句的执行情况，那么可以使用执行计划
  - 情况1(3000000条数据)：
    - sql 20s
    - explain sql -->并不会真正的执行sql，而是会给你列出一个执行计划
  - 情况2(20条数据---》3000000):
    - explain sql
- 原理和概念
  - b树
  - b+树
  - 聚集索引----innodb
  - 辅助索引----innodb  myisam
- sql索引的创建(单个、联合)、删除
- 索引的命中：范围，条件的字段是否参与计算(不能用函数)，列的区分度（长度），条件and/or，联合索引的最左前缀问题
- 一些名词：
  - 覆盖索引
  - 合并索引
- explain执行计划
- 建表、使用sql语句的时候注意的
  - char 代替 varchar
  - 连表代替子查询
  - 创建表的时候 固定长度的字段放在前面

#### 0.3.12.3 数据备份和事务

- mysqldump -uroot -p123  day40 > D:\code\s21day41\day40.sql
- mysqldump -uroot -p123 --databases new_db > D:\code\s21day41\db.sql
- begin; 开启事务
- select * from emp where id = 1 for update;  # 查询id值，for update添加行锁；
- update emp set salary=10000 where id = 1; # 完成更新
- commit; # 提交事务

```python
# create table userinfo(
# id int primary key auto_increment,
# name char(12) unique not null,
# password char(18) not null
# )
#
# insert into userinfo(name,password) values('alex','alex3714')

```

```python
# 输入用户
# 输入密码
#
# 用户名和密码到数据库里查询数据
# 如果能查到数据 说明用户名和密码正确
# 如果查不到，说明用户名和密码不对
# username = input('user >>>')
# password = input('passwd >>>')
# sql = "select * from userinfo where name = '%s' and password = '%s'"%(username,password)
# print(sql)
# -- 注释掉--之后的sql语句
# select * from userinfo where name = 'alex' ;-- and password = '792164987034';
# select * from userinfo where name = 219879 or 1=1 ;-- and password = 792164987034;
# select * from userinfo where name = '219879' or 1=1 ;-- and password = '792164987034';

```

```python
import pymysql

conn = pymysql.connect(host = '127.0.0.1',user = 'root',
                       password = '123',database='day41')
cur = conn.cursor()
username = input('user >>>')
password = input('passwd >>>')
sql = "select * from userinfo where name = %s and password = %s"
cur.execute(sql,(username,password))
print(cur.fetchone())
cur.close()
conn.close()
```




## 0.4 第十三章  面试题

1.关于def func(a,b=[])有什么陷阱？

- 看代码写结果

```python
def func(a,b=[]):
	b.append(a)
    return b
m1 = func(1)
m2 = func(2,[11,22])
m3 = func(3)
print(m1,m2,m3)#[1,3]  [11,22,2] [1,3]
```

- 看代码写结果

```python
def func(a,b=[]):
    b.append(a)
    print(b)
func(1)
func(2,[11,22,33])
func(3)
#[1,] [11,22,33,2]  [1,3]
    
```

- 关于生成器：取一次就没有了，惰性运算，不取不执行。

```python
m=(i for i in range(4))
for i in [1,10]:
    g=(i+j for j in m)
print(list(g))
```

```python
ret = filter(lambda x:x%3==0.range(0))
print(len(list(ret)))
print(len(list(ret)))
```

```python
def demo():
    for i in range(4):
        yield i
g = demo()
g1 = (i for i in g)
g2 = (i for i in g1)
print(list(g))
print(list(g1))
print(list(g2))
```

```python
def add(n,i):
    return n+i
def test():
    for i in range(4):
        yield i
g=test() #[0,1,2,3]
for n in [1,8,5]:#[5,6,7,8][10,11,12,13][15,16,17,18]
    g=(add(n,i) for i in g)
print(list(g))
```

```python
g1 = filter(lambda n:n%2==0,range(10))
g2 = map(lambda n:n*2,range(3))
for i in g1:
    for j in g2:
        print(i*j)#备注：生成器只能取一次，g2在第一次已被取完
```

```python
def multipliers():
    return(lambda x:i*x for i in range(4))
print([m2] for m in multipliers())#i在生成中一直未取，所以以最终3.
```



