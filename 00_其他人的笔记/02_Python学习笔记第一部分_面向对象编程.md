

## 0.1 第七章 面向对象

基本概念：

- 什么是类：具有相同方法和属性的一类事物
- 什么是对象、实例：一个拥有具体属性值和动作的具体个体
- 实例化：从一个类得到一个具体对象的过程

组合：

- 一个类的对象作为另一个类对象的实例变量
  - python是课程类的对象
  - xx是学生类的对象
  - xx.course = python

面向对象的三大特性：封装/继承/多态

- 封装
  - 广义的封装：类中有成员
  - 狭义的封装：私有成员
  - 函数封装到类

```python
class File:
    def read(self):
        pass
    def write(self):
        pass
    
```

- 数据封装到对象	

```python
class Person:
    def __init__(sef,name,age):
        self.name = name
        self.age = age
p = Person('alex',19)
```

- 继承
  - 父类、基类、超类
  - 子类、派生类
  - 单继承：子类可以使用父类的方法
  - 多继承：
    - py2深度优先
    - py3广度优先

```python
class Base:
    pass
class Foo(Base):
    pass
```

备注：

​		多继承

​		self到底是谁？

​		self是由于哪个类创建，则找方法时候就从他开始找。

- 多态
  - 一个类表现出来的多种状态》多各类表现出相似状态
    - user  可以浏览商品、购买支付
    - vip_user 可以浏览商品、购买支付
  - 鸭子类型
  - user  和vip_user 有相似的特性
  - list 和tuple有相似的特性

```python
def func(arg): # 多种类型，很多事物
    arg.send() # 必须具有send方法，呱呱叫
```

格式和关键词

```python
class 类:
    def __init__(self,x):
        self.x = x 
        
    def 方法(self,name):
        print(self.x, name)
        
# 实例化一个类的对象
v1 = 类(666)
v2.方法('alex')
```

关键词：

- 类
- 对象
- 方法

什么时候用面向对象？

- 函数（业务功能）比较多，可以使用面向对象来进行归类。
- 想要做数据封装（创建字典存储数据时，面向对象）。
- 游戏示例：创建一些角色并根据角色需要再创建人物。

### 0.1.1 面向对象的基本格式

类和对象的关系：对象是类的一个实例。

self是一个形式参数，对象调用方法时，python内部将该对象传给这个参数。

```python
#定义类
class 类名（首字母大写）():
    def 方法名(self,name):
        print(name)
        return 123
	def 方法名(slef,name):
        print(name)
        return 123
    def 方法名(slef,name):
        print(name)
        return 123
#调用类中的方法
#1.创建该类的对象
obj = 类名()
#2.通过对象调用方法
result = obj.方法名('alex')
print(result)
    
```

应用场景：遇到很多函数，需要给函数进行归类和划分。【封装】

- 不可修改类型（可命名元组）
  - 创建一个类，这个类没有方法，所有属性不可修改。

```python
from collections import namedtuple   # 可命名元组
Course = namedtuple('Course',['name','price','teacher'])
python = Course('python',19800,'alex')
print(python)
print(python.name)
print(python.price)
```



练习题

```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-

class Db:
    def db_read(self):
        pass

    def db_write(self):
        pass

    def db_delete(self):
        pass

    def db_update(self):
        pass

class File:
    def file_read(self):
        pass

    def file_write(self):
        pass

    def file_delete(self):
        pass

    def file_update(self):
        pass

class Redis:
    def redis_read(self):
        pass

    def redis_write(self):
        pass

    def redis_delete(self):
        pass

    def redis_update(self):
        pass
```

### 0.1.2 对象的作用

存储一些值，以后方便自己使用。

```python
class File:
    def read(self):
        with open(self.xxxxx, mode='r', encoding='utf-8') as f:
            data = f.read()
        return data

    def write(self, content):
        with open(self.xxxxx, mode='a', encoding='utf-8') as f:
            f.write(content)

# # 实例化了一个File类的对象
obj1 = File()
# # 在对象中写了一个xxxxx = 'test.log'
obj1.xxxxx = "test.log"
# # 通过对象调用类中的read方法，read方法中的self就是obj。
# # obj1.read()
obj1.write('alex')


# 实例化了一个File类的对象
obj2 = File()
# 在对象中写了一个xxxxx = 'test.log'
obj2.xxxxx = "info.txt"
# 通过对象调用类中的read方法，read方法中的self就是obj。
# obj2.read()
obj2.write('alex')
```

```python
class Person:
    def show(self):
        temp = "我是%s,年龄：%s,性别：%s " %(self.name,self.age,self.gender,)
        print(temp)
        

p1 = Person()
p1.name = '李邵奇'
p1.age = 19
p1.gender = '男'
p1.show()

p2 = Person()
p2.name = '利奇航'
p2.age = 19
p2.gender = '男'
p2.show()
```

```python
class Person:
    def __init__(self,n,a,g): # 初始化方法（构造方法），给对象的内部做初始化。
        self.name = n
        self.age = a
        self.gender = g

    def show(self):
        temp = "我是%s,年龄：%s,性别：%s " % (self.name, self.age, self.gender,)
        print(temp)

# 类() 实例化对象，自动执行此类中的 __init__方法。
p1 = Person('李兆琪',19,'男')
p1.show()

p2 = Person('利奇航',19,'男')
p2.show()
```

小结：将数据封装到对象，方便使用。

