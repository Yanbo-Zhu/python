
# 1 安装位置  Pycharm  这个 IDE

```
e:\PyCharm Community Edition 2020.3.3\
d:\App_IDE\JetBrains\PyCharm Community Edition 2022.2.3\

```

# 2 安装步骤

![](images/Pasted%20image%2020240326195359.png)
Pycharm 这个 ide 是 32 bit 还是 64bit

![](images/Pasted%20image%2020240326195409.png)


# 3 pycharm 配置 

# 4 光标的宽度 

https://www.jetbrains.com/guide/go/tips/terminal-cursor-shape/
![[04_IDE/images/Pasted image 20240625162636.png]]

## 4.1 Interpreters


0

![](images/Pasted%20image%2020240326195737.png)

![](images/Pasted%20image%2020240326195745.png)

![](images/Pasted%20image%2020240326195750.png)

出现下图：
1处即上边提到的"独立环境"
2处是系统中的环境
3处是放解释器的位置，如果提示非空的话就在项目中新建一个文件夹就ok了
4处是选择解释器。解释器的位置在哪，往下看。

![](images/Pasted%20image%2020240326195758.png)


1 Der erste Schritt nach dem Öffnen ist das Konfigurieren des genutzten Interpreters.

PyCharm wird im Normalfall den systemweiten Python-Interpreter nutzen wollen, wovon aus oben beschriebenen Gründen abgeraten wird. 
Stattdessen werden virtuelle Umgebungen einfach von PyCharm unterstützt.

Unter "File → Project: ... → Project Interpreter" lässt sich der Python-Interpreter konfigurieren. 
Das Zahnradsymbol gefolgt von "Add" fügt einen neuen Interpreter in die PyCharm-Datenbank ein. 

poetry-Projekt
Arbeitet man mit einem poetry-Projekt, kann über poetry install eine vorkonfigurierte Umgebung erzeugt werden. Dieses sollte von PyCharm automatisch gefunden und über "Existing Interpreter" hinzugefügt werden können. 

keine Option zum Interpreter: 
Falls dies keine Option ist, bietet PyCharm auch die Möglichkeit, aus der IDE heraus direkt eine Umgebung zu erzeugen. 
Das Installieren der erforderlichen Abhängigkeiten muss dann aber manuell geschehen.

![](images/Pasted%20image%2020240326195545.png)


2 Nachdem ein Interpreter festgelegt wurde, muss, um ein Skript auszufüren, eine "Konfiguration" definiert werden.
Diese enthält neben dem Pfad zu dem Startskript weitere Informationen wie zusätliche Kommandozeilenargumente. 

Die Liste der Konfigurationen kann in PyCharm in der Ecke oben rechts im Fenster gefunden werden. 
Eine neue Konfiguration kann ueber "Edit Configurations..." in dem Auswahlfeld angelegt werden. 
Ein Rechtsklick auf eine .py-Datei zeigt auch die Option "Run XYZ.py" an, was die entsprechende Konfiguration automatisch erstellt.

![](images/Pasted%20image%2020240326195540.png)

# 4 Editor

<<<<<<< Updated upstream
<<<<<<< Updated upstream
<<<<<<< Updated upstream

## 4.1 autocompletion

如何关闭 

1 
line completion 
关闭 enable automatic compoletion on typing 这个选项
![](images/Pasted%20image%2020240828165346.png)
\

2 
code completion 
关闭 show suggestions as you type 选项 

![](images/Pasted%20image%2020240828170500.png)

||||||| Stash base
# 4 Display Language 
=======
>>>>>>> Stashed changes
||||||| Stash base
# 4 Display Language 
=======
>>>>>>> Stashed changes
||||||| Stash base
# 4 Display Language 
=======
>>>>>>> Stashed changes
# 5 Display Language 

IntelliJ 本身只支持 英语 显示 

要汉化的话 需要 去 plugin 区  下载个插件
https://blog.csdn.net/sinat_26811377/article/details/106182672

下面是 text editor 中属于的 单词字符的纠错 
https://www.jetbrains.com/help/pycharm/proofreading.html
并不可以 使得 IDE 汉化 

![](images/Pasted%20image%2020240326195701.png)


# 6 pycharm中设置新的 terminal 

![[04_IDE/images/Pasted image 20240625162148.png]]



