


# 1 字符串
1.Python的字符串是一种不可变序列，它包含的字符存在从左到右的位置顺序。  
string is immutable   不可变是指：字符串创建以后无法修改它的内容。

```python
msg = 'hello'
msg[1], msg[::-1], 'hi' + 'lo', 'ya' * 3, len('house')
('e', 'olleh', 'hilo', 'yayaya', 5)

msg[2] = 'e'
会报错
TypeError: 'str' object does not support item assignment


```


> 序列包括：字符串、列表、元组




* 字符串由一对双引号或者单引号包围，二者无任何区别
> 如果希望字符串中包含引号，则有两种办法：
>
>* 最外围的引号和字符串中的引号使用不同的格式。如`"who's name is Tex?"`
>* 采用转义字符。如`who\'s name is Tex?'`
* 空字符串是一对引号之间不包含内容：`""`
* Python自动在任意的表达式中合并相邻的字符串常量
* 在字符串中反斜杠代表转义序列，每个转义序列代表一个字符（不一定能够打印出来）：
	* `\\`转义反斜杠本身
	* `\n`为换行符
	* `\0`为`\0x00`（不是字符串结尾）
	* `\xhh`为十六进制值
	* `\o00`为八进制值
	* `\uhhhh`为16位Unicode的十六进制值
	* `\Uhhhhhhhh`为32位Unicode的十六进制值
* Python中`\0`并不去结束一个字符串，Python会在内存中保持整个字符串的长度和文本
* Python会以十六进制显示非打印的字符
* 若无合法的转义编码识别`\`以及之后的字符，则Python会在最终的字符串中保留`\`

![字符串](../imgs/python_4_1.JPG)

2.raw 字符串是一种特殊的字符串。当`r`出现在字符串起始引号之前时，为 raw 字符串。这种字符串会关闭转义机制。  
raw 字符串不能以`\`结尾。  
![raw字符串](../imgs/python_4_2.JPG) 

3.字符串块：以三重引号包围的字符串（引号为一对单引号或者一对双引号均可）。  
三重引号之间的文本会被收集到一个单独的多行字符串中，并且将换行以`\n`代替。


'single' vs "double" vs '''triple''' or """double triple"""
• subtypes
– common: 'common string'
– raw: r"raw string"
– Bytes: b'\xce\xb5\xcf\x85\xcf\x84\xcf\x85\xcf\x87\xce\xaf\xce\xb1'
• b.decode('utf-8')

# 2 String Operation 

4.字符串可以有以下操作：

* 加：两个字符串相加，返回一个新的字符串
* 乘：字符串与整数`N`相乘，返回一个新的字符串，该字符串是原字符串重复`N`次
* `len()`：返回字符串长度
* 迭代：字符串对象是一个可迭代对象

![字符串操作](../imgs/python_4_3.JPG)

"hello"+"world" "helloworld" # concatenation
"hello"*3 "hellohellohello" # repetition
`"hello"[0] "h" # indexing`
`"hello"[1:4] "ell" # slicing`


len("hello") 5 # size
"hello" < "jello" True # comparison
"e" in "hello" True # search

# 3 String Slices 

5.字符串支持索引，其中`S[i]`获取的是偏移为`i`处的字符（偏移`i`从0开始，
  小于等于`len(S)-1`）。  
>若偏移`i`大于`len(S)-1`则Python会抛出`IndexError`异常，
>提示`string index out of range`

你也可以提供一个负的偏移，其中`-1`为最后一个字符，`-n`为`len(S)-n`处的字符。  
![字符串索引](../imgs/python_4_4.JPG)

6.字符串支持分片，语法为`S[m:n]`，它返回从`m`开始到`n`（不包含`n`）的一个新字符串。

* 未给出上界时，该分片默认上界为`len(S)`
* 未给出下界时，该分片默认下界为 0
* 如果是`S[:]`，则返回字符串`S`的一个全新拷贝

如果增加步进参数，则语法为`S[m:n:k]`，它返回从`m`开始到`n`（不包含`n`）且每隔`k`个元素选取一次的一个全新字符串，默认`k`为 1。