```python
"""
如果写代码时，函数比较多比较乱。
1. 可以将函数归类并放到同一个类中。
2. 函数如果有一个反复使用的公共值，则可以放到对象中。
"""

class File:
    def __init__(self,path):
        self.file_path = path
        
    def read(self):
        print(self.file_path)
    
    def write(self,content):
        print(self.file_path)
    
    def delete(self):
        print(self.file_path)
    
    def update(self):
        print(self.file_path)
    
p1 = File('log.txt')
p1.read()

p2 = File('xxxxxx.txt')
p2.read()
```

```python
# 1. 循环让用户输入：用户名/密码/邮箱。 输入完成后再进行数据打印。
# ########## 以前的写法
USER_LIST = []
while True:
    user = input('请输入用户名：')
    pwd = input('请输入密码：')
    email = input('请输入邮箱：')
    temp = {'username':user,'password':pwd,'email':email}
    USER_LIST.append(temp)
for item in USER_LIST:
    temp = "我的名字：%s,密码：%s,邮箱%s" %(item['username'],item['password'],item['email'],)
    print(temp)
    
# ########## 面向对象写法

class Person:
    def __init__(self,user,pwd,email):
        self.username = user
        self.password = pwd
        self.email = email
	
USER_LIST = [对象(用户/密码/邮箱),对象(用户/密码/邮箱),对象(用户/密码/邮箱)]
while True:
    user = input('请输入用户名：')
    pwd = input('请输入密码：')
    email = input('请输入邮箱：')
    p = Person(user,pwd,email)
    USER_LIST.append(p)

for item in USER_LIST:
    temp = "我的名字：%s,密码：%s,邮箱%s" %(item.username,item.password,item.email,)
    print(temp)

# ########## 面向对象写法

class Person:
    def __init__(self,user,pwd,email):
        self.username = user
        self.password = pwd
        self.email = email
        
	def info(self):
        return "我的名字：%s,密码：%s,邮箱%s" %(item.username,item.password,item.email,)
    
USER_LIST = [对象(用户/密码/邮箱),对象(用户/密码/邮箱),对象(用户/密码/邮箱)]
while True:
    user = input('请输入用户名：')
    pwd = input('请输入密码：')
    email = input('请输入邮箱：')
    p = Person(user,pwd,email)
    USER_LIST.append(p)

for item in USER_LIST:
    msg = item.info()
    print(msg)
```

### 0.1.3 游戏开发示例

```python
class Police:
	def __init__(self,name) 
		self.name = name 
         self.hp = 10000
    
    def tax(self):
        msg = "%s收了个税。" %(self.name,)
        print(msg)
	
    def fight(self):
        msg = "%s去战了个斗。" %(self.name,)

lsq = Police('李邵奇') 
zzh = Police('渣渣会')
tyg = Police('堂有光')


class Bandit:
    def __init__(self,nickname) 
		self.nickname = nickname 
		self.hp = 1000
	
    def murder(self,name):
        msg = "%s去谋杀了%s" %(self.nickname, name,)
        
        
lcj = Bandit('二蛋')
lp = Bandit('二狗')
zsd = Bandit('狗蛋')

# 1. 二狗去谋杀渣渣会，二狗生命值-100; 渣渣会生命值减5000
lp.murder(zzh.name)
lp.hp = lp.hp - 100
zzh.hp = zzh.hp - 5000
# ... 
```

```python
class Police:
	def __init__(self,name) 
		self.name = name 
         self.hp = 10000
    
    def dao(self,other):
        msg = "%s个了%s一刀。" %(self.name,other.nickname)
        self.hp = self.hp - 10
        other.hp = other.hp - 50
        print(msg)
	
    def qiang(self):
        msg = "%s去战了个斗。" %(self.name,)
        
	def quan(self,other):
        msg = "%s个了%s一全。" %(self.name,other.nickname)
        self.hp = self.hp - 2
        other.hp = other.hp - 10
        print(msg)
        
        
class Bandit:
    def __init__(self,nickname) 
		self.nickname = nickname 
		self.hp = 1000
	
    def qiang(self,other):
        msg = "%s个了%s一全。" %(self.nickname,other.name)
        self.hp -= 20
        other.hp -= 500
    
	
lcj = Bandit('二蛋')


lsq = Police('李邵奇')
lsq.dao(lcj)
lsq.quan(lcj)
lcj.qiang(lsq)
```

### 0.1.4 继承

```python

# 父类(基类)
class Base:
    def f1(self):
        pass
# 子类（派生类）
class Foo(Base):
    def f2(self):
        pass

# 创建了一个字类的对象
obj = Foo()
# 执行对象.方法时，优先在自己的类中找，如果没有就是父类中找。
obj.f2()
obj.f1()

# 创建了一个父类的对象
obj = Base()
obj.f1()
```

问题：什么时候才能用继承？多个类中如果有公共的方法，可以放到基类中避免重复编写。

```python
class Base:
    def f1(self):
        pass
    
class Foo(Base):
    def f2(self):
        pass
    
class Bar(Base):
    def f3(self):
        pass

obj1 = Foo()

obj2 = Bar()
```

继承关系中的查找方法的顺序：

