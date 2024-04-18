https://www.zhihu.com/question/30082392
https://blog.csdn.net/weixin_38638223/article/details/119714644
https://stackoverflow.com/questions/46319694/what-does-it-mean-to-run-library-module-as-a-script-with-the-m-option


# 1 `if __name__ == '__main__': `

在完成一个模块的编写之前，我们一般会对模块中的功能进行测试，看看各项功能是否正常运行。对于这些测试的代码，我们希望只在直接运行这个py文件的时候执行，在用其他的程序import这个模块的时候不要执行。这个时候就要借助Python内置的__name__变量。

`__name__`变量的取值是什么可以分两种情况，

1. 当一个py文件被直接运行的时候，__name__变量的值为__main__。
2. 当一个py文件被import到其他程序的时候，这个py文件里面的__name__变量的值为这个py文件的名字。

我们可以利用__name__变量的这个特点，结合一个if语句，让我们import某一个模块的时候只用到它提供的功能，而不要运行里面用来测试的代码：
Der flogende Code wird nur ausgefuehrt, wenn das Skript selbst aufgerufen wird und the file nicht durch Modul importiert wird 

```python3
if __name__ == '__main__':
    # put your code here
```



## 1.1 例子 
[https://stackoverflow.com/questions/419163/what-does-if-name-main-do](https://stackoverflow.com/questions/419163/what-does-if-name-main-do)

d1.py
![](images/Pasted%20image%2020240418164452.png)

d2.py
![](images/Pasted%20image%2020240418164501.png)

`__name__` is immer entrypoint, was ausgefuhrt ist 


1 
d1.py ausführen
![](images/Pasted%20image%2020240418164801.png)
Print(d1:1) 被执行
Import d2 被执行: D2.py 中的 print("d2:1") 被执行 , 但是 d1.py 中的 if__name__ == '__main__':  中的没有被被执行 
Print('d1:4') 被执行
![](images/Pasted%20image%2020240418164828.png)



2 
d2.py 被执行 
![](images/Pasted%20image%2020240418164849.png)
![](images/Pasted%20image%2020240418164853.png)

Print('d2:1') 被执行

`If __name__ == '__main__'` 中的也被成功执行


# 2 Python里面存在这样的关系

- 数据可以封装在容器（列表、[元组](https://www.zhihu.com/search?q=%E5%85%83%E7%BB%84&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2030353759%7D)、字符串、字典）里面；
- 代码可以封装在function里面；
- function和数据可以封装在class里面（或者说方法和属性可以封装在类里面）；
- 上述三类内容可以打包在module（模块）里面；
- 多个module可以打包在package（包）里面；
- 多个package可以打包在library（库）里面。

# 3 Module

本质上是一个python程序, 以.py 作为文件的后缀, 任何py文件都可以作为一个模块 
块，可以有效地避免命名空间的冲突，可以隐藏代码细节让我们专注于高层的逻辑，还可以将一个较大的程序分为多个文件，提升代码的可维护性和可重用性。 

## 3.1 导入

导入一个模块一般有两种方法：

```

1. import 模块名1 [as 别名1], 模块名2 [as 别名2]，…。此时，模块名1本身被导入，但保存它原有的命名空间，所以我们需要用”模块名1.成员名1“方式访问其函数或变量。

3. from 模块名 import 成员名1 [as 别名1]，成员名2 [as 别名2]，…。此时，会将该模块的函数/变量导入到当前模块的命名空间中，无须用“模块名1.成员名1"访问了。

```


其中，用 `[]` 括起来的部分，可以使用，也可以省略。

注意，模块名里面只要写py文件的名字，不需要加后缀。

另外，尽量不要使用

```python3
from demo import *
```

的方式进行导入，否则很容易出现名称重复的情况。

例如，如果有两个模块里面有相同的成员，或者你自己定义了某一个对象和demo module里面的成员（例如函数）重名了，运行的时候会出问题。因为此时我们无法确认，我们所指的是自己定义的对象还是[demo module](https://www.zhihu.com/search?q=demo%20module&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2030353759%7D)里面的成员。


## 3.2 **模块的说明文档**

模块的说明文档放在py文件的开头，用成对的三个英文[单引号](https://www.zhihu.com/search?q=%E5%8D%95%E5%BC%95%E5%8F%B7&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2030353759%7D)引起来：

```python3
'''
模块的说明文档放在这里。
'''
```

然后我们可以用模块的__doc__属性来访问模块的说明文档：
```text
import demo
print(demo.__doc__)
```

在调用这个模块来写代码的时候，也可以阅读到模块的说明文档。例如下图，我把鼠标放在导入的 [re 包](https://www.zhihu.com/search?q=re%20%E5%8C%85&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2030353759%7D)名称上面就能看到其说明文档：

![](https://picx.zhimg.com/80/v2-48d6efc6027b6ff58d66712b0f1b2262_720w.webp?source=1def8aca)

在编程中显示的说明文档的内容和原始 py 文件中的内容一样。例如，下面是 re 模块的原始 py 文件中的说明文档：

![](https://pica.zhimg.com/80/v2-fd5c25c9b137181499387d02970b7d04_720w.webp?source=1def8aca)

## 3.3 模块的路径

对于用import语句导入的模块，Python会按照下面的路径列表顺序地查找我们需要的模块：

1. 当前的工作目录；
2. PYTHONPATH（环境变量）中的每一个目录；
3. Python 默认的[安装目录](https://www.zhihu.com/search?q=%E5%AE%89%E8%A3%85%E7%9B%AE%E5%BD%95&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2030353759%7D)。

如果我们在导入自己写的模块的时候，Python[解释器](https://www.zhihu.com/search?q=%E8%A7%A3%E9%87%8A%E5%99%A8&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2030353759%7D)提示找不到这个模块

```text
ModuleNotFoundError: No module named '模块名'
```

那么，说明我们写的模块没有放在上述三类路径。由于这三类目录都保存在标准模块sys的sys.path变量中，因此我们有三种解决方法。

1.向[sys.path变量](https://www.zhihu.com/search?q=sys.path%E5%8F%98%E9%87%8F&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2030353759%7D)中临时添加[模块文件](https://www.zhihu.com/search?q=%E6%A8%A1%E5%9D%97%E6%96%87%E4%BB%B6&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2030353759%7D)所在的完整路径。

```text
import sys
sys.path.append(r'D:\xxx\yyy')
```

2.将模块移动到sys.path 变量中已包含的路径中。

3.修改path 系统的环境变量。

其中，[环境变量](https://www.zhihu.com/search?q=%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2030353759%7D)又分为用户变量（仅对当前用户生效）和系统变量（对系统里所有用户均生效）。Python在使用path变量时，会先按照系统path变量找，然后按照用户path变量的路径找。

通常情况下，设置用户path变量即可。

# 4 包（package）

在比较大型的项目中常常需要编写、用到大量的模块，此时我们可以使用包（Package）来管理这些模块。

## 4.1 什么是包

Python包，就是里面装了一个`__init__.py`文件的文件夹

__init__.py文件（前后各有 2 个下划线'_'）具有下面4个性质：

1. 它本身是一个模块；
2. 这个模块的模块名不是__init__，而是这个包的名字，也就是装着__init__.py文件的文件夹的名字。
3. 它的作用是将一个文件夹变为一个Python模块
4. 它可以不包含代码，不过此时仅仅用`import [该包]`形式是什么也做不了的。所以一般会包含一些Python初始化代码，在这个包被import的时候，这些代码会自动被执行。
5. 第4点所指的初始化代码类型一：批量导入我们需要用到的模块，这样我们就不用在用到的时候再一一导入，方便实用。
6. 第4点所指的初始化代码类型二：如果我们要使用`“from pacakge_1 import *”`的形式导入一个模块里面的所有内容，则需在__init__.py中加上`“all = [‘file_a’, ‘file_b’]”`。其中，package_1下有`file_a.py`和`file_b.py`。
7. 不建议在__init__.py中写类，以保证该py文件简单。

```
mycompany
├─ __init__.py
├─ abc.py
└─ xyz.py
```

`__all__`是Python中的一个重要的变量，放在__init__模块中，用于指定此包（package）被`import *`时，哪些模块（module）会被import进**当前`[作用域]`中。不在 `__all__`列表中的模块不会被其他程序引用。我们可以对 `__all__`进行重写。

`__path__`也是python中的一个常用变量，它是储存着当前包内的搜索路径的一个列表。默认情况下只有一个元素，即当前包（package）的路径。

**Python包具有下面3个性质：**
1. 它实质上是一个文件夹；
2. 该文件夹里面一定有__init__.py模块，其他的模块可以有也可以没有；
3. 它的本质依然是模块，因此一个包里面还可以装其他的包。

## 4.2 导入包

**导入包的方法和导入模块比较类似，只不过由于层级比一般模块多了一级，所以多了一条导入形式：**

```
1. import 包名 [.模块名 [as 别名]]
2. from 包名 import 模块名 [as 别名]
3. from 包名.模块名 import 成员名 [as 别名]

```

我们在导入包的时候，实际上是导入了它的`__init__.py`文件文件。


## 4.3 `__init__.py`

再说__init__.py的问题，在[python3.3](https://www.zhihu.com/search?q=python3.3&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2315826832%7D)之后，**[PEP-420](https://link.zhihu.com/?target=https%3A//www.python.org/dev/peps/pep-0420/)**将包(package)分为了两种，

一种是之前包含__init__.py的包，叫**regular package**。
如果不包含__init__.py，python认为这个目录是**namespace package。** 也就是说 **__init__.py不再是包(package)的必需品。** 比如我建立如下目录

```text
> tree
some_path
├── namespace_pkg     # no __init__.py, namespace package
│   └── say.py
└── regular_pkg 
    ├── __init__.py   # has __init__.py, regular package
    └── say.py

```

其用法几乎一摸一样。

```text
>>> import namespace_pkg
>>> namespace_pkg
<module 'namespace_pkg' (namespace)>
>>> import regular_pkg
>>> regular_pkg
<module 'regular_pkg' from '/some_path/regular_pkg/__init__.py'>
>>> import namespace_pkg.say
>>> namespace_pkg.say.hello()
Hello, This is Namespace Package!
>>> import regular_pkg.say
>>> regular_pkg.say.hello()
Hello, This is Regular Package!

```

虽然__init__.py不再是必需的，但是它让你有更多组织模块的机会，目前使用__init__.py还是主流。

# 5 module 和 package 的区别


 导入单个的module，一般是这样的：
```
import my_module
```
 导入package一般是这样的:
`from my_package.timing.dager.internets import function_of_love`

 可以理解为:
- module：单个的模块，一般是单个（偶尔为多个）python文件；
    - 不含有 `__init__.py`
- package：多个相关的module的组合。肯定是多个，相关的Python文件的组合；Package是用来把相关的模块组织在一起，成为一个整体的。
    - 多个关系密切的模块应该组织成一个包，以便于维护和使用。这项技术能有效避免名字空间冲突。创建一个名字为包名字的文件夹并在该文件夹下创建一个init.py文件就定义了一个包。你可以根据需要在该文件夹下存放资源文件、已编译扩展及子包。
    - 

也就是说，**模块(module)就是有[命名空间](https://www.zhihu.com/search?q=%E5%91%BD%E5%90%8D%E7%A9%BA%E9%97%B4&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2315826832%7D)的，python代码的一种组织形式。不一定是py文件，可以是.so，甚至可以是目录。** 而包(package)是一种可包含子模块或[递归](https://www.zhihu.com/search?q=%E9%80%92%E5%BD%92&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2315826832%7D)地包含子包的模块(module)。所以说**包(package)也是一种模块(module)。** 辨别到底是模块(module)还是包(package)，就看这个模块(module)是否含有__path__的属性。


• Module == Collection of stuff in foo.py file
    – functions, classes, variables, …
• Package == Directory with .py files

• Import of a module: code in the file is executed
• Import of a package: code in the __init__.py file is executed


a package is a module containing other modules (& possibly sub-packages...)
```
– __init__.py: initialization procedure and defines all variables,
functions, classes, which are / can be imported
– subpackages are subdirs with __init__.py
```




## 5.1 例子

![](images/Pasted%20image%2020240418165503.png)

`__init__.py `
![](images/Pasted%20image%2020240418165514.png)

`__main__.py `
![](images/Pasted%20image%2020240418165523.png)


----

Import demo 后, `__init__.py` 中 头一句print() 被执行了, 但是  `__init__.py` 中  def main() 没有被执行
![](images/Pasted%20image%2020240418165553.png)

Demo.main() 执行后, ` __init__.py `中 头一句 print() 没有被执行了, 但是  `__init__.py` 中  def main() 被执行 
![](images/Pasted%20image%2020240418165603.png)


----

python -m demo后 
 整个 package ausfuhren  ` __init__.py `先被自动执行 , 然后 `__main__.py `又被自动执行
![](images/Pasted%20image%2020240418165637.png)


----


若 demo 这个 package 里面包含三个 py script

Python -m demo 的被执行的时候,  kanweg.py 没有被一起执行, 因为 kannweg.py  不符合 naming konvention , 不是以__xxx__ 类型的

![](images/Pasted%20image%2020240418165652.png)


# 6 解释 python module, 以及 python -m modelname
[https://stackoverflow.com/questions/46319694/what-does-it-mean-to-run-library-module-as-a-script-with-the-m-option](https://stackoverflow.com/questions/46319694/what-does-it-mean-to-run-library-module-as-a-script-with-the-m-option)

## 6.1 Python module 的解释 

A Python module 就是 一个 包含很多 script 的 place

Python modules are just script files that are located in a place where Python can find them. As with all scripts, you can just run them directly if you know where they are, e.g. python /path/to/module.py.

Properly designed modules usually do nothing except set up stuff (e.g. functions and types you could import), but they usually won’t have any visible side effect. That’s why you can do import sys and nothing happens.

From demo import main  就是 从 demo 这个 module 中 输入 main 这个 functions

Executed directly by command line

However, some modules may offer useful stuff when they are run from the command line. Examples for that include venv but also http.server or idlelib: All of those are regular modules that can be imported from other modules without side effects.

But when executed directly, they all do things (e.g. venv sets up a virtual environment, http.server runs a simple HTTP server, and idlelib runs IDLE). This is usually done with the following check:

if__name__ == '__main__':  
    print('Module is being executed directly, so do stuff here')

if__name__ == '__main__': 还有个作用 就是 去识别  这个 script 是被直接 执行的, 还是 间接被执行的

This is a special way of recognizing of a script/module is being executed directly, or whether it’s just being imported from some other module. You can learn more about the question [“What does if __name__ == '__main__': do?”](https://stackoverflow.com/q/419163/216074).

---

例子
[https://tutswiki.com/run-module-as-script-python/](https://tutswiki.com/run-module-as-script-python/)

```
mymath.py

def int_sum(a, b):
    print a+b

if __name__ == "__main__":
    import sys
    int_sum(int(sys.argv[1]),int(sys.argv[2]))
```


Now you can run the above as:

`$ python mymath.py 1 2`
3

This works because the value of built-in`__name__` variable is set to` __main__ `if the Python code is executed directly through the interpreter. If you use the above module in a script using import then in that case the value of` __name__` is the filename of module

## 6.2 python -m modulename


So, you can run a module directly using python /path/to/module.py as we established before. But this requires you to know the full path to the module.

That’s where the -m option comes into play: For modules that can usually be imported just using import modulename, you can use python -m modulename to run that module directly. Just as if you typed the full path to it.

So for our above examples, we can just use python -m venv, python -m http.server. or python -m idlelib.

1
Other cool examle is json.tool for pretty-printing from the shell. echo '{"1":"a","2":"b"}' | python -m json.tool

2
If it's a 'package'(a directory rather than a single .py file), python -m modulename works slightly different than python /path/to/module.
The former executes both __init__.py and __main__.py, but the latter executes only __main__.py

==python -m modulename: executes both` __init__.py` and` __main__.py`==
==Python /path/tomodule :  executes only `__main__.py`==

3

Say for example you have folder structure like this

|-HelloModule  
  |_ __init__.py  
  |_ hellomodule.py

To run the hellomodule.py as a module means the command will be:

python -m HelloModule.hellomodule


4
rufen main function  (`If __name__== '__main__': ` 存在 )

python kannweg24.py, 不报错 
python -m kannweg24 , 不报错 
写为 python -m kannweg24.py， 无法运行

![](images/Pasted%20image%2020240418165956.png)


# 7 库(library)和框架(framework)


**库(library)其实主要用来表示可重复利用的代码**。别人写好了，拿过来白嫖一下，我自己也可以写个自定义的库(library)。不管是复杂还是简单，只要是一个可重复使用的代码，都可以称为库(library)。比如大家常用的re,json,numpy，scipy、NLTK、jieba等。

![](images/v2-747bbcc76070e493903d8a4f1a7cf52d_720w.webp)

上面的模式中，是**你调用库(library)来写程序，整体的流程，结构，标准都是你说了算。**

**而框架(framework)，则反过来，是框架(framework)在"调用"你**。整体的流程，结构和标准你一般是不会改的，你所做的都是依赖于框架，在上面添砖加瓦。比如Django，Flask, scrapy


## 7.1 Python中的module和library之间的区别

 对于library和module，说白了，都是提供了一定的功能供别人调用。从这方面来说，也可以理解为：
 Python中的library等价于module；
 只不过Python中很少说library，正常情况下都说module。

 所以，简而言之:

    library多数都是指的是C，C#等语言中的库，库文件；Python中很少用library这个词。
    Python中的“库”称为“module”——模块。

