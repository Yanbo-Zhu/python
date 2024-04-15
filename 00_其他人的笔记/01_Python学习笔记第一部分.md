Python学习笔记

## 0.1 第一章 计算机基础

```
# 新式类和经典类
    # py2 继承object就是新式类
    #     默认是经典类
    # py3 都是新式类，默认继承object
    # 新式类
        # 继承object
        # 支持super
        # 多继承 广度优先C3算法
        # mro方法
    # 经典类
        # py2中不继承object
        # 没有super语法
        # 多继承 深度优先
        # 没有mro方法
```

### 0.1.1 硬件

计算机基本的硬件由：CPU / 内存 / 主板 / 硬盘 / 网卡  / 显卡 等组成，只有硬件但硬件之间无法进行交流和通信。

### 0.1.2 操作系统

操作系统用于协同或控制硬件之间进行工作，常见的操作系统有那些:

- windows
- linux
  - centos  【公司线上一般用】【图形化界面差】
  - ubuntu 【个人开发（图形化比较好）】
  - redhat   【企业级开发】
- mac

### 0.1.3 解释器或编译器

编程语言的开发者写的一个工具，将用户写的代码转换成010101交给操作系统去执行。

#### 0.1.3.1 解释和编译型语言

解释型语言就类似于： 实时翻译，代表：Python / PHP / Ruby / Perl

编译型语言类似于：说完之后，整体再进行翻译，代表：C / C++ / Java / Go ...

### 0.1.4 软件（应用程序）

软件又称为应用程序，就是我们在电脑上使用的工具，类似于：记事本 / 图片查看 / 游戏

### 0.1.5 进制

对于计算机而言无论是文件存储 / 网络传输输入本质上都是：二进制（010101010101），如：电脑上存储视频/图片/文件都是二进制； QQ/微信聊天发送的表情/文字/语言/视频 也全部都是二进制。

进制：

- 2进制，计算机内部。
- 8进制
- 10进制，人来进行使用一般情况下计算机可以获取10进制，然后再内部会自动转换成二进制并操作。
- 16进制，一般用于表示二进制（用更短的内容表示更多的数据），一版是：\x 开头。

| 二进制 | 八进制 | 十进制 | 十六进制 |
| ------ | ------ | ------ | -------- |
| 0      | 0      | 0      | 0        |
| 1      | 1      | 1      | 1        |
| 10     | 2      | 2      | 2        |
| 11     | 3      | 3      | 3        |
| 100    | 4      | 4      | 4        |
| 101    | 5      | 5      | 5        |
| 110    | 6      | 6      | 6        |
| 111    | 7      | 7      | 7        |
| 1000   | 10     | 8      | 8        |
| 1001   | 11     | 9      | 9        |
| 1010   | 12     | 10     | A        |
| 1011   | 13     | 11     | B        |
| 1100   | 14     | 12     | C        |
| 1101   | 15     | 13     | D        |
| 1110   | 16     | 14     | E        |
| 1111   | 17     | 15     | F        |
| 10000  | 20     | 16     | 21       |



## 0.2 第二章 Python入门

### 0.2.1 环境的安装

- 解释器：py2 / py3 （环境变量）
- 开发工具：pycharm
- 环境变量的作用：方便在命令行（终端）执行可执行程序，将可执行程序所在的目录添加到环境变量，那么以后无需再输入路径。

### 0.2.2 编码

#### 0.2.2.1 编码基础

最小的单元是位（bit），接着是字节（Byte），一个字节=8位，英语表示是1 Byte=8 bits 。机器语言的单位Byte。1 KB=1024 Byte; 1 MB=1024 KB; 1 GB=1024 MB ; 1TB=1024 GB。

- ascii 8位表示一个东西 主要用于显示现代英语和其他西欧语言

- unicode  32位表示一个东西

- utf-8  给Unicode压缩，用尽量少的位数表示一个东西。是Unicode的其中一个使用方式

- gbk 是GB2312的扩展(K)，GBK1.0收录了21886个符号，它分为汉字区和图形符号区，汉字区包括21003个字符

- gb2312 第一个汉字“啊”字为例，它的区号16，位号01，则区位码是1601，在大多数计算机程序中，高字节和低字节分别加0xA0得到程序的汉字处理编码0xB0A1。计算公式是：0xB0=0xA0+16, 0xA1=0xA0+1。

  （8位=1个字节）
  
  [https://baike.baidu.com/item/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BC%96%E7%A0%81/9127611?fr=aladdin](https://baike.baidu.com/item/计算机编码/9127611?fr=aladdin)

#### 0.2.2.2 python编码相关

```python
1.编码
python2默认编码方式ASCII码（不能识别中文，要在文件头部加上  #-*- encoding：utf-8 -*-  指定编码方式）

python3默认编码方式unicode（可识别中文）
 2.print
python2中加不加括号都可以打印

python3中必须加括号
3.input
python2 raw_input()
python3 input()
 4.range()
python2 range()/xrange()
python3 range()
循环：
- py2: xrange 执行循环时输出
- py3: range 执行时输出
5.类
python3中都是新式类
python2.7中经典类和新式类混合
新式类中使用广度优先，经典类中使用深度优先
python3可以使用super
python2不能使用super
6.int
py2：int有限定长度，超过限定自动变成long型 
py3：没有long都是int
长度：
- py2中有：int/long
- py3中有：int 
7.整除
py2和py3中整除是不一样
模块和包
字典

- keys
  - py2:列表
  - py3:迭代器，可以循环单不可以索引
- values
  - py2:列表
  - py3:迭代器，可以循环单不可以索引
- values
  - py2:列表
  - py3:迭代器，可以循环单不可以索引
- map/filter
  - py2:返回列表
  - py3:返回迭代器，可以循环单不可以索引

如果想要修改默认编码，则可以使用：

python2中默认不支持中文需添加以下
#！/user/bin/env python 在Linux中指定解释器的路径
# -*- coding:utf-8 -*- 
运行：需要解释器、路径。
注意：对于操作文件时，要按照：以什么编写写入，就要用什么编码去打开。
```

### 0.2.3 变量

问：为什么要有变量？

为某个值创建一个“外号”，以后在使用时候通过此外号就可以直接调用。

变量名的要求：

- 变量名只能包含：子母/数字/下划线
- 数字不能开头
- 不能是Python的关键字【'and', ‘as’, ‘assert’, ‘break’, ‘class’, ‘continue’, ‘def’, ‘del’, ‘elif’, ‘else’, ‘except’, ‘exec’,‘finally’, ‘for’, ‘from’, ‘global’, ‘if’, ‘import’, ‘in’, ‘is’, ‘lambda’, ‘not’, ‘or’, ‘pass’, ‘print’, ‘raise’, ‘return’, ‘try’, ‘while’,‘with’, ‘yield’]

变量名的建议：

- 见名知意：name = 'alex'  age = 20
- 用下划线连接：name_len = len(name)
- NameLen = len(name) (驼峰式命名)

### 0.2.4 运算符

```python
v = 1 or 2 
v = 0 or 2 
v = 1 and 2 
v = 0 and 2 
```



## 0.3 第三章 数据类型

### 0.3.1 整型（int）

- 将字符串转换为数字

  ```python
  a = '55'
  num = int(a)
  print(num)
  ```

#### 0.3.1.1 整型的长度

py2中有：int/long

py3中有：int 

#### 0.3.1.2 整除

py2和py3中整除是不一样。

### 0.3.2 布尔（bool）

布尔值就是用于表示真假。True和False。

其他类型转换成布尔值：

- str
- ...

对于：None /  "" / 0 /[]/()/{}/set().... -> false

### 0.3.3 字符串（str）

字符串是写代码中最常见的，python内存中的字符串是按照：unicode 编码存储。对于字符串是不可变。

字符串自己有很多方法，如：

1. 大写： upper/capitalize()/isupper()

   ```
   v = 'ALEX'
   v1 = v.upper()
   print(v1)
   v2 = v.isupper() # 判断是否全部是大写
   print(v2)
   ```

2. 小写：lower/islower()

   ```
   v = 'alex'
   v1 = v.lower()
   print(v1)
   v2 = v.islower() # 判断是否全部是小写
   print(v2)
   ############ 了解即可
   v = 'ß'
   # 将字符串变小写（更牛逼）
   v1 = v.casefold()
   print(v1) # ss
   v2 = v.lower()
   print(v2)
   ```

3. 判断是否是数字： isdecimal/isdigit

   ```
   v = '1'
   # v = '二'
   # v = '②'
   v1 = v.isdigit()  # '1'-> True; '二'-> False; '②' --> True
   v2 = v.isdecimal() # '1'-> True; '二'-> False; '②' --> False
   v3 = v.isnumeric() # '1'-> True; '二'-> True; '②' --> True
   print(v1,v2,v3)
   # 以后推荐用 isdecimal 判断是否是 10进制的数。
   
   # ############## 应用 ##############
   
   v = ['alex','eric','tony']
   
   for i in v:
       print(i)
   
   num = input('请输入序号：')
   if num.isdecimal():
       num = int(num)
       print(v[num])
   else:
       print('你输入的不是数字')
   ```

4. 去空白+\t+\n + 指定字符串.strip()/=.lstrip()/.rstrip()

   ```python
   
   v1 = "alex "
   print(v1.strip())
   
   v2 = "alex\t"
   print(v2.strip())
   
   v3 = "alex\n"
   print(v3.strip())
   
   v1 = "alexa"
   print(v1.strip('al'))
   ```

5. 替换 replace

   ```python
   a = 'asdasd'
   b = a.replace('d','a')
   print(b)
   ```

6. 判断字符串开头 / 结尾.startswith()/.endswith()

   ```python
   a = 'abdh'
   flag1 = a.startswith('a')
   flag2 = a.endswith('h')
   print(flag1,flag2) #True True
   ```