```python
# 示例一
class Base:
    def f1(self):
        print('base.f1')
        
class Foo(Base):
    def f2(self):
        print('foo.f2')
        
obj = Foo()
obj.f1()
obj.f2()

# 示例二
class Base:
    def f1(self):
        print('base.f1')
        
class Foo(Base):
    def f2(self):
        self.f1()
        print('foo.f2')
        
obj = Foo()
obj.f2()

# 示例三
class Base:
    def f1(self):
        print('base.f1')
        
class Foo(Base):
    def f2(self):
        self.f1()
        print('foo.f2')
	def f1(self):
        print('foo.f1')
        
obj = Foo()
obj.f2()

# 示例四
class Base:
    def f1(self):
        self.f2()
        print('base.f1')
	def f2(self):
        print('base.f2')
class Foo(Base):
    def f2(self):
        print('foo.f2')
        
obj = Foo()
obj.f1()

# 示例五
class TCPServer:
    pass
class ThreadingMixIn:
    pass
class ThreadingTCPServer(ThreadingMixIn, TCPServer): 
    pass

# 示例六
class BaseServer:
    def serve_forever(self, poll_interval=0.5):
        self._handle_request_noblock()
	def _handle_request_noblock(self):
        self.process_request(request, client_address)
        
	def process_request(self, request, client_address):
        pass
    
class TCPServer(BaseServer):
    pass

class ThreadingMixIn:
    def process_request(self, request, client_address):
        pass
    
class ThreadingTCPServer(ThreadingMixIn, TCPServer): 
    pass

obj = ThreadingTCPServer()
obj.serve_forever()
```

注意事项：

- self到底是谁？
- self是哪个类创建的，就从此开始找，自己没有找父类。

### 0.1.5 多态（多种形态/多种类型）鸭子模型

```python
# Python
def func(arg):
    v = arg[-1] # arg.append(9)
    print(v)

# java
def func(str arg):
    v = arg[-1]
    print(v)
```

面试题：什么是鸭子模型

```python
# Python
def func(arg):
    v = arg[-1] # arg.append(9)
    print(v)

# java
def func(str arg):
    v = arg[-1]
    print(v)
```

概念：同一操作作用于不同的对象，可以有不同的解释，产生不同的执行结果，这就是多态性。简单的说:就是用基类的引用指向子类的对象。

<https://www.cnblogs.com/hai-ping/articles/2807750.html>

![1555993885057](C:\Users\xiaohui\AppData\Roaming\Typora\typora-user-images\1555993885057.png)

面向过程和面向对象的区别：  面向过程就是分析出解决问题所需要的步骤，然后用函数把这些步骤一步一步实现，使用的时候一个一个依次调用就可以了。

面向对象是把构成问题事务分解成各个对象，建立对象的目的不是为了完成一个步骤，而是为了描叙某个事物在整个解决问题的步骤中的行为。  （<https://zhidao.baidu.com/question/2089034.html>）

（<https://www.cnblogs.com/wangmo/p/7751199.html>）

### 0.1.6 成员

- 类
  - 类变量
  - 绑定方法
  - 类方法
  - 静态方法
  - 属性
- 实例（对象）
  - 实例变量

#### 0.1.6.1 实例变量

```python
class Foo:
    def __init__(self,name):
        self.name = name
    def info(self):
        pass
obj1 = Foo('alex')
obj2 = Foo('eric')
```

![1556089497767](C:\Users\xiaohui\AppData\Roaming\Typora\typora-user-images\1556089497767.png)

#### 0.1.6.2 类变量

![1556089557239](C:\Users\xiaohui\AppData\Roaming\Typora\typora-user-images\1556089557239.png)

- 定义：卸载类的下一级和方法同一级。
- 访问：

```python
类.类变量名称
对象.类变量名称
```

- 面试题

```python
class Base:
    x = 1
    
obj = Base()


print(obj.x) # 先去对象中找，没有再去类中找。
obj.y = 123  # 在对象中添加了一个y=123的变量。
print(obj.y)
obj.x = 123
print(obj.x)
print(Base.x)
```

```python
class Parent:
    x = 1
    
class Child1(Parent):
    pass

class Child2(Parent):
    pass

print(Parent.x,Child1.x,Child2.x) # 1 1 1
Child1.x = 2
print(Parent.x,Child1.x,Child2.x) # 1 2 1
Child2.x = 3
print(Parent.x,Child1.x,Child2.x) # 1 2 3
```

小结：找变量优先找自己，自己没有找类或基类；修改或赋值只能在自己的内部设置。

![1556089907542](C:\Users\xiaohui\AppData\Roaming\Typora\typora-user-images\1556089907542.png)

#### 0.1.6.3 方法（绑定方法/普通方法）

- 定义：至少有一个self参数
- 执行：先创建对象，有对象、方法。

```python
class Foo:
    def func(self,a,b):
        print(a,b)
        
obj = Foo()
obj.func(1,2)
# ###########################
class Foo:
    def __init__(self):
        self.name = 123

    def func(self, a, b):
        print(self.name, a, b)

obj = Foo()
obj.func(1, 2)
```

#### 0.1.6.4 静态方法

- 定义：
  - @staticmethod装饰器
  - 参数无限制
- 执行：
  - 类.静态方法名（）
  - 对象.静态方法（）（不推荐）

```python
class Foo:
    def __init__(self):
        self.name = 123

    def func(self, a, b):
        print(self.name, a, b)

    @staticmethod
    def f1():
        print(123)

obj = Foo()
obj.func(1, 2)

Foo.f1()
obj.f1() # 不推荐
```

#### 0.1.6.5 类方法

- 定义：
  - @classmethon装饰器
  - 至少有cls参数，当前类
- 执行：
  - 类.类方法()
  - 对象.类方法()（不推荐）

```python
class Foo:
    def __init__(self):
        self.name = 123

    def func(self, a, b):
        print(self.name, a, b)

    @staticmethod
    def f1():
        print(123)

    @classmethod
    def f2(cls,a,b):
        print('cls是当前类',cls)
        print(a,b)

obj = Foo()
obj.func(1, 2)

Foo.f1()
Foo.f2(1,2)
```

面试题：

