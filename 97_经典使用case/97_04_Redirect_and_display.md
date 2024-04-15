
 redirect the output to console as well as to a text file as well simultaneously


# 1 Only redirect 到 file  ，不显示在 screen

sys.stdout	
log = open("myprog.log", "a")
sys.stdout = log // 把 sys.stdout 指向log, 不指向 terminal 的输出显示输出了 （screen stdout ）

```
>>> print("Hello")  // 会把 hello 输出到 sys.stdout,  然后 sys.stdout 直接叔叔到 log, 输出 到 myprog.log
>>> # nothing is printed because it goes to the log file instead.

```


print 	
```
# 2 If you're using python 2.x, uncomment the next line
#from __future__ import print_function
print = log.info  // pinrt 的输出 指向 log.info， 不指向 screen stdout 了 

>>> print("Hello!")
>>> # nothing is printed because log.info is called instead of print
>>> 
```


contextlib.redirect_stdout()	

contextlib 模块通常与 with 语句一起使用。
contextlib.redirect_stdout() 函数通过设置上下文管理器帮助将 sys.stdout 临时重定向到某个文件。

```
import contextlib
 
file_path = 'randomfile.txt'
with open(file_path, "w") as o:
    with contextlib.redirect_stdout(o):
        print("This text will be added to the file")

```


# 2 both print to the standard output and append to a log file
https://stackoverflow.com/questions/11124093/redirect-python-print-output-to-logger/11124247

```

# Uncomment the line below for python 2.x
#from __future__ import print_function

import logging

logging.basicConfig(level=logging.INFO, format='%(message)s')
logger = logging.getLogger()
logger.addHandler(logging.FileHandler('test.log', 'a'))
print = logger.info

print('yo!')

---- 例子2
importlogging, sys
logging.basicConfig(filename='path/to/logfile', level=logging.DEBUG)
logger = logging.getLogger()
sys.stderr.write = logger.error
sys.stdout.write = logger.info

Aus <https://stackoverflow.com/questions/11124093/redirect-python-print-output-to-logger/11124247> 

---例子3
import os
import sys
import logging
import logging.handlers

log = logging.getLogger(__name_)

handler = logging.FileHandler("spam.log")
formatter = logging.Formatter("%(asctime)s - %(name)s - %(levelname)s - %(message)s")
handler.setFormatter(formatter)
log.addHandler(handler)
sys.stderr.write = log.error 
sys.stdout.write = log.info 


```


# 3 sys.stdout

Sys.stdout 中 本身就有 method: write, flush，  buffer， read 等等
我们可以自己写代码， 覆盖  原有的 Sys.stdout 中 本身就有 method: write, flush，  buffer， read. 
从而达到   redirect the output to console as well as to a text file as well simultaneously

```
Aus <https://stackoverflow.com/questions/15535240/how-to-write-to-stdout-and-to-log-file-simultaneously-with-popen> 

#!/usr/bin/env python3importos
importsubprocess
importsys
withsubprocess.Popen(sys.argv[1:], stdout=subprocess.PIPE, stderr=subprocess.STDOUT) asproc, \
        open('logfile.txt', 'bw') aslogfile:
    whileTrue:
        byte = proc.stdout.read(1)
        ifbyte:
            sys.stdout.buffer.write(byte)
            sys.stdout.flush()
            logfile.write(byte)
            # logfile.flush()else:
            breakexit_status = proc.returncode


logfile = open('logfile', 'w')
proc=subprocess.Popen(['cat', 'file'], stdout=subprocess.PIPE, stderr=subprocess.STDOUT)
forline inproc.stdout:
    sys.stdout.write(line)
    logfile.write(line)
proc.wait()
```

# 4 Tee

[https://stackoverflow.com/questions/616645/how-to-duplicate-sys-stdout-to-a-log-file](https://stackoverflow.com/questions/616645/how-to-duplicate-sys-stdout-to-a-log-file)
![](../96_脚本书写/images/Pasted%20image%2020240326203727.png)

[https://stackoverflow.com/questions/616645/how-to-duplicate-sys-stdout-to-a-log-file#comment110441870_651718](https://stackoverflow.com/questions/616645/how-to-duplicate-sys-stdout-to-a-log-file#comment110441870_651718)
![](../96_脚本书写/images/Pasted%20image%2020240326203743.png)


 
 
 <https://stackoverflow.com/questions/616645/how-to-duplicate-sys-stdout-to-a-log-file> 
```
importsubprocess, os, sys
tee = subprocess.Popen(["tee", "log.txt"], stdin=subprocess.PIPE)
# Cause tee's stdin to get a copy of our stdin/stdout (as well as that# of any child processes we spawn)os.dup2(tee.stdin.fileno(), sys.stdout.fileno())
os.dup2(tee.stdin.fileno(), sys.stderr.fileno())
# The flush flag is needed to guarantee these lines are written before# the two spawned /bin/ls processes emit any outputprint("\nstdout", flush=True)
print("stderr", file=sys.stderr, flush=True)
# These child processes' stdin/stdout are os.spawnve("P_WAIT", "/bin/ls", ["/bin/ls"], {})
os.execve("/bin/ls", ["/bin/ls"], os.environ)

```



# 5 自己创造一个class

https://stackoverflow.com/questions/14906764/how-to-redirect-stdout-to-both-file-and-console-with-scripting


Logger 
![](../96_脚本书写/images/Pasted%20image%2020240326203821.png)

unbufferd
![](../96_脚本书写/images/Pasted%20image%2020240326203833.png)

StreamToLogger
https://stackoverflow.com/a/36296215