7. 编码，把字符串转换成二进制.encode()  .decode()

   ```python
   name = '哈'
   v1 = name.encode('utf-8')
   v2 = name.encode('gbk')
   print(v1,v2)
   ```

8. 字符串进行格式化.format()

   ```python
   msg = "我是%s,年龄%s" %('alex',19,)
   print(msg)
   
   msg = "我是%(n1)s,年龄%(n2)s" % {'n1': 'alex', 'n2': 123, }
   print(msg)
   ```

   ```python
   # v1 = "我是{0},年龄{1}".format('alex',19)
   v1 = "我是{0},年龄{1}".format(*('alex',19,))
   print(v1)
   
   # v2 = "我是{name},年龄{age}".format(name='alex',age=18)
   v2 = "我是{name},年龄{age}".format(**{'name':'alex','age':18})
   print(v2)
   ```

   

9. '内容'.join()对元素之间插入，元素为字符串

   ```python
   name = 'lhijoieoij'
   result = '_'.join(name)
   print(result)
   ```

10. .split('分割内容')对字符串进行分割，分割后定义一个新列表。 (split/lsplit/rsplit)

    ```python
    name = 'lhijoieoij'
    result = '_'.join(name)
    print(result)
    ```

11. 其他【可选】x.ljust(8,'a')/x.ljust(8,'a')

    ```
    a = 'asdas'
    b = a.ljust(10,'0')
    print(b)
    ```

    

### 0.3.4 列表

- .append()，在列表的最后追加一个元素

  ```python
  content = [1,2,3,5]
  content.append(56)
  print(content)
  ```

- .insert(位置，'内容')，在列表制定位置添加指定内容

  ```python
  content = [1,5,5,'kjoj']
  content.insert(2,'haha')
  print(content)
  ```

- .remove('内容')，删除指定元素

  ```python
  content = ['哈','658','hah']
  content.remove('hah')
  print(content)
  ```

- .pop()通过下标删除元素（若没有填写则删除最后一个内容），还可以对删除内容定义新变量

  ```python
  content = ['hioh','oiajdoi','hsauhd']
  b = content.pop(1)
  print(b,content)
  ```

- .clear(),清空

  ```python
  content = ['haisjdio','asd','dsad']
  content.clear()
  print(content)
  ```

- .extend(),将要添加的内容拆分成单个元素后添加到列表

  ```python
  content = ['haisjdio','asd','dsad']
  b = 'sjdaj'
  content.extend(b)
  print(content)
  ```

- reverse(),将列表进行反转

  ```python
  content = ['haisjdio','asd','dsad']
  content.reverse()
  print(content)
  ```

- .sort(),排序 默认从小到大(只能是一种类型，字符串或整型)

  ```python
  li = [1,6,8,6]
  li.sort()
  #li.sort(reverse=False) 与不填相同为默认从小到大
  #li.sort(reverse=True)
  print(li)
  ```

  

### 0.3.5 公共功能

- len
- 索引
- 切片
- 步长
- for循环

### 0.3.6 嵌套

- if嵌套
- while 循环

### 0.3.7 3.10字典（dict）可变类型

- 有序字典

  ```python
  from collections import OrderedDict
  
  info = OrderedDict()
  info['k1'] = 123
  info['k2'] = 456
  
  print(info.keys())
  print(info.values())
  print(info.items())
  ```

  - 字典的另一种创建方式

  ```python
  # from collections import OrderedDict
  # odic = OrderedDict([('a', 1), ('b', 2), ('c', 3)])
  # print(odic)
  # for k in odic:
  #     print(k,odic[k])
  ```

  

- 特有方法

  - .keys(),获取字典中的所有键

    ```python
    info = {'name':'hei','age':18,'gender':'男'}
    for item in info.keys():
        print(item)
    ```

  - .values(),获取字典中所有的值

    ```python
    info = {'name':'hei','age':18,'gender':'男'}
    for item in info.values():
        print(item)
    ```

  - .items(),获取字典中所有的键值对（需两个变量对应）

    ```python
    info = {'name': 'hei', 'age': 18, 'gender': '男'}
    for item in info.items():
        v1,v2 = item
        print(v1,v2)
        print(item)
    ```

  - .get()根据“键”获取“值”(若没有返回None，不会报错)

    ```python
    info = {'name': 'hei', 'age': 18, 'gender': '男'}
    value = info.get('name') 
    print(value) #若“键”不存在则返回None
    ```

  - .pop(),(删除的键值对可以赋予一个新的变量与之对应)

    ```python
    info = {'name': 'hei', 'age': 18, 'gender': '男'}
    result = info.pop('name')
    print(result,info)
    ```

  - .update() 不存在则添加，存在则更新

    ```python
    info = {'name': 'hei', 'age': 18, 'gender': '男'}
    info1 = {'name': 'bai', 'sha': 18}
    info.update(info1)
    print(info)
    ```

### 0.3.8 3.11集合(set)(可变类型)

- 特有方法

  - .add('内容') 添加指定内容

    ```python
    v = {1, 2, 3, 'abc', '计算机'}
    v.add("Python")
    print(v)
    ```

  - .discard('内容')，删除指定内容，无则返回None

    ```python
    v = {1,2,3,5,'k','hggh'}
    val = v.discard('m')
    print(v,val)
    ```

  - .update()批量添加（列表、元组、集合都可以，若为字典只将键更新到集合内）

    ```python
    v = {1, 2, 3, 'abc', '计算机'}
    b = [4, 5, 6]
    v.update(b)
    print(v)
    ```

  - .intersection() 交集

    ```python
    v1 = {1, 2, 3, 'abc', '计算机'}
    v2 = {2, 3, 4, 'ABC', '计算机'}
    v3 = v1.intersection(v2)
    print(v3)
    ```

  - .union()并集

    ```python
    v1 = {1, 2, 3, 'abc', '计算机'}
    v2 = {2, 3, 4, 'ABC', '计算机'}
    v3 = v1.union(v2)
    print(v3)
    ```

  - .difference()前者对后者的差集（前有后无）

    ```python
    v1 = {1, 2, 3, 'abc', '计算机'}
    v2 = {2, 3, 4, 'ABC', '计算机'}
    v3 = v1.difference(v2)  # v1对v2的差集
    # v3 = v2.difference(v1)  # v2对v1的差集
    print(v3)
    ```

  - .symmertric_difference()对称差集

    ```python
    v1 = {1, 2, 3, 'abc', '计算机'}
    v2 = {2, 3, 4, 'ABC', '计算机'}
    v3 = v1.symmetric_difference(v2)
    print(v3)
    ```

    

## 0.4 第四章 文件操作

### 0.4.1 文件基本操作

```python
obj = open('路径',mode='模式',encoding='编码')
obj.write()
obj.read()
obj.close()
```

### 0.4.2 打开模式

- r / w / a
- r+ / w+ / a+
- rb / wb / ab
- r+b / w+b / a+b 

### 0.4.3 操作

- read() , 全部读到内存

- read(1) 

  - 1表示一个字符

    ```python
    obj = open('a.txt',mode='r',encoding='utf-8')
    data = obj.read(1) # 1个字符
    obj.close()
    print(data)
    ```

  - 1表示一个字节

    ```python
    obj = open('a.txt',mode='rb')
    data = obj.read(3) # 1个字节
    obj.close()
    ```

- write(字符串)

  ```python
  obj = open('a.txt',mode='w',encoding='utf-8')
  obj.write('中午你')
  obj.close()
  ```

- write(二进制)

  ```python
  obj = open('a.txt',mode='wb')
  
  # obj.write('中午你'.encode('utf-8'))
  v = '中午你'.encode('utf-8')
  obj.write(v)
  
  obj.close()
  ```

- seek(光标字节位置)，无论模式是否带b，都是按照字节进行处理。

  ```
  obj = open('a.txt',mode='r',encoding='utf-8')
  obj.seek(3) # 跳转到指定字节位置
  data = obj.read()
  obj.close()
  print(data)
  
  obj = open('a.txt',mode='rb')
  obj.seek(3) # 跳转到指定字节位置
  data = obj.read()
  obj.close()
  
  print(data)
  ```
  
- tell(), 获取光标当前所在的字节位置

  ```
  obj = open('a.txt',mode='rb')
  # obj.seek(3) # 跳转到指定字节位置
  obj.read()
  data = obj.tell()
  print(data)
  obj.close()
  ```

- flush，强制将内存中的数据写入到硬盘

  ```
  v = open('a.txt',mode='a',encoding='utf-8')
  while True:
      val = input('请输入：')
      v.write(val)
      v.flush()
  
  v.close()
  ```



### 0.4.4 关闭文件

文艺青年

```python
v = open('a.txt',mode='a',encoding='utf-8')

v.close()
```

二逼

```python
with open('a.txt',mode='a',encoding='utf-8') as v:
    data = v.read()
	# 缩进中的代码执行完毕后，自动关闭文件
```



### 0.4.5 文件内容的修改

```python
with open('a.txt',mode='r',encoding='utf-8') as f1:
    data = f1.read()
new_data = data.replace('飞洒','666')

with open('a.txt',mode='w',encoding='utf-8') as f1:
    data = f1.write(new_data)
```

大文件修改

```
f1 = open('a.txt',mode='r',encoding='utf-8')
f2 = open('b.txt',mode='w',encoding='utf-8')

for line in f1:
    new_line = line.replace('阿斯','死啊')
    f2.write(new_line)
f1.close()
f2.close()
```

```
with open('a.txt',mode='r',encoding='utf-8') as f1, open('c.txt',mode='w',encoding='utf-8') as f2:
    for line in f1:
        new_line = line.replace('阿斯', '死啊')
        f2.write(new_line)
```