```python
# 问题： @classmethod和@staticmethod的区别？
"""
一个是类方法一个静态方法。 
定义：
	类方法：用@classmethod做装饰器且至少有一个cls参数。
	静态方法：用staticmethod做装饰器且参数无限制。
调用：
	类.方法直接调用。
	对象.方法也可以调用。 
"""
```

#### 0.1.6.6 属性

- 定义：
  - @property装饰器
  - 只有一个self参数
- 执行：
  - 对象.方法     ps：不用加括号

```python
class Foo:

    @property
    def func(self):
        print(123)
        return 666

obj = Foo()
result = obj.func
print(result)
```

```python
# 属性的应用

class Page:
    def __init__(self, total_count, current_page, per_page_count=10):
        self.total_count = total_count
        self.per_page_count = per_page_count
        self.current_page = current_page
    @property
    def start_index(self):
        return (self.current_page - 1) * self.per_page_count
    @property
    def end_index(self):
        return self.current_page * self.per_page_count


USER_LIST = []
for i in range(321):
    USER_LIST.append('alex-%s' % (i,))

# 请实现分页展示：
current_page = int(input('请输入要查看的页码：'))
p = Page(321, current_page)
data_list = USER_LIST[p.start_index:p.end_index]
for item in data_list:
    print(item)
```

### 0.1.7 成员装饰符

- 公有，所有地方都能访问到。
- 私有，只有自己可以访问。

```python
class Foo:
    def __init__(self, name):
        self.__name = name

    def func(self):
        print(self.__name)


obj = Foo('alex')
# print(obj.__name)
obj.func()
```

```python
class Foo:
    __x = 1

    @staticmethod
    def func():
        print(Foo.__x)


# print(Foo.__x)
Foo.func()
```

```python
class Foo:

    def __fun(self):
        print('msg')

    def show(self):
        self.__fun()

obj = Foo()
# obj.__fun()
obj.show()
```

### 0.1.8 小补充

```python
class Foo:
    def __init__(self,num):
        self.num = num
        
        
cls_list = []
for i in range(10):
    cls_list.append(Foo)
    
for i in range(len(cls_list)):
    obj = cls_list[i](i)
    print(obj.num)
```

```python
class Foo:
    def __init__(self,num):
        self.num = num
        
B = Foo
obj = B('alex')
```

```python
class Foo:
	def f1(self):
        print('f1')
    
    def f2(self):
        print('f2')

obj = Foo()

v = [ obj.f1,obj.f2 ]
for item in v:
    item()
```

```python
class Foo:
    def f1(self):
        print('f1')
    
    def f2(self):
        print('f2')
        
	def f3(self):
        v = [self.f1 , self.f2 ]
        for item in v:
            item()
            
obj = Foo()
obj.f3()
```

```python
class Account:
    
    def login(self):
        pass
    
    def register(self):
        pass
    
    def run(self):
        info = {'1':self.register, '2':self.login }
        choice = input('请选择:')
        method = info.get(choice)
        method()
```

```python
class Foo:
    pass

class Foo(object):
    pass

# 在python3中这俩的写法是一样，因为所有的类默认都会继承object类，全部都是新式类。


# 如果在python2中这样定义，则称其为：经典类
class Foo:
    pass 
# 如果在python2中这样定义，则称其为：新式类
class Foo(object):
    pass 

class Base(object):
    pass
class Bar(Base):
    pass
```

强制访问私有成员

```python
# 强制访问私有成员

class Foo:
    def __init__(self,name):
        self.__x = name


obj = Foo('alex')

print(obj._Foo__x) # 强制访问私有实例变量
```

### 0.1.9 嵌套

- 函数：参数可以是任意类型。
- 字典：对象和类都可以做字典的key和value

```python
class School(object):
    def __init__(self,title,addr):
        self.title = title
        self.address = addr
        
class ClassRoom(object):
    
    def __init__(self,name,school_object):
        self.name = name
        self.school = school_object
        
s1 = School('北京','沙河')
s2 = School('上海','浦东')
s3 = School('深圳','南山')

c1 = ClassRoom('全栈21期',s1)
c1.name
c1.school.title
c1.school.address
# ############################################
v = [11,22,33,{'name':'山海','addr':'浦东'}]

v[0]
v[3]['name']
```

- 继承的查找关系

```python
class StarkConfig(object):
    pass

class AdminSite(object):
    def __init__(self):
        self.data_list = []
        
    def register(self,arg):
        self.data_list.append(arg)
        
site = AdminSite()

obj = StarkConfig()
site.register(obj)
```

```python
class StarkConfig(object):
    def __init__(self,name,age):
        self.name = name
        self.age = age

class AdminSite(object):
    def __init__(self):
        self.data_list = []
        self.sk = None

    def set_sk(self,arg):
        self.sk = arg
        
        
site = AdminSite() # data_list = []  sk = StarkConfig
site.set_sk(StarkConfig)
site.sk('alex',19)
```

```python
class StackConfig(object):
    pass

class Foo(object):
    pass

class Base(object):
    pass

class AdminSite(object):
    def __init__(self):
        self._register = {}

    def registry(self,key,arg):
        self._register[key] = arg

site = AdminSite()
site.registry(1,StackConfig)
site.registry(2,StackConfig)
site.registry(3,StackConfig)
site.registry(4,Foo)
site.registry(5,Base)

for k,v in site._register.items():
    print(k,v() )
```

```python
class StackConfig(object):
    pass

class UserConfig(StackConfig):
    pass


class AdminSite(object):
    def __init__(self):
        self._register = {}

    def registry(self,key,arg=StackConfig):
        self._register[key] = arg

    def run(self):
        for key,value in self._register.items():
            obj = value()
            print(key,obj)
site = AdminSite()
site.registry(1)
site.registry(2,StackConfig)
site.registry(3,UserConfig)
site.run()
```

