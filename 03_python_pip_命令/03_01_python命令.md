
```
# # Starten des interaktiven Python-Interpreters.
python

# 查 python 版本 
python --version

```


# 1 Py -0p
列出一共 install 多少 version / bit version 的 python 
![](image/Pasted%20image%2020240326190653.png)

![](image/Pasted%20image%2020240326190823.png)

# 2 Ausfuehren eines Python-Skripts

Ausfuehren eines Python-Skripts per python 

```
Windows:
python f:\python\test.py

Linux:
./test.py

Set comment in every script:
#!/usr/bin/python
```

Ausfuehren eines Python-Skripts per py
```
py instead of python as the command.: 
This avoids you having to put the current Python installation into PATH yourself. 
That way, you can easily have multiple Python installations  (不同的 python version ) side-by-side without them interfering with each other.

You can also specify a version: 
Python3: py -3.7 or py -3.8 
Python2 也可以使用 python lancher: py -2 script.py

Can specifiy a bit version: 
Py -3.9-64  
Py -3.9-32
```


# 3 Python.exe Command line 解释

Options and agruments 
https://docs.python.org/3/using/cmdline.html

-d
It provides debug output.

-O
It generates optimized bytecode (resulting in .pyo files).

-S
Do not run import site to look for Python paths on startup.

-v
verbose output (detailed trace on import statements).

-X
disable class-based built-in exceptions (just use strings); obsolete starting with version 1.6.

-c cmd
run Python script sent in as cmd string

file
run Python script from given file



# 4 Python2 和 Python3 使用哪个


Python2 和 Python3 都已经安装好了的时候， 输入 python hello.py , 如何知道 用的 那个 version  

3 种方法
1 using the py command (py-launcher) in python 3, 
2  virtual environment or 
3 configuring your default python system path. 

## 4.1 Using py Command line 

```
py -3 hello.py
py -2 hello.py

写成 python3 hello.py 是无效的 

也可以指明 bit verssion (Can specifiy a bit version:) 
Py -3.9-64  
Py -3.9-32

```

## 4.2 configuring your default python system path. 

如果只输入 py hello.py， 如何判定使用的是 python2  还是 3 

因为python.exe 在  `c:\Users\yzh\AppData\Local\Programs\Python\Python310-32\` 中  ( `c:\Users\yzh\AppData\Local\Programs\Python\Python310-32\python.exe`)

	• py hello.py by itself will choose the latest Python installed, 
	• or consult PATH 
		○  (如果 c:\Users\yzh\AppData\Local\Programs\Python\Python310-32 写入 PATH 中了， Python 3.3 comes with PyLauncher "py.exe", installs it in the path )
		○ 如果 两个 python version 对应的 路径 都写入 PATH 中了， 则用 位于 t
	• or consult the PY_PYTHON environment variable, e.g. set PY_PYTHON=3.6，set PY_PYTHON=3  或者 set PY_PYTHON=2

如果 PATH 中 python2 和 python3 的路径 都有呢 
In case you have both python 2 and 3 in your path, you can move up the Python27 folder in your path, so it search and executes python 2 first.


# 5 hello.py 中的内容 指明  用 python 2 还是 3 

With it, a special comment at the top of a script tells the launcher which version of Python to run:

```
#!python2
print "hello"
Or

#!python3
print("hello")

```