### 0.4.6 4.6三元运算（三目运算）

```python
v =  前面  if 条件 else 后面 

if 条件：
	v = '前面'
else:
    v = '后面'
```

```python
# 让用户输入值，如果值是整数，则转换成整数，否则赋值为None

data = input('>>>')
value =  int(data) if data.isdecimal() else None 
```

注意：先做出来，再考虑如何简化。

## 0.5 第五章 函数

### 0.5.1 函数

函数以前：面向过程编程，[可读性查、可重用性差]

函数式编程：增加代码的可读性和重用性。

- a = 1 b = 2 ==> a,b = b,a

```python
#面向过程编程
user_input = input('请输入角色：')

if user_input == '管理员':
    import smtplib
    from email.mime.text import MIMEText
    from email.utils import formataddr

    msg = MIMEText('管理员，我想演男一号，你想怎么着都行。', 'plain', 'utf-8')
    msg['From'] = formataddr(["李邵奇", '15776556369@163.com'])
    msg['To'] = formataddr(["管理员", '344522251@qq.com'])
    msg['Subject'] = "情爱的导演"

    server = smtplib.SMTP("smtp.163.com", 25)
    server.login("15776556369@163.com", "qq1105400511")
    server.sendmail('15776556369@163.com', ['管理员', ], msg.as_string())
    server.quit()
elif user_input == '业务员':
    import smtplib
    from email.mime.text import MIMEText
    from email.utils import formataddr

    msg = MIMEText('业务员，我想演男一号，你想怎么着都行。', 'plain', 'utf-8')
    msg['From'] = formataddr(["李邵奇", '15776556369@163.com'])
    msg['To'] = formataddr(["业务员", '业务员'])
    msg['Subject'] = "情爱的导演"

    server = smtplib.SMTP("smtp.163.com", 25)
    server.login("15776556369@163.com", "qq1105400511")
    server.sendmail('15776556369@163.com', ['业务员', ], msg.as_string())
    server.quit()
elif user_input == '老板':
    import smtplib
    from email.mime.text import MIMEText
    from email.utils import formataddr

    msg = MIMEText('老板，我想演男一号，你想怎么着都行。', 'plain', 'utf-8')
    msg['From'] = formataddr(["李邵奇", '15776556369@163.com'])
    msg['To'] = formataddr(["老板", '老板邮箱'])
    msg['Subject'] = "情爱的导演"

    server = smtplib.SMTP("smtp.163.com", 25)
    server.login("15776556369@163.com", "qq1105400511")
    server.sendmail('15776556369@163.com', ['老板邮箱', ], msg.as_string())
    server.quit()
```

```python
#函数式编程
def send_email():
	import smtplib
    from email.mime.text import MIMEText
    from email.utils import formataddr

    msg = MIMEText('老板，我想演男一号，你想怎么着都行。', 'plain', 'utf-8')
    msg['From'] = formataddr(["李邵奇", '15776556369@163.com'])
    msg['To'] = formataddr(["老板", '老板邮箱'])
    msg['Subject'] = "情爱的导演"

    server = smtplib.SMTP("smtp.163.com", 25)
    server.login("15776556369@163.com", "qq1105400511")
    server.sendmail('15776556369@163.com', ['老板邮箱', ], msg.as_string())
    server.quit()


user_input = input('请输入角色：')

if user_input == '管理员':
    send_email()
elif user_input == '业务员':
    send_email()
elif user_input == '老板':
    send_email()

```

对于函数编程：

- 本质：将N行代码拿到别处并给他起个名字，以后通过名字就可以找到这段代码并执行。
- 场景
  - 代码重复执行。
  - 代码量特别多超过一屏，可以选择通过函数进行代码的分割。

### 0.5.2 函数的基本结构

```python
# 函数的定义
def 函数名():
    # 函数内容
    pass

# 函数的执行
函数名()
```

```python
def get_list_first_data():
    v = [11,22,33,44]
    print(v[0])


get_list_first_data()

# 注意：函数如果不被调用，则内部代码永远不会被执行。
```

```python
# 假如：管理员/业务员/老板用的是同一个邮箱。
def send_email():
	print('发送邮件成功，假设有10含代码')


user_input = input('请输入角色：')

if user_input == '管理员':
    send_email()
elif user_input == '业务员':
    send_email()
elif user_input == '老板':
    send_email()
```

5.2.1函数的嵌套

```python
def func():
    name = 'oldboy'
    def inner():
        print(name)
    name = 'alex'
    inner()
	print(name)
func()
```

5.2.2 函数名当做变量使用

```python
def func():
    print(123)
    
v1 = func 

func()
v1（）
```

```python
def func():
    print(123)
    
func_list = [func, func, func]
# func_list[0]()
# func_list[1]()
# func_list[2]()
for item in func_list:
    v = item()
    print(v)
```

```python
def func():
    print(123)

def bar():
    print(666)

info = {'k1': func, 'k2': bar}

info['k1']() #等价于func（）  
info['k2']() #等价于bar（）  
```

```python
def func():
    return 123

func_list1 = [func,func,func]
func_list2 = [func(),func(),func()]

print(func_list1)
print(func_list2)

info = {
    'k1':func,
    'k2':func(),
}

print(info)
```

5.2.3 函数可以当做参数传递

```python
def func(arg):
    print(arg)
    
func(1)
func([1,2,3,4])

def show():
    return 999
func(show)
```

```python
def func(arg):
    v1 = arg()
    print(v1)
    
def show():
    print(666)
    
func(show)
```

```python
def func(arg):
    v1 = arg()
    print(v1)
    
def show():
    print(666)
    
result = func(show)
print(result)
```

面试题

```python
def func():
    print('花费查询')
def bar():
    print('语音沟通')
def base():
    print('xxx')
def show():
    print('xxx')
def test():
    print('xxx')
info = {'f1': func, 'f2': bar,'f3':base,'f4':show,'f5':test}
choice = input('请选择要选择功能：')
function_name = info.get(choice)
if function_name:
    function_name()
else:
    print('输入错误')
```

### 0.5.3 5.3函数中高级

补充：对于函数的默认值慎用可变类型（坑）。

```python
#如果要给value设置默认是空列表
#不推荐（坑）
def func(data,value=[])
	pass	
#推荐
def func(data,value=None)
	if not value:
        value = []
```

```python
def func(data,value=[])
	value.append(data)
    return value
v1 = func(1)#先打印v1时此时为[1,]，
v2 = func(2,[11,22])#[11,22,2]
v3 = func(3)#[1,3]
#此处打印时v1 v3 都为[1,3]
```





#### 0.5.3.1 5.3.1函数可做返回值

```python
def func():
    print(123)
def bar():
    return func
v = bar() 
v()
```

```python
name = 'oldboy'
def func():
    print(name)
    
def bar():
    return func

v = bar()

v()
```

```python
def bar():
    def inner():
        print(123)
    return inner
v = bar()
v()
```

```python
name = 'oldboy'
def bar():
    name = 'alex'
    def inner():
        print(name)
    return inner
v = bar()
v()
```

```python
name = 'oldboy'
def bar(name):
    def inner():
        print(name)
    return inner
v1 = bar('alex') # { name=alex, inner }  # 闭包，为函数创建一块区域（内部变量供自己使用），为他以后执行提供数据。
v2 = bar('eric') # { name=eric, inner }
v1()
v2()
```

练习题

```python
# 第一题
name = 'alex'
def base():
    print(name)

def func():
 	name = 'eric'
    base()

func() # {name=alex, }
    

# 第二题
name = 'alex'

def func():
 	name = 'eric'
    def base():
    	print(name)
    base()
func() # eric 

# 第三题
name = 'alex'

def func():
 	name = 'eric'
    def base():
    	print(name)
    return base 
base = func()
base() # eric
```

注意：函数在何时被谁创建？

面试题

```python
info = []

def func():
    print(item)
    
for item in range(10):
    info.append(func)

info[0]()
```

```python
info = []

def func(i):
    def inner():
        print(i)
	return inner

for item in range(10):
    info.append(func(item))

info[0]()
info[1]()
info[4]()
```

#### 0.5.3.2 5.3.2闭包

- 闭包的概念：为函数创建一块区域并为其维护自己的数据，以后执行时方便调用。【应用场景：装饰器/SQLAlchemy源码】

```python
def func(name):
    def inner():
        print(name)
	return inner 

v1 = func('alex')
v1() # alex
v2 = func('eric')
v2() #eric
```

#### 0.5.3.3 5.3.3高阶函数

- 把函数当做参数传递
- 把函数当作返回值

注意：对函数进行赋值、函数执行的流程分析（函数到底是谁创建的？）

### 0.5.4 参数

- 基本参数知识
  - 任意个数
  - 任意类型
  - 调用或执行函数时，传参：位置>关键字参数（必须位置参数在前关键字参数在后）
  - 参数传参分为：位置传参和关键字传参
  - 定义函数：
    - def func(a)
    - def func(a,b=None),对于默认值，如果是可变类型，有坑》》》》》
    - def func(*args,**kwargs)

```python
def func(a1,a2,a3):
    print(a1,a2,a3)
    
func(1,"asdf",True)
```

形式参数和实际参数

```python
def get_list_first_data(aaa): # aaa叫形式参数(形参)
    v = [11,22,33,44]
    print(v[aaa])


get_list_first_data(1) # 2/2/1调用函数时传递叫：实际参数（实参）
get_list_first_data(2)
get_list_first_data(3)
get_list_first_data(0)
```