```python
class StackConfig(object):
    list_display = '李邵奇'

class UserConfig(StackConfig):
    list_display = '利奇航'


class AdminSite(object):
    def __init__(self):
        self._register = {}

    def registry(self,key,arg=StackConfig):
        self._register[key] = arg

    def run(self):
        for key,value in self._register.items():
            obj = value()
            print(key,obj.list_display)
site = AdminSite()
site.registry(1)
site.registry(2,StackConfig)
site.registry(3,UserConfig)
site.run()
```

```python
class StackConfig(object):
    list_display = '李邵奇'
    
    def changelist_view(self):
        print(self.list_display)
        
class UserConfig(StackConfig):
    list_display = '利奇航'

class AdminSite(object):
    def __init__(self):
        self._register = {}

    def registry(self,key,arg=StackConfig):
        self._register[key] = arg

    def run(self):
        for key,value in self._register.items():
            obj = value()
            obj.changelist_view()
site = AdminSite()
site.registry(1)
site.registry(2,StackConfig)
site.registry(3,UserConfig)
site.run()
```

### 0.1.10 特殊成员

#### 0.1.10.1 ’‘’ __ init __ ‘’‘初始化方法

```python
class Foo:
    """
    类是干啥的。。。。
    """
    def __init__(self,a1):
        """
        初始化方法
        :param a1: 
        """
        self.a1 = a1
        
obj = Foo('alex')
```

#### 0.1.10.2 '' __ new __  ''构造方法

' __ new__ '方法创建实例，并在init之前工作。

```python
class Foo(object):
    def __init__(self):
        """
        用于给对象中赋值，初始化方法
        """
        self.x = 123
    def __new__(cls, *args, **kwargs):
        """
        用于创建空对象，构造方法
        :param args: 
        :param kwargs: 
        :return: 
        """
        return object.__new__(cls)

obj = Foo()
```

#### 0.1.10.3 ’‘ __ call __'' 

```python
class Foo(object):
    def __call__(self, *args, **kwargs):
        print('执行call方法')

# obj = Foo()
# obj()
Foo()()
```

```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-
from wsgiref.simple_server import make_server

def func(environ,start_response):
    start_response("200 OK", [('Content-Type', 'text/plain; charset=utf-8')])
    return ['你好'.encode("utf-8")  ]

class Foo(object):

    def __call__(self, environ,start_response):
        start_response("200 OK", [('Content-Type', 'text/html; charset=utf-8')])
        return ['你<h1 style="color:red;">不好</h1>'.encode("utf-8")]


# 作用：写一个网站，用户只要来方法，就自动找到第三个参数并执行。
server = make_server('127.0.0.1', 8000, Foo())
server.serve_forever()
```

7.10.4   ’‘ __ getitem__  __ setitem __   __ delitem __ ''

```python
class Foo(object):

    def __setitem__(self, key, value):
        pass

    def __getitem__(self, item):
        return item + 'uuu'

    def __delitem__(self, key):
        pass


obj1 = Foo()
obj1['k1'] = 123  # 内部会自动调用 __setitem__方法
val = obj1['xxx']  # 内部会自动调用 __getitem__方法
print(val)
del obj1['ttt']  # 内部会自动调用 __delitem__ 方法
```

#### 0.1.10.4 '' __ str __''打印

```python
class Foo(object):
    def __str__(self):
        """
        只有在打印对象时，会自动化调用此方法，并将其返回值在页面显示出来
        :return: 
        """
        return 'asdfasudfasdfsad'

obj = Foo()
print(obj)
```

```python
class User(object):
    def __init__(self,name,email):
        self.name = name
        self.email = email
    def __str__(self):
        return "%s %s" %(self.name,self.email,)
user_list = [User('二狗','2g@qq.com'),User('二蛋','2d@qq.com'),User('狗蛋','xx@qq.com')]
for item in user_list:
    print(item)
```

#### 0.1.10.5 ’‘__ dict __''

```python
class Foo(object):
    def __init__(self,name,age,email):
        self.name = name
        self.age = age
        self.email = email

obj = Foo('alex',19,'xxxx@qq.com')
print(obj)
print(obj.name)
print(obj.age)
print(obj.email)
val = obj.__dict__ # 去对象中找到所有变量并将其转换为字典
print(val)
```

#### 0.1.10.6 上下文管理【面试题】

```python
class Foo(object):
    def __enter__(self):
        self.x = open('a.txt',mode='a',encoding='utf-8')
        return self.x
    def __exit__(self, exc_type, exc_val, exc_tb):
        self.x.close()

with Foo() as ff:
    ff.write('alex')
    ff.write('alex')
    ff.write('alex')
    ff.write('alex')
```

```python
# class Context:
#     def __enter__(self):
#         print('进入')
#         return self
#
#     def __exit__(self, exc_type, exc_val, exc_tb):
#         print('推出')
#
#     def do_something(self):
#         print('内部执行')
#
# with Context() as ctx:
#     print('内部执行')
#     ctx.do_something()


class Foo(object):
    def do_something(self):
        print('内部执行')

class Context:
    def __enter__(self):
        print('进入')
        return Foo()

    def __exit__(self, exc_type, exc_val, exc_tb):
        print('推出')

with Context() as ctx:
    print('内部执行')
    ctx.do_something()
```

7.10.8   两个对象相加

```python
val = 5 + 8
print(val)

val = "alex" + "sb"
print(val)

class Foo(object):
    def __add__(self, other):
        return 123
    
obj1 = Foo()
obj2 = Foo()
val  = obj1 + obj2
print(val)
```

