


# 1 安装

python -m pip install pylint
见  https://confluence.ivu.de/pages/viewpage.action?spaceKey=MBDEV&title=Python

安装在 
`C:\Users\yzh\AppData\Local\Programs\Python\Python310-32\Scripts\pylint.exe\`

Error messages and options: 
http://docs.pylint.org/features.html#options

Pylint 配置文件 
见 [https://cloud.tencent.com/developer/article/1486578](https://cloud.tencent.com/developer/article/1486578)


# 2 使用

```

Run from DOS:

pylint --indent-string="  " --const-rgx "[a-z][a-zA-Z0-9]{1,29}|[A-Z0-9_]{2,30}$"  --variable-rgx "[a-z][a-zA-Z0-9]{1,29}|[A-Z0-9_]{2,30}$" --method-rgx "[a-z][a-zA-Z0-9]{1,29}|[A-Z0-9_]{2,30}|__[a-z]*__$" --function-rgx "[a-z][a-zA-Z0-9]{1,29}|[A-Z0-9_]{2,30}$" --max-line-length=100 <module name without extension>
or from Linux shell with ' instead of ".

PRE: 
Save files as Unix file type.

POST:
pylint detects undefined class variables (also named member variables) and undefined variables.
pylint returns errorcode.

```


# 3 pylint在项目中的使用

Pylint als externale tool
https://stackoverflow.com/questions/38134086/how-to-run-pylint-with-pycharm
https://www.jetbrains.com/help/pycharm/configuring-third-party-tools.html

Pylint as plugin 
https://github.com/leinardi/pylint-pycharm
https://cloud.tencent.com/developer/article/1486578

Pylint  在命令行中单独使用
https://www.jianshu.com/p/c0bd637f706d

## 3.1 Pylint als externale tool

![](image/Pasted%20image%2020240326193444.png)

1 Program
where pylint, 或者 which pylint 对应的地址


2 Argument
Pylint can be configured to output messages in a specific format using the msg-template option in the pylintrc file or the CLI option --msg-template.
I set it to: msg-template='{abspath}:{line}:{column}: {msg_id} {msg}'

解释
E:\Python_Pycharm\test\main.py:    1, 0: C0114 (Missing module docstring)
1 is line
0 is column 
C0114 是 msg_id
Missing module docstring 是 Msg 

(用户可根据自己的情况，选择 pylint 输出信息显示格式和要 disable 的项目)：
`--output-format=parseable --disable=R --disable=C0102,C0103,C0111,C0301,C0302,C0303,C0304,C0305,W0120,W0123,W0401,W0603,W0612,W0614,W0621,W0622,W0703,E1003,E1101 $FilePath$`


3 Output filters: 
can be set to  
in windows:   `$FILE_PATH$:\s*$LINE$\,\s*$COLUMN$:  `       
In linux or macos : `$FILE_PATH$\:$LINE$\:$COLUMN$\:.*`
so PyCharm shows links 链接 to directly jump to the reported locations. 

This can be combined with output-format=colorized so I get this:

## 3.2 Pylint as plugin 

Real-time inspection disabled by default
Preferences > Editor > Inspections > Pylint
Check "Pylint real-time scan"

![](image/Pasted%20image%2020240326193535.png)



# 4 其他

pylint 禁用某些功能的方法：
在配置文件中的   [MESSAGES CONTROL] 的 disable 添加 想禁用的功能；
如：报错如下;
![](image/Pasted%20image%2020240326193650.png)

则 在 disable尾部添加 missing-docstring 即可；
pylint在行级别的代码中 禁用某些功能（也就是 不对所有代码禁用某个检测，只对某行代码禁用某个检测）：
教程地址：https://pylint.readthedocs.io/en/latest/user_guide/message-control.html


在一行代码的 后面 添加注释，便只忽略检查某一行；
![](image/Pasted%20image%2020240326193618.png)