```python
# 假如：管理员/业务员/老板用的是同一个邮箱。
"""
def send_email(to):
	import smtplib
    from email.mime.text import MIMEText
    from email.utils import formataddr

    msg = MIMEText('导演，我想演男一号，你想怎么着都行。', 'plain', 'utf-8')
    msg['From'] = formataddr(["李邵奇", '15776556369@163.com'])
    msg['To'] = formataddr(["导演", to])
    msg['Subject'] = "情爱的导演"

    server = smtplib.SMTP("smtp.163.com", 25)
    server.login("15776556369@163.com", "qq1105400511")
    server.sendmail('15776556369@163.com', [to, ], msg.as_string())
    server.quit()
"""
def send_email(to):
    template = "要给%s发送邮件" %(to,)
    print(template)
 


user_input = input('请输入角色：')

if user_input == '管理员':
    send_email('xxxx@qq.com')
elif user_input == '业务员':
    send_email('xxxxo@qq.com')
elif user_input == '老板':
    send_email('xoxox@qq.com')
```

- 位置传参（调用函数并传入函数）【执行】

```python
def func(a1,a2):
    print(a1,a2)
    
func(1,3)
```

- 关键字参数【执行】

```python
def func(a1, a2):
    print(a1, a2)

func(a2=99,a1=2)

# 关键字传参数和位置传参可以混合使用（位置传入的参数 > 关键字参数在后 = 总参数个数）
def func1(a1, a2, a3):
    print(a1, a2, a3)

# func(1, 2, a3=9)
# func(1, a2=2, a3=9)
# func(a1=1, a2=2, a3=9)
# func(a1=1, 2,3) # 错误
```

- 默认参数【定义】

```python
def func(a1,a2,a3=9,a4=10):
    print(a1,a2,a3,a4)

func(11,22)
func(11,22,10)
func(11,22,10,100)
func(11,22,10,a4=100)
func(11,22,a3=10,a4=100)
func(11,a2=22,a3=10,a4=100)
func(a1=11,a2=22,a3=10,a4=100)
```

- 万能参数（打散）

  - *args

    - 可以接受任意个数的位置参数，并将参数转换成元组。

      - 调用函数无*

      ```python
      def func(*args):
          print(args)
      
      func(1,2,3,4)
      ```

      - 调用函数有*

      ```python
      def func(*args):
          print(args)
      
      func(*(1,2,3,4))
      func(*[1,2,3,4])#将*后所有元素逐个调出后形成新的元组
      ```

  - 只能用位置传参

    ```python
    def func(*args):
        print(args)
    
    # func(1)
    # func(1,2)
    func(1,2) # args=(1, 2)
    func((11,22,33,44,55)) # args=((11,22,33,44,55),)
    func(*(11,22,33,44,55)) # args=(11,22,33,44,55)
    ```

- **kwargs

  - 可以接受任意个数的关键字参数，并将参数转换成字典。

    - 调用函数无**

    ```python
    def func(**kwargs):
        print(kwargs)
    func(k1=1,k2='alex') #{'k1': 1, 'k2': 'alex'}
    ```

    ```python
    def func(**kwargs)
    	print(kwargs)
    print(**{'k1':'v2','k2':'v2'})#{'k1'='v2','k2'='v2'}
    ```

- 综合应用：无敌 + 无敌=》真无敌

  ```python
  def func(*args,**kwargs):
      print(args,kwargs)
  
  # func(1,2,3,4,5,k1=2,k5=9,k19=999)
  func(*[1,2,3],k1=2,k5=9,k19=999)
  func(*[1,2,3],**{'k1':1,'k2':3})
  func(111,222,*[1,2,3],k11='alex',**{'k1':1,'k2':3})
  ```

- 参数的相关重点：

  - 定义函数

  ```python
  def func1(a1,a2):
      pass 
  
  def func2(a1,a2=None):
      pass 
  
  def func3(*args,**kwargs):
      pass 
  
  ```

  - 调用函数

  位置参数》关键字参数

### 0.5.5 作用域

- python文件：全局作用域

- 函数：局部作用域

  ```python
  a = 1
  def s1():
      x1 = 666
      print(x1)
      print(a)
      print(b)
  
  b = 2
  print(a)
  s1()
  a = 88888
  def s2():
      print(a,b)
      s1()
  
  s2()
  ```

- 本作用域中无变量对应赋值，只能依次向上一级中寻找与之对应的值，上一级的变量无法用下一级的变量进行赋值。（global/nonlocal可以强制赋值）global执行到根域，nonlocal执行到上一级。

  ```python
  name = 'oldboy'
  def func():
      name = 'alex' # 在自己作用域再创建一个这样的值。
      print(name)
  func()
  print(name)
  
  
  
  # #####################
  name = [1,2,43]
  def func():
      name.append(999)
      print(name)
  func()
  print(name)
  
  # ###################### 如果非要对全局的变量进行赋值
  # 示例一
  name = ["老男孩",'alex']
  def func():
      global name
      name = '我'
  func()
  print(name)
  # 示例一
  name = "老男孩"
  def func():
      name = 'alex'
      def inner():
          global name
          name = 999
      inner()
      print(name)
  func()
  print(name)
  
  
  name = "老男孩"
  def func():
      name = 'alex'
      def inner():
          global name
          name = 999
      inner()
      print(name)
  func()
  print(name)
  
  # ############################## nonlocal
  name = "老男孩"
  def func():
      name = 'alex'
      def inner():
          nonlocal name # 找到上一级的name
          name = 999
      inner()
      print(name)
  func()
  print(name)
  ```

  

- 作用域小结：

  - 一个函数是一个作用域

  ```python
  def func():
      x = 9
      print(x)
  func()
  ```

  - 作用域中查找数据规则：优先在自己的作用域找数据，若本作用域中没有则一次向上一级作用域中查找数据，全局无则报错。

```python
x = 10 
def func():
    x = 9
    print(x)
func()
```

作用域练习题

```python
# x = 10
# def func():
#     x = 9
#     print(x)
#     def x1():
#         x = 999
#         print(x)
#
# func()#9



# x = 10
# def func():
#     x = 9
#     print(x)
#     def x1():
#         x = 999
#         print(x)
#     x1()
#
# func()#9 999


# x = 10
# def func():
#     x = 9
#     print(x)
#     def x1():
#         x = 999
#         print(x)
#     print(x)
#     x1()
# func()#9 9 999

# x = 10
# def func():
#     x = 8
#     print(x)
#     def x1():
#         x = 999
#         print(x)
#     x1()
#     print(x)
# func()    #8 999 8


# x = 10
# def func():
#     x = 8
#     print(x)
#     def x1():
#         print(x)
#     x1()
#     print(x)
# func() #8 8 8



# x = 10
# def func():
#     x = 8
#     print(x)
#     def x1():
#         print(x)
#     x = 9
#     x1()
#     x = 10
#     print(x)
# func()#8 9 10

#
# x = 10
# def func():
#     x = 8
#     print(x)
#     def x1():
#         print(x)
#     x1()
#     x = 9
#     x1()
#     x = 10
#     print(x)
# func() #8 8 9 10
```



练习题

```python
# 1. 请写一个函数，函数计算列表 info = [11,22,33,44,55] 中所有元素的和。

def get_sum():
    info = [11,22,33,44,55]
    data = 0
    for item in info:
        data += item
    print(data)

get_sum()

# 2. 请写一个函数，函数计算列表中所有元素的和。

def get_list_sum(a1):
   	data = 0
    for item in a1:
        data += item
   	print(data)
    
get_list_sum([11,22,33])
get_list_sum([99,77,66])
v1 = [8712,123,123]
get_list_sum(v1)

# 3. 请写一个函数，函数将两个列表拼接起来。
def join_list(a1,a2):
    result = []
    result.extend(a1)
    result.extend(a2)
    print(result)
    
join_list([11,22,33],[55,66,77]

# 4. 计算一个列表的长度
def my_len(arg):
	count = 0
	for item in arg:
          count += 1
	print(count)

v = [11,22,33]
my_len(v)
len(v)

# 5. 发邮件的示例
          
def send_email(role,to):
    template = "要给%s%s发送邮件" %(role,to,)
    print(template)
 

user_input = input('请输入角色：')

if user_input == '管理员':
    send_email('管理员','xxxx@qq.com')
elif user_input == '业务员':
    send_email('业务员','xxxxo@qq.com')
elif user_input == '老板':
    send_email('老板','xoxox@qq.com')
```

### 0.5.6 返回值

返回值若不指定，则默认返回：None

```python
def func(arg):
    # ....
    return 9 # 返回值为9 默认：return None

val = func('adsfadsf')
```

```python
# 1. 让用户输入一段字符串，计算字符串中有多少A字符的个数。有多少个就在文件a.txt中写多少个“李邵奇”。

def get_char_count(data):
    sum_counter = 0
    for i in data:
        if i == 'A':
            sum_counter += 1
            
	return sum_counter

def write_file(line):
    if len(line) == 0:
        return False  # 函数执行过程中，一旦遇到return，则停止函数的执行。
    with open('a.txt',mode='w',encoding='utf-8') as f:
        f.write(line)
	return True 


content = input('请输入:')
counter = get_char_count(content)
write_data = "李邵奇" * counter 
status = write_file(write_data)
if status:
    print('写入成功')
else:
    print('写入失败')
```

f分析函数执行的内存

```python
def func(name):
    def inner():
        print(name)
        return 123
    return inner 

v1 = func('alex')
v2 = func('eric')

v1()
v2()
```

闭包

```python
#不是闭包
def func(name):
    def inner():
        return 123
    return inner
#是闭包：封装值+内层函数需要使用
def func2(name):
    def inner():
        print(name)
        return 123
    return inner

        
```

以上总结

```python
# 情况1
def f1():
    pass 
f1()

# 情况2
def f2(a1):
    pass 
f2(123)

# 情况3
def f3():
    return 1 
v1 = f3()

# 情况4
def f4(a1,a2):
    # ... 
    return 999
v2 = f4(1,7)
```

练习题