特殊成员：就是为了能够快速实现执行某些方法。

### 0.1.11 内置函数补充

#### 0.1.11.1 type,查看类型

```python
class Foo:
    pass

obj = Foo()

if type(obj) == Foo:
    print('obj是Foo类的对象')
```

#### 0.1.11.2 issubclass

```python
class Base:
    pass

class Base1(Base):
    pass

class Foo(Base1):
    pass

class Bar:
    pass

print(issubclass(Bar,Base))
print(issubclass(Foo,Base))
```

#### 0.1.11.3 isinstance

```python
class Base(object):
    pass

class Foo(Base):
    pass

obj = Foo()

print(isinstance(obj,Foo))  # 判断obj是否是Foo类或其基类的实例（对象）
print(isinstance(obj,Base)) # 判断obj是否是Foo类或其基类的实例（对象）
```

#### 0.1.11.4 super

```python
class Base(object):
    def func(self):
        print('base.func')
        return 123


class Foo(Base):
    def func(self):
        v1 = super().func()
        print('foo.func',v1)

obj = Foo()
obj.func()
# super().func() 去父类中找func方法并执行
```

```python
class Bar(object):
    def func(self):
        print('bar.func')
        return 123

class Base(Bar):
    pass

class Foo(Base):
    def func(self):
        v1 = super().func()
        print('foo.func',v1)

obj = Foo()
obj.func()
# super().func() 根据类的继承关系，按照顺序挨个找func方法并执行(找到第一个就不在找了)
```

```python
class Base(object): # Base -> object
    def func(self):
        super().func()
        print('base.func')

class Bar(object):
    def func(self):
        print('bar.func')

class Foo(Base,Bar): # Foo -> Base -> Bar
    pass

obj = Foo()
obj.func()

# super().func() 根据self对象所属类的继承关系，按照顺序挨个找func方法并执行(找到第一个就不在找了)
```

## 0.2 单例模式（23种设计模式）

- 无论实例化多少次，永远用的都是第一次实例化出的对象。

```python
class Foo:
    pass

# 多例，每实例化一次就创建一个新的对象。
obj1 = Foo() # 实例，对象
obj2 = Foo() # 实例，对象
# 单例，无论实例化多少次，都用第一次创建的那个对象。
obj1 = Foo()
obj2 = Foo()
```

- 单例模式标准

```python
class Singleton(object):
    instance = None
    def __new__(cls, *args, **kwargs):
        if not cls.instance:
            cls.instance = object.__new__(cls)
        return cls.instance

obj1 = Singleton()
obj2 = Singleton()

# 不是最终，加锁。
```

- 文件连接池

```python
class FileHelper(object):
    instance = None
    def __init__(self, path):
        self.file_object = open(path,mode='r',encoding='utf-8')

    def __new__(cls, *args, **kwargs):
        if not cls.instance:
            cls.instance = object.__new__(cls)
        return cls.instance

obj1 = FileHelper('x')
obj2 = FileHelper('x')
```

- 模块导入

```python
import jd # 第一次加载：会加载一遍jd中所有的内容。
import jd # 由已经加载过，就不在加载。
print(456)
```

```python
import importlib
import jd
importlib.reload(jd)
print(456)
```

通过模块导入的特性也可以实现单例模式：

```python
# jd.py
class Foo(object):
    pass

obj = Foo()
```

```python
# app.py
import jd # 加载jd.py，加载最后会实例化一个Foo对象并赋值给obj
print(jd.obj)
```


## 0.3 异常处理

#### 0.3.1.1 基本格式

```python
try:
    pass
except Exception as e:
    pass
```

```python
try:
    v = []
    v[11111] # IndexError
except ValueError as e:
    pass
except IndexError as e:
    pass
except Exception as e:
    print(e) # e是Exception类的对象，中有一个错误信息。
```

```python
try:
    int('asdf')
except Exception as e:
    print(e) # e是Exception类的对象，中有一个错误信息。
finally:
    print('最后无论对错都会执行')
    
# #################### 特殊情况 #########################
def func():
    try:
        # v = 1
        # return 123
        int('asdf')
    except Exception as e:
        print(e) # e是Exception类的对象，中有一个错误信息。
        return 123
    finally:
        print('最后')

func()
```

#### 0.3.1.2 主动触发异常

```python
try:
    int('123')
    raise Exception('阿萨大大是阿斯蒂') # 代码中主动抛出异常
except Exception as e:
    print(e)
```

```python
def func():
    result = True
    try:
        with open('x.log',mode='r',encoding='utf-8') as f:
            data = f.read()
        if 'alex' not in data:
            raise Exception()
    except Exception as e:
        result = False
    return result
```

#### 0.3.1.3 自定义异常

```python
class MyException(Exception):
    pass

try:
    raise MyException('asdf')
except MyException as e:
    print(e)
```

```python
class MyException(Exception):
    def __init__(self,message):
        super().__init__()
        self.message = message

try:
    raise MyException('asdf')
except MyException as e:
    print(e.message)
```

### 0.3.2 约束和反射

- #### 约束（抽象类/接口类）

  - 给子类一个规范，让子类必须按照抽象类的规范来实现方法。

```python
# 约束字类中必须写send方法，如果不写，则调用时候就报抛出 NotImplementedError 
class Interface(object):
    def send(self):
        raise NotImplementedError()
        
class Message(Interface):
    def send(self):
        print('发送短信')z
        
class Email(Interface):
    def send(self):
        print('发送邮件')
```

