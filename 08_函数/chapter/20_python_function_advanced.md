
# 1 Functions as First-Class Objects  
  
- in Python, functions are objects that can be:  
- passed as arguments  
- returned from other functions   
- assigned to variables  
- stored in data structures


```python
def apply_twice(func, value):  
    """Apply a function twice to a value."""  
    return func(func(value))  
  
def add_one(x):  
    return x + 1  
  
result = apply_twice(add_one, 10)  
print(f"After applying add_one twice to 10: {result}")
```

# 2 Closures

- when defining a function in another function, the inner function can access the outer functions variables

```python
def make_greeter(greeting):
    """Creates a function that greets with a specific greeting"""
    def greet(name):
        return f"{greeting}, {name}!"
    return greet

# Create different greeting functions
say_hello = make_greeter("Hello")
say_aloha = make_greeter("Aloha")

print(say_hello("Alice"))  # "Hello, Alice!"
print(say_aloha("Bob"))    # "Aloha, Bob!"
```

we can even modify the outer function's variables:

```python
def create_counter():  
    count = 0  # This variable is "enclosed" in the closure  
    def increment():  
        nonlocal count  # Need nonlocal to modify enclosed variable  
        count += 1  
        return count  
          
    return increment  # Return the inner function  
  
counter = create_counter()  
print(counter())  # 1  
print(counter())  # 2  
print(counter())  # 3  
  
# ATTENTION:  
# While this is sometimes useful, it is also considered bad practice when following the functional programming paradigm.
```

# 3 Decorators  
  
- decorators are functions that modify other functions (or classes)  
- they can be applied using the special `@` syntax  
- commonly used for:  
  - logging  
  - timing  
  - input validation  
  - access control

```python
def log_calls(func):
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__} with args={args}, kwargs={kwargs}")
        result = func(*args, **kwargs)
        print(f"{func.__name__} returned {result}")
        return result
    return wrapper

@log_calls
def multiply(a, b):
    return a * b

print(multiply(3, 4))
```


In Python, defining a function as `def wrapper(*args, **kwargs):` creates a function that can accept any number of positional (`*args`) and keyword (`**kwargs`) arguments. Here's what each part does:

1. **`*args`**: This allows the function to accept any number of positional arguments. Inside the function, `args` is a tuple containing all the positional arguments passed.
    
2. **`**kwargs`**: This allows the function to accept any number of keyword arguments. Inside the function, `kwargs` is a dictionary containing all the keyword arguments passed.
    

A common use for this type of function is when writing **decorators**. The `wrapper` function can take the same arguments as the original function it wraps, allowing it to process arguments before passing them to the original function.

Here’s an example of a simple decorator using `wrapper`:
```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Before the function call")
        result = func(*args, **kwargs)   # 这句话 就是执行 say_hello 的 
        print("After the function call")
        return result
    return wrapper

@my_decorator
def say_hello(name):
    print(f"Hello, {name}!")

say_hello("Alice")

```


Explanation:
- `wrapper` receives `name` as an argument through `*args`.
- It executes some code before and after calling `say_hello`, adding behavior to the original function without modifying it directly.

In this way, wrapper helps add functionality around a function call by handling a flexible set of arguments.
```
Before the function call
Hello, Alice!
After the function call

```

---
中文

- 装饰器：在不改变原函数内部代码的基础上，在函数执行之前和之后自动执行某个功能。（他们是修改其他函数的功能的函数。有助于让我们的代码更pythonic（python范儿））

- 应用场景：想要为函数扩展功能时，可以选择用装饰器。
- 装饰器编写格式(双层嵌套)：

```python
def 外层函数（参数）:
    def 内层参数(*args,**kwargs):
        return 参数(*args,**kwargs)
    return 内层函数
```

传参时候加`*args，**kwargs`由于每次传参时候参数格式不同，减少定义函数的繁琐。

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



## 3.1 练习题

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


# 4 partical function 

- `partial` creates a new function with some arguments fixed  
- equivalent to writing a closure, but much shorter  
- equivalent to writing a lambda function but arguably more readable  
- import from `functools` module


```python
from functools import partial

def power(base, exponent):
    return base ** exponent

# Create specialized functions
square = partial(power, exponent=2)
cube = partial(power, exponent=3)

# equivalent to
square = lambda x: power(x, 2)
cube = lambda x: power(x, 3)

print(f"Square of 4: {square(4)}")
print(f"Cube of 4: {cube(4)}")

# 输出 
Square of 4: 16
Cube of 4: 64
```
# 5 函数的高级特性
1.在Python中，函数的递归通常比`for`循环要慢而且空间消耗大，但是递归的优点是可以遍历任意形状的结构。

2.Python函数是对象，自身存储在内存块中，它可以自由地传递与引用。

* 函数对象支持一个特殊操作：有括号`()`以及参数列表执行调用行为
* 我们可以通用地检查函数对象的某些属性：如`.__name__`属性、`.__code__`属性
* 可以向函数对象附加任意的用户自定义属性，如`func.count=0`。这样的属性可以用来直接将状态信息附加到函数对象上
* Python3中，可以给函数对象附加注解。注解不作任何事情，而且注解是可选的，它被附加在函数对象的`.__annotaions__`属性中。注解的格式为：

  ```
  def func(a:'a',b:(1,10),c:float) -> int:
	return a+b+c  
  ```
	* 注解分两种：参数注解紧随形参名字的冒号`:`之后；返回值注解紧随参数列表的`->`之后
	* 当出现注解时，Python将它们收集到字典中并附加到`.__annotations__`属性中
	* 注解可以与默认值同时出现，此时形参形式为`c:float=4.0`
	* 注解只有在`def`中有效，在`lambda`表达式中无效
	
  ![函数对象](../imgs/python_20_1.JPG)



6.Python是静态检测局部变量的：

  ```
  x='global'
  def func():
	print(x)
	x=3
  ```
编译时，Python看到了赋值语句`x=3`，因此决定了在函数内的任何地方，`x`都是本地变量。但是`print(x)`时赋值语句并未发生，此时即使全局中有全局的`x`，也会报错。

* 任何在函数体内的赋值、`import`，嵌套`def`，嵌套类等都受这种行为影响
  >即只要有局部变量的定义，无论在函数内哪个地方，其作用域都是本局部作用域全域

  ![局部作用域的全域效果](../imgs/python_20_3.JPG)

7.Python在内部会将每个默认实参保存成对应的对象，附加在这个函数本身。在不同的函数调用期间，这些默认实参会保存同一个对象。因此对于可变对象作为默认实参注意保持警惕。  
 ![可变的默认实参](../imgs/python_20_4.JPG)