```python
# 1. 写函数，计算一个列表中有多少个数字，打印： 列表中有%s个数字。
#    提示：type('x') == int 判断是否是数字。
"""
# 方式一：
def get_list_counter1(data_list):
    count = 0
    for item in data_list:
        if type(item) == int:
            count += 1
	msg = "列表中有%s个数字" %(count,)
    print(msg)
    
get_list_counter1([1,22,3,'alex',8])

# 方式二：
def get_list_counter2(data_list):
    count = 0
    for item in data_list:
        if type(item) == int:
            count += 1
	return count
    
v = get_list_counter1([1,22,3,'alex',8])
msg = "列表中有%s个数字" %(v,)
print(msg)
"""

# 2. 写函数，计算一个列表中偶数索引位置的数据构造成另外一个列表，并返回。
"""
# 方式一：
def get_data_list1(arg):
    v = arg[::2]
    return v

data = get_data_list1([11,22,33,44,55,66])

# 方式二：
def get_data_list2(arg):
    v = []
    for i in range(0,len(arg)):
    	if i % 2 == 0:
    		v.append(arg[i])
   	return v

data = get_data_list2([11,22,33,44,55,66])

"""

# 3. 读取文件，将文件的内容构造成指定格式的数据，并返回。
"""
a.log文件
    alex|123|18
    eric|uiuf|19
    ...
目标结构：
a.  ["alex|123|18","eric|uiuf|19"] 并返回。
b. [['alex','123','18'],['eric','uiuf','19']]
c. [
	{'name':'alex','pwd':'123','age':'18'},
	{'name':'eric','pwd':'uiuf','age':'19'},
]
"""
```

### 0.5.7 全局变量必须全部大写

```python
USER_LIST = [1,2,3]
def func():
    name = 'alex'
    USER_LIST.append(12)
    USER_list.append(name)
func()
print(USER_LIST)
```

### 0.5.8 lambda表达式

```python
#三元运算，为了解决简单的if else的情况，如：
if a == b:
    a = 135
else:
    a = 0
a 135 if a ==b else 0
# lambda表达式，为了解决简单函数情况，如：
def func(a1,a2):
    return a1 + 100
func = lambda a1,a2: a1+100
```

```python
func1 = lambda : 100
func2 = lambda x1: x1*10
func3 = lambda *args,**kwargs: len(args)+len(kwargs)
DATA = 100
func4 = lambda a1: a1 +DATA
v = func4(1)
print(v)
DATA = 100
def func():
    DATA = 666
    func4 = lambda a1: a1 +DATA
    v = func4(1)
    print(v)
func()
func5 = lambda n1,n2: n1 if n1 > n2 else n2
v = func(111,6)
print(v)
```

练习题

```python
#练习题1
USER_LIST = []
def func(x):
    v = USER_LIST.append(x)
    return v  #None
result = func('alex')
print(result)
#练习题2
def func0(x):
    v = x.strip()
    return v 

result = func0(' alex ')
print(result)  #alex
#练习题3
USER_LIST = []
func1 = lambda x: USER_LIST.append(x)

v1 = func1('alex')
print(v1) #None
print(USER_LIST) #['alex']
#练习题4
func1 = lambda x: x.split('l')

v1 = func1('alex')
print(v1) #['a','ex']
#练习题5
func_list = [lambda x:x.strip(), lambda y:y+199,lambda x,y:x+y]

v1 = func_list[0]('alex ')
print(v1) #alex

v2 = func_list[1](100)
print(v2) #299

v3 = func_list[2](1,2)
print(v3) #3
```

### 0.5.9 内置函数

- 自定义函数

#### 0.5.9.1 5.9.1内置函数分类

- 其他

  - len
  - open
  - range
  - id
  - type

- 输入输出

  - print
  - input

- 强制转换

  - dict()
  - list()
  - tuple()
  - int()
  - str()
  - bool()
  - set()

- 数学相关

  - abs,绝对值

  ```python
  v = abs(-2)
  print(v)
  ```

  - float,转换成浮点型（小数）

  ```python
  v = 55
  v1 = float(v)
  print(v1)
  ```

  - max,min找到最大/小值

  ```python
  v = [52,69,32,58]
  result = max(v)
  result1 = min(v)
  print(result,result1)
  ```

  - sum,求和

  ```python
  v = [23,65,89,74]
  result = sum(v)
  print(result)
  ```

  - divmod,两数相除的商和余数

  ```python
  a,b =divmod(335,53)
  print(a,b)
  ```

  ```python
  #练习题 通过分页对数据进行显示
  要求：每页显示n条数据
  让用户输入要查看的页面
  USER_LIST = []
  for i in range(1,999):
      temp = {'name':"name%s" %i,'email':'110%s'%i}
      USER_LIST.append(temp)
  total_count = len(USER_LIST)
  per_page_count = 10
  max_page_num,a = divmod(total_count,per_page_count)
  if a != 0
  	max_page_num += 1
   pager = int(input('请输入要查看第几页：'))
  if not 0 < pager <= max_page_num:
      print('输入不合法，请输入1-%s'%max_page_num)
  else:
      start = (pager-1)*per_page_count
      end = pager*per_page_count
      data = USER_LIST[start：end]
      for item in data:
          print(item)
  ```

- 进制转换相关

  - bin，将十进制转换成二进制

  ```python
  num = 13
  v1 = bin(num)
  print(v1)
  ```

  - oct,将十进制转换成八进制

  ```python
  num = 8
  v1 = oct(num)
  print(v1)
  ```

  - int 将其他进制转换成十进制

  ```python
  # 二进制转化成十进制
  v1 = '0b1101'
  result = int(v1,base=2)
  print(result)
  
  # 八进制转化成十进制
  v1 = '0o1101'
  result = int(v1,base=8)
  print(result)
  
  # 十六进制转化成十进制
  v1 = '0x1101'
  result = int(v1,base=16)
  print(result)
  ```

  - hex 将十进制转换成十六进制

  ```python
  num = 16
  v1 = hex(num)
  print(v1)
  ```

- 编码相关

  - chr,将十进制数字转换成Unicode编码中的对应字符串。

  ```python
  v = chr(99)
  print(v)
  ```

  - ord,根据字符在Unicode编码中找到对应的十进制数字

  ```python
  nun = ord('哈')
  print(num)
  ```

  - 应用：

  ```python
  随机验证码
  import random
  def get_random_ocde(length=6):
      data = []
      for i in range(length):
          v = random.radint(65,90)
          data.append(chr(v))
      return ''.join(data)
  code = get_random_code()
  print(code)
  ```

  ```python
  import random #导入一个模块
  v = random.randint(起始，终止)#得到一个随机数
  ```

#### 0.5.9.2 5.9.2高级一点的内置函数

- map，循环每个元素（第二个参数），然后每个元素执行函数（第一个参数），将每个函数执行的结果保存到新的列表中，并返回。

```python
v1 = [11,22,33,44]
result = map(lambda x:x+100,v1)
print(list(result)) #py3需加list  py2不需要
```

- filter

```python
v = [1,2,3,4,'df',34,'kjh']
第一种
def func(x):
    if type(x) == int:
        return True
    return False
result = fliter(func,v)
print(list(result))
第二种
result = filter(lambda x:True if type(x) == int else False,v)
print(list(result))
第三种
result = filter(lambda x:type(x) == int,v)
print(list(result))  #x必须传

```

- reduce

```python
import functools
v = ['wo','shi','chuanqi']
第一种
def func(x,y):
    return x+y
result = functools.reduce(func,v)
print(result)
第二种
result = functools.reduce(lambda.x,y:x+y,v)
print(result) #woshichuanqi 数字可以加减乘除
```



- 面试题

```python
# 1字节等于8位
# IP: 192.168.12.79  ->  001010010 . 001010010 . 001010010 . 001010010

# 1. 请将 ip = "192.168.12.79" 中的每个十进制数转换成二进制并通过,连接起来生成一个新的字符串。
ip = "192.168.12.79"
ip_list = ip.split('.') # ['192','168','12','79']
result = []
for item in ip_list:
    result.append(bin(int(item)))
print(','.join(result))


# 2. 请将 ip = "192.168.12.79" 中的每个十进制数转换成二进制: 
#          0010100100001010010001010010001010010 -> 十进制的值。
ip = '192.168.7.13'
print(int(''.join([data[2:].rjust(8,'0') if data[2:]!=8 else data[2:] for data in [bin(int(item)) for item in ip.split('.')]]),base=2))
#
```

- 常用的内置函数有哪些？
- filter/map/reduce是什么意思？
- 什么是匿名函数？

```python
def func():
    pass
v = [lambda x:x+10]
```

#### 0.5.9.3 递归

函数自己调用自己。（效率低不推荐使用）

```python
def func():
    print(1)
    func()
func()
```

```python
def func(i):
    print(i)
    func(i+1)
    return
func(1)
```

```python
def func(a,b):
    print(b)
    func(b,a+b)
    
v = func(0,1)
```

```python
def func(a):
    if a == 5:
        return 100000
    result = func(a+1) + 10
    return result

v = func(1)
print(v)
```



### 0.5.10 装饰器

- 装饰器：在不改变原函数内部代码的基础上，在函数执行之前和之后自动执行某个功能。（他们是修改其他函数的功能的函数。有助于让我们的代码更pythonic（python范儿））

- 应用场景：想要为函数扩展功能时，可以选择用装饰器。
- 装饰器编写格式(双层嵌套)：

```python
def 外层函数（参数）:
    def 内层参数(*args,**kwargs):
        return 参数(*args,**kwargs)
    return 内层函数
```

传参时候加*args，**kwargs由于每次传参时候参数格式不同，减少定义函数的繁琐。

- 装饰器应用格式（@外层函数）：

```python
@外层函数
def index():
    pass
index()
```