```python
class Message(object):
    
    def msg(self):
        print('发短信')

	def email(self):
        print('邮件')
        
    def wechat(self):
        print('微信')

obj = Message()
obj.msg()
obj.email()
obj.wechat()
```

```python
class BaseMessage(object):
    def send(self,a1):
        raise NotImplementedError('字类中必须有send方法')
        
class Msg(BaseMessage):
    def send(self):
        pass

class Email(BaseMessage):
    def send(self):
        pass

class Wechat(BaseMessage):
    def send(self):
        pass

class DingDing(BaseMessage):
    def send(self):
        print('钉钉')
    
obj = Email()
obj.send()
```

- 反射

  - 通过对象来获取实例变量、绑定方法
  - 通过类来获取类变量、类方法、静态方法
  - 通过模块名来获取模块中的任意变量（普通变量、函数、类）
  - 通过本文件来获取本文件中的任意变量
    - getattr(sys.modules[name],'变量名')

根据字符串的形式去某个对象中 操作 他的成员。

- getattr(对象,"字符串")     根据字符粗的形式去某个对象中 获取 对象的成员。 

```python
class Foo(object):
    def __init__(self,name):
        self.name = name
obj = Foo('alex')

# 获取变量
v1 = getattr(obj,'name')
# 获取方法
method_name = getattr(obj,'login')
method_name()
```

- hasattr(对象,'字符串')   根据字符粗的形式去某个对象中判断是否有该成员。 

```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-
from wsgiref.simple_server import make_server

class View(object):
    def login(self):
        return '登陆'

    def logout(self):
        return '退出'

    def index(self):
        return '首页'


def func(environ,start_response):
    start_response("200 OK", [('Content-Type', 'text/plain; charset=utf-8')])
    #
    obj = View()
    # 获取用户输入的URL
    method_name = environ.get('PATH_INFO').strip('/')
    if not hasattr(obj,method_name):
        return ["sdf".encode("utf-8"),]
    response = getattr(obj,method_name)()
    return [response.encode("utf-8")  ]

# 作用：写一个网站，用户只要来访问，就自动找到第三个参数并执行。
server = make_server('192.168.12.87', 8000, func)
server.serve_forever()
```

- setattr(对象,'变量','值')   根据字符粗的形式去某个对象中设置成员。 

```python
class Foo:
    pass


obj = Foo()
obj.k1 = 999
setattr(obj,'k1',123) # obj.k1 = 123

print(obj.k1)
```

- delattr(对象,'变量')   根据字符粗的形式去某个对象中删除成员。

```python
class Foo:
    pass

obj = Foo()
obj.k1 = 999
delattr(obj,'k1')
print(obj.k1)
```

```python
class Cloud(object):

    def upload(self):
        pass
    
    def download(self):
        pass
    
    def run(self):
        # up|C:/xxx/xxx.zip
        # down|xxxx.py
        value = input('请用户输入要干什么？')
        action = value.split('|')[0]
        # 最low的形式
        if action == 'up':
            self.upload()
		elif action == 'down':
            self.download()
		else:
            print('输入错误')
		
		# 构造字典 (*)
		method_dict = {'up':self.upload, 'down':self.download}
         method = method_dict.get(action)
		method()
         
		# 反射（*）
         method = getattr(self,action) # upload  # self.upload
		method()
```

```python
class Foo(object):
    def get(self):
        pass

obj = Foo()
# if hasattr(obj,'post'): 
#     getattr(obj,'post')

v1 = getattr(obj,'get',None) # 推荐
print(v1)
```



python一切皆对象

- py文件
- 包
- 类
- 对象

python一切皆对象，所以以后想要通过字符串的形式操作其内部成员都可以通过反射的机制实现。 

模块：importlib 

```
importlibimport importlib
importlib.import_module('模块名')
os = __import__('os')
print(os.path.isdir('D:\code\day24\pack'))
print(os.path.isfile('D:\code\day24\pack'))
```

根据字符串的形式导入模块。

```python
模块 = importlib.import_module('utils.redis')
```

![1556266716326](C:\Users\xiaohui\AppData\Roaming\Typora\typora-user-images\1556266716326.png)

## 0.4 栈和队列

- 栈 Stack
  - 后进先出 last in first out
- 队列 Queue
  - 先进先出 first in first out

```python
class Stack(object):
    pass

class Queue(object):
    pass
```


## 0.5 日志（模块logging）

- 基本应用：用于统计日志、用来做故障排除debug、用来记录错误，完成代码优化。
- 日志处理本质：Logger/FileHandler/Formatter
- logging.basicconfig和logger对象的区别
  - logging.basicconfig:使用方便，但不能同时向文件和屏幕上输出。（logging.debug,logging.warning）
  - logger对象：复杂
    - 创建一个logger对象
    - 创建一个文件操作符
    - 创建一个屏幕操作符
    - 创建一个格式
    - 给logger对象绑定 文件操作符
    - 给logger对象绑定 屏幕操作符
    - 给文件操作符设定格式
    - 给屏幕操作符设定格式
    - 用logger对象来操作

```python
import logging

logger = logging.getLogger()
fh = logging.FileHandler('log.log')
sh = logging.StreamHandler()
logger.addHandler(fh)
logger.addHandler(sh)
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
fh.setFormatter(formatter)
sh.setFormatter(formatter)
logger.warning('message')
```



- 推荐处理日志方式

```python
import logging

file_handler = logging.FileHandler(filename='x1.log', mode='a', encoding='utf-8',)
logging.basicConfig(
    format='%(asctime)s - %(name)s - %(levelname)s -%(module)s:  %(message)s',
    datefmt='%Y-%m-%d %H:%M:%S %p',
    handlers=[file_handler,],
    level=logging.ERROR
)

logging.error('你好')
```