* 若`k`为正数则从左到右步进；若`k`为负数，则从右向左步进
* `S[::-1]`返回S的翻转字符串
* 负步进时，默认的上下界极限有所不同。
	* 上界极限可以为空或者为`len(S)`或者为`len(S)-1`
	* 下界极限必须为空，否则 0 号元素会被排除掉

![字符串分片](../imgs/python_4_5.JPG)

# 4 String conversion

7.可以通过`str()`函数与`repr()`函数将数字转成字符串。

* `str()`函数的效果类似`print()`的效果
* `repr()`函数产生的结果可以由解释器解释。`eval(repr(x))`会返回`x`。

![str()与repr()](../imgs/python_4_6.JPG)

8.可以在单个字符与它对应的 ASCII 码值之间转换：

* `ord(char)`：返回单个字符的 ASCII 值
* `chr(ascii_int)`： 返回 ASCII 值对应的字符

![字符与ASCII值之间转换](../imgs/python_4_7.JPG)

9.字符串是不可变序列，因此不能原地修改一个字符串，只能够生成新的字符串并赋值给原变量。  
![字符串不可原地修改](../imgs/python_4_8.JPG)


# 5 String format expression 

## 5.1 基于C语言的printf格式化表达式

10.字符串格式化表达式是基于C语言的printf格式化表达式。其格式为：
`"%d %s apples" % (3,'bad')`
它返回一个新的字符串。

* 占位符有多种：  
 `%s`：字符串； `%r`：也是字符串，但用`repr()`得到的而不是`str()`；  
  `%c`：字符； `%d`：十进制整数； `%i`：整数； `%e`：浮点指数；  
  `%f`： 浮点十进制；`%%`：百分号 `%`， `%g`：自动转成浮点`%e`或者`%f`  
  ![字符串格式化占位符](../imgs/python_4_9.JPG)

* 转换通用目标结构为：`%[(key_name)][flags][width][.precision]type`
	* `key_name`：用于从右边字典中取对应键的值（此时右边的是字典对象，而不是元组）
	  如：`"%(n)%d %(x)%s" %{"n":3,"x":"apples"}` 
	* `flags`：如果为`-`则左对齐；如果为`+`则为正负号；如果为`0`：则补零
	* `width`： 指定位宽（包括小数点在内），至少为`width`字符宽度
	* `precision`：指定小数点后几位
		>`width`和`precision`可以为`*`，表示它们从输入的下一项中取值
		（即从元组中取得）
	* `type`为类型，如`d`,`r`,`f`,`e`等  
  	![字符串格式化表达式通用目标结构](../imgs/python_4_10.JPG)



12.格式化单个值比较简单，可以有以下方法：
* `"%s" % 1.23`
* `"%s" % (1.23,)`，这里`(1.23,)`是一个单元素元组，
  而`(1.23)`是一个表达式
* `"{0}".format(1.23)`

13.由于Python内部会暂存并重复使用短字符串来进行优化，因此该短字符串在内存中只有一份。  
![字符串暂存优化](../imgs/python_4_14.JPG)

14.浮点数格式化时，采用`%s`说明符与`%f`说明符，其结果不同：  
![浮点数格式化](../imgs/python_4_15.JPG)

因为按照`%f`格式化输出时，浮点数有精度和位宽的设定（虽然这里没有显式指定，但是它们有默认值）。而`%s`格式化输出时，首先调用了`str()`函数，然后再进行输出。


## 5.2 `.format()`
11.格式化字符串除了使用字符串格式化表达式之外，还可以通过字符串的`.format()`
  方法达到同样的效果。

* `.format()`方法支持位置参数、关键字参数、以及二者的混合。
	* 位置参数： `"{0},{1},{2}".format('abc','def','ghi')`
	* 关键字参数：`"{k1},{k2},{k3}".format(k1='abc',k2='def',k3='ghi')`
	* 混合使用：`"{0},{1},{k}".format('abc','def',k='ghi')`  
  ![.format参数类型](../imgs/python_4_11.JPG)