```python
def x(func):
    def inner(*args,**kwargs):
        return func(*args,**kwargs)
    return inner
@x
def index(a1):
    pass

```

```python
def x(func):
    def inner(a1,a2):
        return func(a1,a2)
    return inner 

@x
def index(a1,a2):
	pass

# index = inner
index(1,2)

# ################################### 参数统一的目的是为了给原来的index函数传参
def x(func):
    def inner(a1,a2):
        return func()
    return inner 

@x
def index():
	pass
# func = 原来的index函数u
# index = inner
index(1,2)
```



```python
#计算函数执行时间
import time
def wrapper(func):
    def inner():
        start_time =time.time()
        v = func()
        end_time = time.time()
        print(end_time-start_time)
        return v
    return inner
@wrapper
def func1():
    time.sleep(2)
    print('123')
@wrapper
def func2():
    time.sleep(1)
    print('1234')
def func3():
    for i in range(10)
    print('12345')
func1()
        
```

- 带参数的装饰器

```python
#第一步：执行 ret = xxx(index)
#第二部：将返回值赋值给index = ret
@xxx
def index():
    pass
#第一步：执行v1 = uuu(9)
#第二部：ret = v1(index)
#第三部：index = ret
@uuu(9)
def index():
    pass

```

```python
# ################## 普通装饰器 #####################
def wrapper(func):
    def inner(*args,**kwargs):
        print('调用原函数之前')
        data = func(*args,**kwargs) # 执行原函数并获取返回值
        print('调用员函数之后')
        return data
    return inner 

@wrapper
def index():
    pass

# ################## 带参数装饰器 #####################
def x(counter):
    def wrapper(func):
        def inner(*args,**kwargs):
            data = func(*args,**kwargs) # 执行原函数并获取返回值
            return data
        return inner 
	return wrapper 

@x(9)
def index():
    pass
```

练习题

```python
# 写一个带参数的装饰器，实现：参数是多少，被装饰的函数就要执行多少次，把每次结果添加到列表中，最终返回列表。
def xxx(counter):
    print('x函数')
    def wrapper(func):
        print('wrapper函数')
        def inner(*args,**kwargs):
            v = []
            for i in range(counter):
                data = func(*args,**kwargs) # 执行原函数并获取返回值
                v.append(data)
            return v
        return inner
    return wrapper

@xxx(5)
def index():
    return 8

v = index()
print(v)

# 写一个带参数的装饰器，实现：参数是多少，被装饰的函数就要执行多少次，并返回最后一次执行的结果【面试题】
def xxx(counter):
    print('x函数')
    def wrapper(func):
        print('wrapper函数')
        def inner(*args,**kwargs):
            for i in range(counter):
                data = func(*args,**kwargs) # 执行原函数并获取返回值
            return data
        return inner
    return wrapper

@xxx(5)
def index():
    return 8

v = index()
print(v)
# 写一个带参数的装饰器，实现：参数是多少，被装饰的函数就要执行多少次，并返回执行结果中最大的值。
def xxx(counter):
    print('x函数')
    def wrapper(func):
        print('wrapper函数')
        def inner(*args,**kwargs):
            value = 0
            for i in range(counter):
                data = func(*args,**kwargs) # 执行原函数并获取返回值
                if data > value:
                    value = data 
            return value
        return inner
    return wrapper

@xxx(5)
def index():
    return 8

v = index()
print(v)
```

```python
def x(counter):
    print('x函数')
    def wrapper(func):
        print('wrapper函数')
        def inner(*args,**kwargs):
            if counter:
                return 123
            return func(*args,**kwargs)
        return inner
    return wrapper

@x(True)
def fun990():
    pass

@x(False)
def func10():
    pass
```



### 0.5.11 5.11推导式

- 列表推导式

  - 基本格式

  ```python
  """
  目的：方便生成一个列表。
  格式：
  	v1 = [i for i in 可迭代对象]
  	v2 = [i for i in 可迭代对象 if 条件] #条件为True才进行append
  """
  v1 = [i for i in 'alex']
  v2 = [i+100 for i in range(10)]
  v3 = [99 if i>5 else 66 for i in range(10)]
  
  def func():
      return 100
  v4 = [func for i in range(10)]
  v5 = [lambda : 100 for i in range(10)]
  result = v5[9]()
  def func():
      return i #此处i未被定义会报错
  v6 = [func for i in range(2)]
  result = v6[1]()
  v7 = [lambda :i for i in range(3)]
  result = v7[1]() #执行此处是i已循环完毕
  
  v8 = [lambda x:x*i i in range(4)]
  #1.问v8是什么？ v8为列表存放了四个lambda函数的内存地址
  #2.问v8[2](3)的结果是什么？ return 9
  def num():
      return[lambda x: x*i for i in range(4)]
  print([m(6) for m in num()])
  #[18,18,18,18]
  #筛选
  v9 = [i for i in range(10) if i>7 ]
  #[8,9]
  
  ```

- 集合推导式

```python
v1 = {i for i in 'alex'}
```

- 字典推导式

```python
v1 = {'k'+str(i):i for i in range(4)}
```

### 0.5.12 暂时未讲

- 元数据：flask框架
- 多个装饰器：flask框架

```python
@x1
@x2
def func():
    pass
```

## 0.6 第六章 模块

### 0.6.1 模块的基本知识

- 什么是模块：写好了的对程序员可以提供某方面功能的py文件。
- 什么是包：存储了多个py文件的文件夹。（如果导入的一个包，这个包里的模块默认是不可用的，导入一个包相当于执行‘__ init__' .py文件内容。）
- 常见的内置模块
  - random
  - hashlib
  - getpass
  - os
  - sys
  - time(三种类型)
  - datetime 和 timezone[了解]
  - json
    - dumps
    - loads
  - pickle
  - shutil、
  - logging
  - copy
- 模块的分类：内置模块、第三方模块、自定义模块。
- 内置模块，python内部提供的功能。

```python
import sys
print(sys.argv) #http://www.cnblogs.com/aland-1415/p/6613449.html#top
```

- 第三方模块，下载/安装/使用。
  - 源码安装：
    - 下载源码包：压缩文件。
    - 解压文件
    - 打开cmd窗口，并进入此目录：cd C:\Python36\Lib\site-packages
    - 执行 python36 setup.py build
    - 执行：python36 setup.py install
  - 安装路径：C:\Python36\Lib\site-packages
  - 了解的第三方模块：
    - xlrd
    - request

```python
#把pip.exe所在的目录添加到环境变量中。
pip install 要安装的模块名称 #pip install
```

- 自定义模块
  - xxx.py
  - py文件夹
  - 文件夹''' _ _init_ _.py '''

```python
def f1():
    print('f1')
def f2():
    print('f2')
```

- x1.py

```python
#调用自定义模块中的功能
import xxx
xxx.f1()
xxx.f2()
```

- 运行

```python
python x1.py
```

### 0.6.2 模块的调用

```python
import time
v = time.time()#获取当前时间
time.sleep(n)#(睡眠n秒)
```

示例一

```python
# xxx.py

#!/usr/bin/env python
# -*- coding:utf-8 -*-

def show():
    print('我司里种种')

def func():
    pass

print(456)
```

```python
# 导入模块，加载此模块中所有的值到内存
import xxx
print(123)
func()#因为函数已加载到内存，先执行模块的全局在执行本域内
```

```python
# 导入模块,多种导入方式
from xxx import func,show
from xxx import func
from xxx import show
from xxx import *
func()
```

导入模块：

- import
  - import 模块1                                    模块1.函数()
  - import 模块1.模块2.模块3                模块1.模块2.模块3.函数()
- from 模块 import xxx
  - from 模块.模块 import 函数		函数()
  - from 模块.模块 import 函数 as  f         f()
  - from 模块.模块 import *                      函数1()    函数2()
  - from 模块 import  模块                        模块.函数()
  - from 模块 import  模块  as m              m.函数()

示例二：

文件夹下的py文件调取

```python
xxx#文件夹
	-a.py
    -b.py
    -c.py
bao.py
```

```python
import xxx.a
xxx.a.func()
```

```python
from xxx import a
a.func()
```

```python
from xxx.a import func
func()
```

小结：

- 模块和要执行的py文件在同一目录且需要模块中的很多功能时，推荐用：import模块。
- 其他推荐：from模块import模块 模块.函数（）
- 其他推荐：from模块.模块 import函数 函数（）

注意：sys.path的作用是什么

![1555577445171](C:\Users\xiaohui\AppData\Roaming\Typora\typora-user-images\1555577445171.png)

![1555577465736](C:\Users\xiaohui\AppData\Roaming\Typora\typora-user-images\1555577465736.png)



#### 0.6.2.1 6.1.1将制定的‘字符串’进行加密（hashlib）。

作用：密文验证、校验文件的一致性、md5、sha

```python
import hashlib
md5 = hashlib.sha1('盐'.encode())
md5.update(b'str')
print(md5.hexdigest())
```

```python
import hashlib
def get_md5(data):
    obj =hashlib.md5()
    obj.update(data.encode('utf-8'))
    result = obj.hexdigest()
    return result
val = get_md5('123')
print(val)
```

#### 0.6.2.2 加盐

```python
import hashlib
def get_md5(data):
    obj = hashlib.md5('sdsd'.encode('utf-8'))
    obj.update(data.encode('utf-8'))
    result = obj.hexdigest()
    return result
val = get_md5('110')
print(val)
```

加盐的应用

