
https://blog.csdn.net/qq_37555071/article/details/107581812

pdb:  python debugger 
目前在[jupyter](https://so.csdn.net/so/search?q=jupyter&spm=1001.2101.3001.7020)中还没有可视化调试界面，而python pdb是代码调试的一个不错的选择，它支持设置断点和单步调试，使用起来非常方便
在使用PDB调试的时候，当我们运行程序的时候会出现一个`命令的窗口`，通过输入命令来实现在notebook中对python的代码进行调试


# 1 xx

- jupyter notebooks allow us to directly debug when an exceptions causes the program to halt, which can be enabled by calling `%pdb on`

```
%pdb on
```


# 2 常见的使用案例 

- here we see the call stack again, with a text input below  
- try entering `u` or `d` followed by hitting `Enter` in the text input to go up or down the call stack respectively  
- try printing variables using `p <variable-name>`, you can only access ones that are accessible in the current frame  
- exit the debugger with `q`

## 2.1 Manually setting breakpoints

- to investigate bugs that do not crash the program, we can manually set breakpoints within pdb using `b`  
- the `%debug` magic command is used to manually attach the debugger to a code line  
- try adding a breakpoint inside the `searchsorted` function by writing `b searchsorted`  
- try also adding a breakpoint by filename and line number by entering `b insert-fixed.py:13`  
- run the code by entering `c`, this will continue until the first breakpoint  
- we can step over lines with `n` and into lines with `s`  
- we can disable and reenable breakpoints with `disable <bpnumber>` and `enable <bpnumber>`, or remove them with `clear <bpnumber>`; use `b` to list all breakpoints


- a very powerful tool of breakpoints are conditions, which will only pause execution when an associated Python expression evaluates to `True`  
- try setting a conditional breakpoint in the loop using `b insert-fixed.py:13, i==2`, which will only halt when `i` in that line is equal to 2  
- condition expressions are executed every time the line is visited, which we can leverage for more advanced debugging  
- for instance, we may use a `print` expression, which will never pause execution as its return value `None` evaluates to `False`; however, it will be evaluated every time its breakpoint location is visited  
- try changing the condition of the breakpoint (list by `b`) using `condition <bpnumber> print(f'{i}: {elem} vs.  {compared}; {result}')`, 
or by using a new breakpoint   `b insert-fixed.py, print(f'{i}: {elem} vs. {compared}; {result}')`



# 3 命令 


 here is a short, non-exhaustive overview over some of the commands we used  
  
| command | description |  
| - | - |  
| `w[here]` | prints the trackback, and indicates with an arrow on which frame we currently are |  
| `u[p]` | go up one frame in the traceback |  
| `d[own]` | go down one frame in the traceback |  
| `c[ontinue]` | resumes execution of the program, e.g., after hitting a breakpoint |  
| `n[ext]` | proceeds to the next line |  
| `s[tep]` | steps into the next function |  
| `l[ist]` | prints the current line and context |  
| `p <expression>` | evaluate and print a Python expression in the current context |  
| `pp <expression>` | does the same as `p`, but the result is pretty-printed |  
| `b[reak] [([filename:]lineno \| function) [, condition]]` | sets a breakpoint, with an optional condition, which when evaluating to `True`, will trigger the breakpoint |  
| `disable <bpnumber>` | removes one or more breakpoints |  
| `help` | lists the available commands, and details when providing it with a command name |  
| `q[uit]` | exits PDB |

ENTER (重复上次命令)
c (继续)
l (查找当前位于哪里)
s (进入子程序,如果当前有一个函数调用，那么 s 会进入被调用的函数体)
n(ext) 让程序运行下一行，如果当前语句有一个函数调用，用 n 是不会进入被调用的函数体中的
r (运行直到子程序结束)
!<python 命令>
h (帮助)
a(rgs) 打印当前函数的参数
j(ump) 让程序跳转到指定的行数
l(ist) 可以列出当前将要运行的代码块
p(rint) 最有用的命令之一，打印某个变量
q(uit) 退出调试
r(eturn) 继续执行，直到函数体返回


参数	说明	实例
h	help 帮助文档	h b： 查看 b 命令的文档
b	break 打断点	b：查看所有断点
b 5： 给第5行打断点
b function_name：当前文件名为 function_name 的函数打断点
b test1.A.add：在 import test1 文件的 A 类的 add 方法打断点
b A.add：在 A 类的 add 方法打断点
tbreak	设置临时断点，运行完毕后会删除这个断点	设置方法和 b 一样
w	where 查看当前执行的位置	w
cl	clear 清除断点	cl：清除所有断点
cl 2：清除断点列表中编号为2断点
cl test.py:18：清除 test.py 文件编号为18断点
cl test1:18：清除 import test1 文件编号为18的断点
condition	给断点设置条件	condition 1` i==4`：当断点列表中编号为1的断点中变量 i 等于 4 的时候执行断点
s	step 执行下一条命令，遇到函数则进入	参考下面执行效果
n	next 执行下一条语句，遇到函数不进入	参考下面执行效果
c	continue 继续执行，直到遇到下一条断点	参考下面执行效果
r	return 执行当前运行函数到结束	参考下面执行效果
args	args 打印当前函数的所有参数及参数值	参考下面执行效果
p	print 打印出当前所在函数中的变量或表达式结果	p a：打印变量a
p dir(a)：打印变量a所有属性
pp	格式化打印出来的结果	pp a：格式化打印变量a
run	重新执行	
q	quit 退出pdb调试	


参数	说明	实例
l	list 列出当前或范围周围代码	l 5, 20： 列出5到20行代码
l： 查看当前位置的代码
disable	停用断点	disable：清除所有断点
disable 2：清除断点列表中编号为2断点
disable test.py:18：清除 test.py 文件编号为18断点
disable test1:18：清除 import test1 文件编号为18的断点
enable	启动断点	用法和disable一样
ignore bpnumber	忽略某个断点几次	ignore 1 3：忽略断点列表中第1个断点3次，一般循环中用，
commands	给断点写一个脚本执行	commands 1：给断点编号为1的的断点写脚本
unt	until 执行到下一行	参考下面 unt 执行效果
j	jump 跳转至指定程序行，如果是前行，则忽略中间行代码。
如果是后退，状态重设为回退行状态	注意：是跳转到不是执行
alias	自定义一个函数，参数可由％1，％2来表示。
类似 Python 的 lambda	
unalias	删掉别名函数	unalias name





# 4 在python 设置 pdb断点 

```python

import pdb   # 注意看这里 
import sys

def add(num1=0, num2=0):
    return int(num1) + int(num2)
    
def sub(num1=0, num2=0):
    return int(num1) - int(num2)
    
def main():
    num1 = 28
    num2 = 8
    pdb.set_trace() #添加断点 要写上这一句 
    addition = add(num1, num2)
    print (addition)
    subtraction = sub(num1, num2)
    print (subtraction)
    
if __name__ == '__main__':
    main()
```


# 5 效果图 

在运行cell中的代码之后，会出现一个下面的命令窗口  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/71acc42e61708e9a0abe6bb072986f0c.png)  


在`ipdb`的输入框中输入字母`n`然后`回车`运行，程序会跳到下一行不会进行到调用函数的内部，如果想要子函数内部进行调试可以在子函数内部添加`set_trace`来实现  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/9196f6b3bba258490a3ccd986a917cd3.png)




# 6 Debugging with `breakpoint()` and Jupyter's graphical debugger

- another approach to run the debugger is calling `breakpoint()` inside the code, which when run in the terminal, will execute pdb  
- inside jupyter notebooks, `breakpoint()` will trigger the graphical debugger instead  
- jupyter notebook will **ignore** `breakpoint()` unless the **debugger** is enabled (bug-button on the top right) 
    - ![](images/Pasted%20image%2020241110174519.png)
- with the jupyter graphical debugger, breakpoints can be alternatively set by clicking left of the line number


```python
def compute(offset, vector):  
    result = []  
    for elem in vector:  
        result.append((elem - offset) ** 2)  
    breakpoint()  
    return sum(result)  
  
compute(1, [1., 2., 3., 4.])
```





