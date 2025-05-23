

1 
`globals()`
print 出所有的 globals 的variable 

2 
For-loops leak their variables
```
def check_for_leak():
    i = 40
    for i in range(25):
        pass
    print(i)
check_for_leak() 

输出为 24 
```

# 1 Inplace operations on global variables



会报错, 会引用不了在global variable 
```python
from traceback import print_exception

temperature = 21

def heat_up():
    temperature += 1

try:
    heat_up()
except UnboundLocalError as error:
    print_exception(error)
```




to make inplace operations possible, we can explicitly indicate that we refere to a **global** variable
```python
from traceback import print_exception

temperature = 21

def heat_up():
    global temperature  # 如果不加这个 global , 就引用不了 之前 定义的 temperature = 21
    temperature += 1
    print(locals()) # will remain empty

heat_up()
print(f'{temperature}°C?! Is it getting hot in here?')
```



# 2 Local operations on non-local variables

- variables local to a higher block are subject to the same limitations
    - 会报错, 会引用不了 在同一个 functiion 中 不同 scope 的 variable 
```python
def simulate_temperature():  
    temperature = 21  
  
    def local_heat_up():  
        temperature += 1  
  
    try:  
        local_heat_up()  
    except UnboundLocalError as error:  
        print_exception(error)  
  
simulate_temperature()
```


- we can indicate that we refer to a variable that is not local to the current block by using `nonlocal`
    - 这样就能引用了
```python
def simulate_temperature():
    temperature = 21

    def local_heat_up():
        nonlocal temperature
        temperature += 1

    local_heat_up()
    print(f'{temperature}°C?! Is it getting hot in here?')

simulate_temperature()
print(f'Outside is still {temperature}°C!')
```

# 3 作用域
1.代码中变量名被赋值的位置决定了这个变量名的作用域（即可见范围）。因为变量是在首次赋值的时候定义的。

* Python将一个变量名首次被赋值的地点关联为一个特定的命名空间

2.变量可以在3个不同的地方定义，对应三种不同的作用域：

* `def`内赋值定义的变量：作用域为本函数
	>这里的赋值包括显式`=`赋值和隐式赋值。隐式赋值包括
	>
	>*  `import`语句隐式赋值
	>*  `def`函数定义来隐式赋值（函数名这个变量）
	>*  形参匹配来隐式赋值
* 嵌套的`def`中赋值定义的变量：对于父函数来说，该变量不是本地的
* `def`之外赋值，作用域为整个文件全局的  
![三种作用域](../imgs/python_18_1.JPG)

3.作用域法则：

* 每个模块文件就是一个全局作用域。从外面看，模块的全局变量就成为该模块对象的属性；从内部看，模块的全局变量就是普通的、作用域为全局的变量
* 全局作用域的范围仅限于变量所在的单个文件
* 每次调用函数，都创建一个新的局部作用域
* 默认情况下，所有函数定义内部的变量都是局部变量
	* `global`语句声明会将变量名作用域提升至全局
	* `nonlocal`语句声明会将变量名作用域提升至外层的`def`
* Python预定义的`_builtin_`模块提供了一些预定义的内置变量  
![作用域法则](../imgs/python_18_2.JPG)

4.交互式运行的代码实际上位于`__main__`的内置模块中
5.变量名查找规则：`LGBE`

* 首先查找本地作用域`L`
* 接着查找上一层`def`或`lambda`的本地作用域`E`
* 接着查找全局作用域`G`
* 最后查找内置作用域`B`

如果均未找到变量名则报错。  
当前面作用域的变量名覆盖内置的作用域名字时，可以手动`import builtins`模块，在用`builtins.name`来直接使用这个变量名。注意不要随意修改`builtins`模块内变量的值。

```
a=1
b=2
def func():
	global a,b,c #一个名字或逗号分隔的多个名字，这些变量名被提升到全局作用域内
	a=2
	b=0
	c=0 #虽然c没有在def外定义，但这里的global 和 c=0会在全局作用域内定义c
```
  ![global用法](../imgs/python_18_3.JPG)

7.要在局部作用域中修改全局变量，方法有以下几种：

* global声明
* 通过`import modname`然后利用`modname.attr`来访问
* 通过`import sys`然后利用`sys.modules['modname'].attr`来访问  
  ![global用法](../imgs/python_18_4.JPG)

8.作用域示例：

```
x='global_x'          #全局作用域
def f1():             
  x='f1_x'            #f1的局部作用域
  z='f1_z'            #f1的局部作用域
  def f2():
	global y      #全局作用域
	y='f2_y'
	print('in f2',x) #LGBE法则，找到的是f1局部作用域中的x
	nonlocal z    #f2的nonlocal作用域，是f1的局部作用域
   	z='f2_z'
	t='f2_t'      #f2的本地作用域
  f2()
```
  ![作用域示例](../imgs/python_18_5.JPG)

9.嵌套的函数返回后也是有效的。

```
def f1():
  x=99
  def f2():
      print(x)
  return f2 # f2是个局部变量，仅在f1执行期间因为新建了局部作用域所以才存在。
action=f1() #f2指向的函数对象，由于action引用它，因此不会被收回。
#但是f2这个位于局部作用域中的变量名被销毁了
action() #此时f1执行结束，但是f2记住了在f1嵌套作用域中的x。这种行为叫闭包
```  
>类比闭包在语义上更明确，因为类可以明确定义自己的状态

  ![闭包](../imgs/python_18_6.JPG)

10.在函数内部调用一个未定义的函数是可行的，只要在函数调用是，该未定义函数已定义即可。  
  ![调用未定义函数](../imgs/python_18_7.JPG)

11.嵌套作用域中的变量在嵌套的函数调用时才进行查找，而不是定义时。 、

```
def func():
	acts=[]
	for i in range(5):
		acts.append(lambda x:i**x) #添加匿名函数对象
	return acts
acts=func()
acts[0](2) #调用时才开始查找i,此时i最后被记住的值是4
``` 
  ![嵌套作用域中变量名查找](../imgs/python_18_8.JPG)

要解决这个这个陷阱，可以用默认参数：

```
def func():
	acts=[]
	for i in range(5):
		acts.append(lambda x,i=i:i**x) #每次循环，形参i的默认实参均不同
	return acts
acts=func()
acts[0](2) 
``` 

12.`nonlocal`是Python3中引入的。

```
def func():
  a=0
  b=1
  def func1():
	nonlocal a,b#限定了查找只能在func1所在的作用域（即func的本地作用域），且要求名字a,b已经存在。
	a='a' #对a,b的赋值会影响到func中的a,b
```

* 如果没有`nonlocal`，则在`func1`中的赋值会创建本地变量，而无法修改`func`中的局部变量
* `global`使得作用域查找先从全局作用域开始，跳过了局部作用域以及`nonlocal`作用域。
* Python在函数创建的时候解析`nonlocal`，而不是在函数调用时，因此要求`nonlocal`的名字已经存在

13.全局变量、`nonlocal`变量、类、函数属性都提供了状态保持能力

14.`global`、`nonlocal`只是修改了变量作用域（即作用域提升），但是并未给出变量定义   
![global|nonlocal不是定义](../imgs/python_18_9.JPG)