```python
import hashlib
USER_LIST = []
def get_md5(data):
    obj = hashlib.md5('jgh',encode('utf-8'))
    obj.update(data.encode('utf-8'))
    result = obj.hexdigest()
    return result
def register():
    print('*********用户注册*********')
    while True:
        user = input('输入用户名：')
        if user == 'N':
            return
        pwd = input('输入密码：')
        tempe = {'username':user,'password':get_md5(pwd)}
        USER_LIST.append(temp)
def login():
    print('********请登录********')
    user = input('请输入用户名：')
    pwd = input('请输入明码：')
    for item in USER_LIST:
        if item['username'] == user and item['password'] == get_md5(pwd):
            return True
register()
result = login()
if result:
    print('登录成功')
else:
    print('登录失败')
    
```

- 密码不显示（只能在终端运行）

```python
import getpass
pwd = getpass.getpass('请输入密码：')
if pwd == '123':
    print('输入正确')
```

#### 0.6.2.3 sys 

- python解释器相关的数据

  - sys.gatrefcount,获取一个值的应用计数

  ```python
  a = [11,22]
  b = a
  print(sys.gatrefcount(a))
  ```

  - sys.getrecursionlimit ,python默认支持的递归数量
  - sys.stdout.write --->print(进度)

  ```python
  import time
  for i in range(1,101):
      msg = '%s%%\r' %i
      print(msg,end='')
      time.sleep(0.05)
  ```

  - sys.argv 获取命令行的参数

  ```python
  #!/usr/bin/env python
  # -*- coding:utf-8 -*-
  '''
  让用户执行脚本传入要删除的文件路径，在内部帮助用将目录删除。
  C:\Python36\python36.exe D:/code/s21day14/7.模块传参.py D:/test
  C:\Python36\python36.exe D:/code/s21day14/7.模块传参.py
  '''
  import sys
  # 获取用户执行脚本时，传入的参数。
  # C:\Python36\python36.exe D:/code/s21day14/7.模块传参.py D:/test
  # sys.argv = [D:/code/s21day14/7.模块传参.py, D:/test]
  path = sys.arg[1]
  shutil.retree(path)
  ```

  - sys.path 模块搜索路径，默认python去导入模块时，会按照sys.path中的路径挨个查找。一个模块是否导入全看sys.path中是否有这个模块所在的路径。

  ```python
  import sys #调用模块
  sys.path.append('路径')#添加要增加的模块路径
  import 模块#调用新增加的模块
  ```
  
  - sys.modules 存储了当前程序中用到的所有模块，反射本文件中的内容

#### 0.6.2.4 os

和操作系统相关的数据。

- os.makedirs，创建目录和子目录
- os.path.exists(path) ,如果path路径存在则返回True,不存在则返回False

```python
import os
file_path = r'路径下的某个文件'
file_folder = os.path.dirname(file_path)#获取文件的上级目录
if not os.path.exists(file_folder):#看os.path.exists(path)解释
    os.makedirs(file_folder)#按照地址创建文件夹
with open(file_path,mode='w',encoding='utf-8') as f:
    f.write('asdf')
```

- os.path.getsize('pack')获取文件的大小

- os.stat('文件名').st_size ,获取文件大小

```python
import os
# 1.读取文件大小（字节）
file_size = os.stat('文件名').st_size

# 2.一点一点的读取文件
read_size = 0
with open('文件名',mode='rb') as f1,open('文件名2',mode='wb') as f2:
    while read_size < file_size:
        chunk = f1.read(1024) #每次最多读取1024字节
        f2.write(chunk)
        read_size += len(chunk)
        val = int(read_size/file_size*100)
        print('%s%%\r' %val ,end='')
```

- os.path.abspath() ,获取一个文件的绝对路径

```python
path = '文件名'

import os
v1 = os.path.abspath(path)
print(v1)
```

- os.path.dirname ,获取路径的上级目录

```python
import os
v = r"D:\code\s21day14\20190409_192149.mp4"

print(os.path.dirname(v))
```

- os.path.join ,路径的拼接

```python
import os
path = "D:\code\s21day14" # user/index/inx/fasd/
v = 'n.txt'
result = os.path.join(path,v)
print(result)
result = os.path.join(path,'n1','n2','n3')
print(result)
```

```python
import os
print("1:",os.path.join('aaaa','/bbbb','ccccc.txt'))
print("2:",os.path.join('/aaaa','/bbbb','/ccccc.txt'))  #不良写法习惯
print("3:",os.path.join('aaaa','./bbb','ccccc.txt'))   
print("22:",os.path.join('/aaaa/','bbbb/','ccccc.txt'))  #通常可以这样写
输出为
#以字符串中含有 / 的第一个开始拼接
1: /bbbb/ccccc.txt
#当有多个是最后一个才开始，
2: /ccccc.txt

#以./ 的上一个开始拼接
3: aaaa/bbb/ccccc.txt

22: aaaa/bbb/ccccc.txt
--------------------- 
作者：furuit 
来源：CSDN 
原文：https://blog.csdn.net/fu6543210/article/details/80032895 
版权声明：本文为博主原创文章，转载请附上博文链接！
```



- os.walk ,查看一个目录下所有的文件（所有层）

```python
import os
result = os.walk(r'路径)
for a,b,c in result:#a,正在查看的目录 b,此目录下的文件夹 c,此目录下的文件
	for item in c:
     	path = os.path.join(a,item)
		print(path)
```

- os.rename ,重命名

```python
import os
os.rename('db','ab')#在指定目录下将文件名为db的改为ab
```

- os.listdir(path)用于返回指定的文件夹包含的文件或文件夹的名字的列表。

```python
import os
path = r'E:\刘小辉作业\作业题'
dirs = os.listdir(path)
print(dirs)#文件夹下所有的文件、文件夹名名组成的列表。
```

- 补充：

  - 转义

  ```python
  v1 = r"D:\code\s21day14\n1.mp4"  (推荐)
  print(v1)
  
  
  v2 = "D:\\code\\s21day14\\n1.mp4"
  print(v2)
  ```

- shutil.rmtree(path)

```python
import shutil
shutil.rmtree(path)
```

#### 0.6.2.5 json

json是一个特殊的字符串。【长得像列表/字典/字符串/数字/真假】

- 所有的字符串都是双引号
- 最外层只能是列表或字典
- 只支持int float str list dict bool
- 存在字典中的key只能是str
- 不能连续load多次
- 字典或列表中如有中文，序列化时想要保留中文显示：

```python
v = {'k1':'alex','k2':'哈哈'}
import json
val =json.dumps(v,ensure_ascii=False)
print(val)
```

- dump #将内容写入到文件

```python
import json
v = {'k1':'alex','k2':'哈哈'}
f = open('x.txt',mode='w',encoding='utf-8')
val = json.dump(v,f)
f.close()
```

- dumps #将python的值转为json格式的字符串
- loads #将json的字符串转换成python类型

```python
import json
#序列化，将python的值转换为json格式的字符串。
v = [12,3,4,{'k1':'v1'},True,'asdf']
v1 = json.dumps(v)
print(v1)#[12, 3, 4, {"k1": "v1"}, true, "asdf"]
#json格式的字符串全部为双引号无单引号，bool值为小写

#反序列化，将json格式的字符串转换成python的数据类型
v2 = '["alex",123]'
print(type(v2))
v3 = json.loads(v2)
print(v3,type(v3))#['alex', 123] <class 'list'>


```

- load

  ```python
  import json
  v = {'k1':'alex','k2':'哈哈'}
  f = open('x.txt',mode='r',encoding='utf-8')
  data = json.load(f)
  f.close()
  print(data,type(data)) #与上部dump产生的文件一块运行
  ```

  

```python
	+-------------------+---------------+
    | Python            | JSON          |
    +===================+===============+
    | dict              | object        |
    +-------------------+---------------+
    | list, tuple       | array         |
    +-------------------+---------------+
    | str               | string        |
    +-------------------+---------------+
    | int, float        | number        |
    +-------------------+---------------+
    | True              | true          |
    +-------------------+---------------+
    | False             | false         |
    +-------------------+---------------+
    | None              | null          |
    +-------------------+---------------+
```

#### 0.6.2.6 pickle 和json对比

- json优点：所有语言通用；缺点：只能序列化基本的数据类型list/dict/int...
- pickle，优点：python中所有的东西都能被他序列化（socket对象），支持多次load；缺点：序列化的内容只有python认识。

```python
import pickle
# #################### dumps/loads ######################
v = {1,2,3}
val = pickle.dumps(v)
print(val)
data = pickle.loads(val)
print(data,type(data))
#########################
def f1():
    print('f1')
v1 = pickle.dumps(f1)
print(v1)
v2 = pickle.loads(v1)
v2()
#########
v = {1,2,3,4}
f = open('x.txt',mode='wb')
val = pickle.dump(v,f)
f.close()
f = open('x.txt',mode='rb')
data = pickle.load(f)
f.close()
print(data)
```

#### 0.6.2.7 shutil模块

```python
import shutil
# 删除目录
# shutil.rmtree('test')

# 重命名 移动文件
# shutil.move('test','ttt')

# 压缩文件
# shutil.make_archive('zzh','zip','D:\code\s21day16\lizhong')

# 解压文件
# shutil.unpack_archive('zzh.zip',extract_dir=r'D:\code\xxxxxx\xxxx',format='zip')
```

```python
import os
import shutil
from datetime import datetime
ctime = datetime.now().strftime('%Y-%m-%d-%H-%M-%S')
# 1.压缩xxx文件夹 zip
# 2.放到code目录（默认不存在）
# 3.将文件解压到D：\x1目录中。
if not os.path.exists('code'):
    os.makedirs('code')
shutil.make_archive(os.path.join('code',ctime),'zip','D:\code\s21day16\xxx')    
```

#### 0.6.2.8 time&datetime

- UTC/GMT：世界时间

