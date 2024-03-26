
# 1 auto-py-to-exe


https://confluence.ivu.de/display/MBDEV/GIT+Tooling 

You might want to use your own python installation for this.
	python -m pip install auto-py-to-exe    # use minus symbols

-----
输入命令 in console
auto-py-to-exe

	auto_py_to_exe            # use underscore# or
	python -m auto_py_to_exe  # use underscore
	
A browser windows should open:
![](image/Pasted%20image%2020240326193744.png)

Convert the script to a binary. auto-py-to-exe will create a output folder containing the binerary in the folder of the script.



# 2 cx_Freeze
(traurig) No Compiler!

Download: http://www.lfd.uci.edu/~gohlke/pythonlibs/#cx_freeze
Official download is buggy, see below: https://pypi.python.org/pypi?:action=display&name=cx_Freeze&version=4.3.3

Documentation: http://cx-freeze.readthedocs.org/en/latest/index.html

Execution (if python is installed in c:\Python34): python c:\Python34\Scripts\cxfreeze test.py --target-dir dist

Due to this error we use the alternative download page:
	File "c:\python\32-bit\3.4\lib\importlib\_bootstrap.py", line 2214, in _find_and_load
=>http://sourceforge.net/p/cx-freeze/mailman/cx-freeze-users/

![](image/Pasted%20image%2020240326193807.png)


# 3 pyinstaller

http://www.pyinstaller.org/
(Warnung) This tool requires pywin32 which itself requires Microsoft Visual Studio.


# 4 py2exe

https://pypi.python.org/pypi/py2exe/

Download py2exe-0.9.2.0.win32.exe => downloaded file is removed by virus scanner! (Warnung)
py -3.4 -m pip install py2exe
	Downloading/unpacking py2exe
	Cannot fetch index base URL https://pypi.python.org/simple/
Could not find any downloads that satisfy the requirement py2exe