- 推荐处理日志方式+日志分割

```python
import time
import logging
from logging import handlers
# file_handler = logging.FileHandler(filename='x1.log', mode='a', encoding='utf-8',)
file_handler = handlers.TimedRotatingFileHandler(filename='x3.log', when='s', interval=5, encoding='utf-8')
logging.basicConfig(
    format='%(asctime)s - %(name)s - %(levelname)s -%(module)s:  %(message)s',
    datefmt='%Y-%m-%d %H:%M:%S %p',
    handlers=[file_handler,],
    level=logging.ERROR
)

for i in range(1,100000):
    time.sleep(1)
    logging.error(str(i))
```

注意事项：

```python
# 在应用日志时，如果想要保留异常的堆栈信息。
import logging
import requests

logging.basicConfig(
    filename='wf.log',
    format='%(asctime)s - %(name)s - %(levelname)s -%(module)s:  %(message)s',
    datefmt='%Y-%m-%d %H:%M:%S %p',
    level=logging.ERROR
)

try:
    requests.get('http://www.xxx.com')
except Exception as e:
    msg = str(e) # 调用e.__str__方法
    logging.error(msg,exc_info=True)
```

- 项目结构目录

  - 脚本

  ![1556453767003](C:\Users\xiaohui\AppData\Roaming\Typora\typora-user-images\1556453767003.png)

  - 单可执行文件

  ![1556453804687](C:\Users\xiaohui\AppData\Roaming\Typora\typora-user-images\1556453804687.png)

  - 多可执行文件

  ![1556453832951](C:\Users\xiaohui\AppData\Roaming\Typora\typora-user-images\1556453832951.png)

## 0.6 正则表达式和re模块

#### 0.6.1.1 re模块

- re模块本身只是用来操作正则表达式，但是和正则本身是没有关系的。

#### 0.6.1.2 正则表达式

- 正则表达式是一种规则，匹配字符串的规则。
- 正则表达式的应用场景：匹配字符串（电话号码、身份证号、ip地址）、表单验证（验证用户输入是否正确、银行卡号）、爬虫（从网页源码中获取一些重要信息）
- 正则规则（元字符，量词）
  - 第一条规则 ： 本身是哪一个字符，就匹配字符串中的哪一个字符
  - 第二条规则 ： 字符组[字符1字符2]，一个字符组就代表匹配一个字符，只要这个字符出现在字符组里，那么就说明这个字符能匹配上字符组中还可以使用范围所有的范围都必须遵循ascii码从下到大来指定[0-9] [a-z] [A-Z]
    - [0-9]   \d   表示所有的数字
              d  -->   d
              \d -->   \是转义符   转义符转义了d，让d能够匹配所有0-9之间的数
    - \w 表示 大小写字母  数字 下划线
    - \s 表示空白 空格 换行符 制表符
    -  \t 匹配制表符
    - \n 匹配换行符
    - \D 表示所有的非数字
    - \W 表示除 数字字母下划线之外的所有字符
    - \S 表示非空白
    - . 表示除了换行符之外的任意内容
    - [] 字符组 ：只要在中括号内的所有字符都是符合规则的字符
    - [^ ]非字符组 ：只要在中括号内的所有字符都是不符合规则的字符
          []   [^]
    - ^ 表示一个字符的开始
    - $ 表示一个字符的结束
    - | 表示或，注意，如果两个规则有重叠部分，总是长的在前面，短的在后面
    - () 表示分组，给一部分正则规定为一组，|这个符号的作用域就可以缩小了
    - [\d]  [0-9]  \d  没有区别 都是要匹配一位数字
    - [\d\D]  [\W\w]  [\S\s] 匹配所有一切字符

```
# 元字符
# \d \w \s \t(table) \n(next)
# \D \W \S
# .
# []   [^]
# ^    $
# |   ()
```

```
# 量词
# {n}  表示只能出现n次
# {n,} 表示至少出现n次
# {n,m}表示至少出现n次，至多出现m次
```

```
# ？ 表示匹配0次或1次   表示可有可无 但是有只能有一个 比如小数点
# +  表示匹配1次或多次
# *  表示匹配0次或多次  表示可有可无 但是有可以有多个 比如小数点后n位

# 匹配0次

# 匹配任意的2位整数
# 匹配任意的保留两位小数的数字
# 匹配一个整数或者小数  \d+\.\d+|\d+   \d+\.?\d*   \d+(\.\d+)?

# 默认贪婪匹配，总是会在符合量词条件的范围内尽量多匹配
    # \d{7,12}
# <html>adljdkjsljdlj</html>
# <.+>
# 非贪婪匹配 ：惰性匹配
    # 总是匹配符合条件范围内尽量小的字符串

# 元字符 量词 ? x
# 表示按照元字符规则在量词范围内匹配，一旦遇到x就停止

# .*?x  匹配任意的内容任意多次遇到x就立即停止

# 元字符
# 元字符量词
# 元字符量词？

# \d+?x   .*?x   爬虫


# 身份证号
# 15位  全数字 首位不为0
# 18位  前17位全数字 首位不为0  最后一位可能是x和数字
# [1-9](\d{14}|\d{16}(\d|x))
# [1-9](\d{16}[\dx]|\d{14})
# [1-9]\d{14}(\d{2}[\dx])?


# 元字符
# 量词
# 贪婪匹配和非贪婪

# 尝试自己学习正则模块

# 基于listdir完成计算文件夹总大小
    # 1.递归
    # 2.堆栈  递归函数-三级菜单
```