- 本地时间：本地时区的时间

  ##### 6.1.8.1  time模块

  - time.time() ,时间戳：1970.1.1 00:00（自此时间开始）
  - time.sleep(10)，等待秒数。
  - time.timezone

  ```python
  # https://login.wx.qq.com/cgi-bin/mmwebwx-bin/login?loginicon=true&uuid=4ZwIFHM6iw==&tip=1&r=-781028520&_=1555559189206
  ```

  ##### 6.1.8.2  datetime模块

  - datetime.now()当前时间
  - strftime('%Y-%m-%d %H:%M:%S')格式化时间
  - strptime('2019-1-1 10:23:23','%Y-%m-%d %H:%M:%S')) 获取到一个datetime对象
  - timedelta(days=140) 时间加减
  - fromtimestamp(时间戳时间)  时间戳转datetime
  - timestap(datetime对象)  datetime转时间戳
  
  ```python
  #!/usr/bin/env python
  # -*- coding:utf-8 -*-
  import time
  from datetime import datetime,timezone,timedelta
  
  # ######################## 获取datetime格式时间 ##############################
  v1 = datetime.now() #当地时间
  print(v1)
  tz = timezone(timedelta(hours=7))
  v2 = datetime.now(tz)
  print(v2)
  v3 = datetime.utcnow() #当前utc时间
  print(v3)
  ######把datetime格式转换成字符串
  v1 = datetime.now()
  print(v1,type(v1))
  val = v1.strftime('%Y-%m-%d %H:%M:%S')
  print(val)
  #######把字符串格式转成datetime
  v1 = datetime.strptime('2012-02-14','%Y-%m-%d')
  print(v1)
  #####时间戳跟datetime关系
  ctime = time.time()
  print(ctime)
  v1 = datetime.fromtimestamp(ctime)
  print(v1)
  ```

#### 0.6.2.9 logging [暂未讲]

#### 0.6.2.10 异常处理

```python
try:
    val = input('请输入数字:')
    num = int(val)
except Exception as e:
    print('操作异常')
```

```python
# import requests
#
# try:
#     ret = requests.get('http://www.google.com')
#     print(ret.text)
# except Exception as e:
#     print('请求异常')
```

```python
def func(a):
    try:
        return a.strip()
    except Exception as e:
        pass
    return False

v = func('alex')
if not v:
    print('函数执行失败')
else:
    print('结果是',v)
```

练习题

```python
# 1. 写函数，函数接受一个列表，请将列表中的元素每个都 +100
def func(arg):
    result = []
    for item in arg:
        if item.isdecimal():
            result.append(int(item) + 100)
	return result 

# 2. 写函数去，接受一个列表。列表中都是url，请访问每个地址并获取结果。
import requests 
def func(url_list):
    result = []
    try:
        for url in url_list:
            response = requests.get(url)
            result.append(response.text)
	except Exception as e:
        pass
	return result 

def func2(url_list):
    result = []
    for url in url_list:
        try:
            response = requests.get(url)
            result.append(response.text)
        except Exception as e:
            pass
	return result 

func(['http://www.baidu.com','http://www.google.com','http://www.bing.com'])
```

#### 0.6.2.11 random

- choice 随机抽取一个
- sample  随机抽取多个
- shuffle  洗牌 算法 （无返回值）

```python
随机验证码
import random
def get_random_ocde(length=6):
    data = []
    for i in range(length):
        v = random.radint(65,90)
        data.append(chr(v))
    return ''.join(data)
code = get_random_code()
print(code)
```

#### 0.6.2.12 collections

- OderedDict
- namedtuple
- deque 双端队列
- defaultDict 默认字典，可以给字典的value设置一个默认值

### 0.6.3 定义模块

定义模块时可以把一个py文件或一个文件夹（包）当做一个模块，以便于以后其他py文件的调用。

对于包的定义：

- py2:文件夹中必须有_ _init_ _.py。
- py3:不需要_ _init_ _.py。
- 建议以后写代码时都要加上此文件。

### 0.6.4 迭代器和生成器

#### 0.6.4.1 迭代器

- 迭代器

  - 对某种对象(str/list/tuple/dict/set类创建的对象)-可迭代对象中的元素进行逐一获取，表象：具有`__next__`方法且每次调用都获取可迭代对象中的元素（从前到后一个一个获取）。
  - 列表转换成迭代器：
  - v1 = iter([11,22,33])
  - ``` v1 = [11,22,33,44].__iter__() ```
  - 迭代器想要获取每个值：反复调用  ```val = v1.__next__() ```

  ```python
  v1 = [11,22,33,44]
  
  # 列表转换成迭代器
  v2 = iter(v1)
  result1 = v2.__next__()
  print(result1)
  result2 = v2.__next__()
  print(result2)
  result3 = v2.__next__()
  print(result3)
  result4 = v2.__next__()
  print(result4)
  result5 = v2.__next__()
  print(result5)
  """
  # v1 = "alex"
  # v2 = iter(v1)
  # while True:
  #     try:
  #         val = v2.__next__()
  #         print(val)
  #     except Exception as e:
  #         break
  ```

  - 直到报错：stoplteration错误，表示迭代完毕。
  - 如何判别一个对象是否是迭代器：内部是否有`__next__方法` 。
  - for 循环

  ```python
  v1 = [11,22,33,44]
  
  # 1.内部会将v1转换成迭代器
  # 2.内部反复执行 迭代器.__next__()
  # 3.取完不报错
  for item in v1:
      print(item)
  ```

- 可迭代对象

  - 内部具有 `__iter__()` 方法且返回一个迭代器。（*）

  ```python
  v1 = [11,22,33,44]
  result = v1.__iter__()
  ```

  - 可以被for循环

表象：可以被for循环对象就可以成为是可迭代对象：‘x’ [11,2]

```python
class Foo:
    pass

obj = Foo()
```

如何让一个对象编程可迭代对象？

在类中实现`__iter__`方法且返回一个迭代器（生成器）

```python
class Foo:
    def __iter__(self):
        return iter([1,2,3,4])

obj = Foo()


class Foo:
    def __iter__(self):
        yield 1
        yield 2
        yield 3

obj = Foo()
```

备注：只要能被for循环就去看他内部的iter方法。


#### 0.6.4.2 生成器（函数的变异）

生成器推导式

```python
# def func():
#     result = []
#     for i in range(10):
#         result.append(i)
#     return result
# v1 = func()
v1 = [i for i in range(10)] # 列表推导式，立即循环创建所有元素。
print(v1)

# def func():
#     for i in range(10):
#         yield i
# v2 = func()
v2 = (i for i in range(10)) # 生成器推导式，创建了一个生成器，内部循环为执行。

# 面试题：请比较 [i for i in range(10)] 和 (i for i in range(10)) 的区别？
```

```python
# 示例一
# def func():
#     result = []
#     for i in range(10):
#         result.append(i)
#     return result
# v1 = func()
# for item in v1:
#    print(item)

# 示例二
# def func():
#     for i in range(10):
#         def f():
#             return i
#         yield f
#
# v1 = func()
# for item in v1:
#     print(item())

# 示例三：
v1 = [i for i in range(10)] # 列表推导式，立即循环创建所有元素。
v2 = (lambda :i for i in range(10))
for item in v2:
    print(item())
```



```python
# 函数
def func():
    return 123
func()
```

```python
# 生成器函数（内部是否包含yield）
def func():
    print('F1')
    yield 1
    print('F2')
    yield 2
    print('F3')
    yield 100
    print('F4')
# 函数内部代码不会执行，返回一个 生成器对象 。
v1 = func()
# 生成器是可以被for循环，一旦开始循环那么函数内部代码就会开始执行。
for item in v1:
    print(item)
```

```python
def func():
    count = 1
    while True:
        yield count
        count += 1
        
val = func()

for item in val:
    print(item)
```

小结：函数中如果存在yield，那么该函数就是一个生成器函数，调用生成器函数会返回一个生成器，生成器只有被for循环时，生成器函数内部的代码才会执行，每次循环都会获取yield返回的值。

```python
def func():
    count = 1
    while True:
        yield count
        count += 1
        if count == 100:
            return

val = func()
for item in val:
    print(item)
```

示例：读文件

```python
def func():
    """
    分批去读取文件中的内容，将文件的内容返回给调用者。
    :return:
    """
    cursor = 0
    while True:
        f = open('db', 'r', encoding='utf-8')# 通过网络连接上redis
        # 代指   redis[0:10]
        f.seek(cursor)
        data_list =[]
        for i in range(10):
            line = f.readline()
            if not line:
                return
            data_list.append(line)
        cursor = f.tell()
        f.close()  # 关闭与redis的连接


        for row in data_list:
            yield row


for item in func():
    print(item)
```

- yeild from关键字【未讲】
- 生成器推导式【未讲】

总结

- 迭代器，对可迭代对象中的元素进行逐一获取，迭代器对象的内部都有一个 __next__方法，用于以一个个获取数据。

- 可迭代对象，可以被for循环且此类对象中都有 __iter__方法且要返回一个迭代器（生成器）。

- 生成器，函数内部有yield则就是生成器函数，调用函数则返回一个生成器，循环生成器时，则函数内部代码才会执行。

  特殊的迭代器（**）：

  ```python
  def func():
      yield 1
      yield 2
      yield 3
  
  v = func()
  result = v.__next__()
  print(result)
  result = v.__next__()
  print(result)
  result = v.__next__()
  print(result)
  result = v.__next__()
  print(result)
  ```

  特殊的可迭代对象：

  ```python
  def func():
      yield 1
  
  v = func()
  result = v.__iter__()
  print(result)
  ```

### 0.6.5 项目文件

- bin开始文件夹 start

  ```python
  import os
  import sys
  base_path = os.path.dirname(os.path.dirname(__file__))
  sys.path.append(base_path)
  from src improt core
  ```

- conf配置文件夹 settings

- src 业务逻辑

  ```python
  student.py
  from src import sore
  core.py
  from conf import settings
  ```

- db数据文件

- lib扩展模块

- log日志文件