* 格式化字符串中可以指定对象的属性、字典键、序列的索引：
	* 指定字典的键：`"{0[a]}".format({'a':'value'})`，
	  <font color='red'>注意这里的键`a`并没有引号包围</font>
	* 指定对象的属性：`"{0.platform}".format(sys)`，也可以用关键字参数：
	  `"{obj.platform}".format(obj=sys)`
	* 指定序列的索引：`"{0[2]}".format("abcd")` ，这里只能进行正索引值，且不能分片 
  	![.format参数类型](../imgs/python_4_12.JPG)
* 通用目标结构为： `{fieldname!conversionflag:formatspec}`
	* `fieldname`为位置数字 0,1,2,... 或者为关键字，它后面可选地跟随
		* `.name`：则指定对象的属性
		* `[index]`：指定了索引
		* `[key]`：指定了字典的键
	* `conversionflag`为转换标记，可以为：
		* `r`：在该值上调用一次`repr()`函数
		* `s`：在该值上调用一次`str()`函数
		* `a`：在该值上调用一次`ascii()`函数
	* `formatspec`为格式，其结构为：
	   `[[fill] align] [sign] [#] [0] [width] [.precision] [type]`
		* `fill`一般与`align`为`=`时配合
		* `align`为对齐：
			* `<`：左对齐
			* `>`：右对齐
			* `=`：必须指定`fill`（单个字符），此时用这个字符填充
			* `^`：居中对齐
		* `sign`：为正负号标记
		* `#`：作用未知
		* `0`：补0
		* `width`：位宽
		* `.precision`：精度
		* `type`：为类型，如`d`,`r`,`f`,`e`等，
		  但与格式化字符串表达式相比，多了`b`（二进制格式输出）  
    	![.format通用目标结构](../imgs/python_4_13.JPG)
	* 某些值可以从`.format()`的参数中获取，如`"{0:+0{1}d}".format(128,8)`，
	  其指定精度信息从`format()`的参数中取(参数8)


```python
print('Hello {}, you reached {} of {}
points'.format('Thomas', 87, 100))

print('Hello {fname:s}, you reached {yp:d} of {tp:7}
points'.format(fname='Thomas',yp=87,tp=100))

template = 'Today is {}, {}{} of {}'  
print(template.format('Tuesday', 2 * 8 + 1, 'th', 'October'))  
print(template.format('Monday', 2, 'nd', 'November'))  
print('The weight of %d %s is approximately %.1f g' % (3, 'Apples', 85 * 3))
```


## 5.3 f-strings 

```python
day = 17
suffix = 'th'
day_of_week = 'Monday'
month = 'October'

f'Today is {day_of_week} {day}{suffix} of {month}'

name = 'Jack'
age = 11
f'{name} is {age} years old.'

f'Result: {3 ** 0.5:0.3f}' # operation inside + 3 digits after the floating point
f'Value:{15:05d}', f'Value:{15:5d}' # 5 digits long output filled with zeros/empty string

```

```python
# second string  
a = "irony"  
b = "anyone"  
c = "room"  
  
string2 = f"The {a} of the situation wasn't lost on {b} in the {c}."  
  
# third string  
string3 = f"{7*10} * {9/3} with three digits after the floating point looks like this: {70*3 :.3f}."
```




# 6 String Method


`s = ' Thomas.Preuss@TH-Brandenburg.de '`
s.find('s')
s.find('s', 3)
t = s.split('.')
u = '.'.join(t) # !!!
s.split('.', 1)
s.strip().startswith('Tho')
s.center(100)
s.ljust(100, '*')
`s.isalpha()`
`' and '.join(['Huey', 'Dewey', 'Louie'])  # joining a list of strings using a delimiter`



# 7 print and input 

print():
• Separator (' ')
• End of line ('\n')
• File (sys.stdout)

x=y=54
f=open("fruitsfile.txt", "w")
print("hahhdf", "ee", x, y, sep='*', end="!\n", file=f)


• input:
– input(prompt): returns string trims trailing \n
– int(input(prompt)): to casts to int, etc.

• output:
– print(string_1, … string_n, sep='*')
– default separator == ' '


