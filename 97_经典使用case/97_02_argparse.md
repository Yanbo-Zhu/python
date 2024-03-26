
https://docs.python.org/zh-cn/3/howto/argparse.html#id1

https://docs.python.org/zh-cn/3/library/argparse.html

https://realpython.com/command-line-interfaces-python-argparse/
写的非常好 

import argparse


# 1 `parser = argparse.ArgumentParser()`


1 usage
在用法消息中可以使用 %(prog)s 格式说明符来填入程序名称。
![](images/Pasted%20image%2020240326201951.png)



2 description
parser = argparse.ArgumentParser(description="calculate X to the power of Y")



3 epilog
一些程序喜欢在 description 参数后显示额外的对程序的描述。这种文字能够通过给 ArgumentParser:: 提供 epilog= 参数而被指定
和 description 参数一样，epilog= text 在默认情况下会换行，但是这种行为能够被调整通过提供 formatter_class 参数给 ArgumentParse.
![](images/Pasted%20image%2020240326202017.png)


4 formatter_class
ArgumentParser 对象允许通过指定备用格式化类来自定义帮助格式。目前，有四种这样的类。

class argparse.RawDescriptionHelpFormatter
class argparse.RawTextHelpFormatter
class argparse.ArgumentDefaultsHelpFormatter
class argparse.MetavarTypeHelpFormatter

formatter_class=xx。 
Xx 只能使用一个 

如何使用两个 需要自己写代码 见
https://python-forum.io/thread-28707.html
Looking into arpgarse's code, we see that ArgumentDefaultsHelpFormatter overrides a single method _get_help_string() and RawDescriptionHelpFormatter overrides only _fill_text(). It may depend on the python version, but I think you could try this

class MyFormatter(ArgumentDefaultsHelpFormatter, RawDescriptionHelpFormatter):
    pass
 
...formater_class=MyFormatter...



# 2 parser.add_argument()

add_argument() 该方法用于指定程序能够接受哪些命令行选项

1 Positional arguments 	 
parser.add_argument("echo", help="echo the string you use here")
1 写成 "--echo" 就是 optional arguments 

2 Optional arguments 	
parser.add_argument("--verbosity", help="increase output verbosity")

不添加这一选项时程序没有提示任何错误而退出，表明这一选项确实是可选的。注意，如果一个可选参数没有被使用时，相关变量被赋值为 None，在此例中是 args.verbosity，这也就是为什么它在 if 语句中被当作逻辑假。
如果你不添加 --verbosity 标志，则args.verbosity 的值会是 None。

3 短选项 和 常选项 共存	
parser.add_argument("-v", "--verbose", help="increase output verbosity", action="store_true")
则 使用 -v, 或者 --verbose 都可以 


4 Positional arguments  和 Optional  arguments  写入的顺序无关紧要 	

$ python3 prog.py 4 --verbose
the square of 4 equals 16
$ python3 prog.py --verbose 4
the square of 4 equals 16

4 的位置 为一个 positional arguments 
--verbose 为一个 optional arguments 

## 2.1 add_argument() 中的参量 

## 2.2 help 
parser.add_argument("echo", help="echo the string you use here")
echo 这个 option 对应的 解释 是 help = 的内容 

## 2.3 type
arser.add_argument("square", help="display a square of a given number", type=int)  
规定 这个 arguemnt 的输入被视为 整数

## 2.4 choices
我们可以通过限制 --verbosity 选项可以接受的值
parser.add_argument("-v", "--verbosity", type=int, choices=[0, 1, 2], help="increase output verbosity")


## 2.5 default

parser.add_argument("-v", "--verbosity", action="count", default=0, help="increase output verbosity")

我们刚刚引入了又一个新的关键字 default。我们把它设置为 0 来让它可以与其他整数值相互比较。
记住，默认情况下如果一个可选参数没有被指定，它的值会是 None，并且它不能和整数值相比较（所以产生了 TypeError 异常）。

## 2.6 Action 

 1 action="store_true"  ， store_false， store_const

'store_true' and 'store_false' - 这些是 'store_const' 分别用作存储 True 和 False 值的特殊用例。另外，它们的默认值分别为 False 和 True。

```
parser.add_argument("--verbose", help="increase output verbosity", action="store_true")
args = parser.parse_args()
if args.verbose:
    print("verbosity turned on")

执行python3 prog.py --verbose （这时候 args.verbose =  True ）
```


解释：
现在，这一选项更多地是一个标志，而非需要接受一个值的什么东西。 （一个 option 有 action="store_true"， 使用的它的时候， 后面就不需要跟着输入值了 ）
当你为其指定一个值时，它会报错，符合作为标志的真正的精神。

我们甚至改变了选项的名字来符合这一思路。注意我们现在指定了一个新的关键词 action，并赋值为 "store_true"。这意味着，当这一选项存在时，为 args.verbose 赋值为 True。没有指定时则隐含地赋值为 False。

2 action="count"
可以通过 -v,-vv, 
--verbosity,  --verbosity --verbosity
来决定 args.verbosity的值

parser.add_argument("-v", "--verbosity", action="count", help="increase output verbosity")
args = parser.parse_args()
answer = args.square**2
if args.verbosity == 2:
    print(f"the square of {args.square} equals {answer}")
elif args.verbosity == 1:
    print(f"{args.square}^2 == {answer}")
else:
    print(answer)


$ python3 prog.py 4 -v
4^2 == 16
$ python3 prog.py 4 -vv
the square of 4 equals 16
$ python3 prog.py 4 --verbosity --verbosity
the square of 4 equals 16

## 2.7 required

通常，argparse 模块会认为 -f 和 --bar 等旗标是指明 可选的 参数，它们总是可以在命令行中被忽略。 要让一个选项成为 必需的，则可以将 True 作为 required= 关键字参数传给 add_argument():
parser.add_argument('--foo', required=True)


## 2.8 metavar

请注意 metavar 仅改变 显示的 名称 - parse_args() 对象的属性名称仍然会由 dest 值确定

当 ArgumentParser 生成帮助消息时，它需要用某种方式来引用每个预期的参数。 
默认情况下，ArgumentParser 对象使用 dest 值作为每个对象的 "name"。 
默认情况下，对于位置参数动作，dest 值将被直接使用，
而对于可选参数动作，dest 值将被转为大写形式。 
因此，一个位置参数 dest='bar' 的引用形式将为 bar。 一个带有单独命令行参数的可选参数 --foo 的引用形式将为 FOO。 示例如下:

可以使用 metavar 来指定一个替代名称:
```
>>> parser.add_argument('--foo', metavar='YYY')
>>> parser.add_argument('bar', metavar='XXX')
```


nargs 
不同的 nargs 值可能导致 metavar 被多次使用。 提供一个元组给 metavar 即为每个参数指定不同的显示信息:

```
>>> parser = argparse.ArgumentParser(prog='PROG')
>>> parser.add_argument('-x', nargs=2)
>>> parser.add_argument('--foo', nargs=2, metavar=('bar', 'baz'))
>>> parser.print_help()
usage: PROG [-h] [-x X X] [--foo bar baz]
```

options:
 -h, --help     show this help message and exit
 -x X X
 --foo bar baz
 
## 2.9 Dest

args = parser.parse_args()
 args.verbosity  就是 dest 的值 


大多数 ArgumentParser 动作会添加一些值作为 parse_args() 所返回对象的一个属性。 
该属性的名称由 add_argument() 的 dest 关键字参数确定。 

位置参数动作
对于位置参数动作，dest 通常会作为 add_argument() 的第一个参数提供:
>>> parser = argparse.ArgumentParser()
>>> parser.add_argument('bar')
>>> parser.parse_args(['XXX'])
Namespace(bar='XXX')

可选参数动作
对于可选参数动作，dest 的值通常取自选项字符串。 
ArgumentParser 会通过接受第一个长选项字符串并去掉开头的 -- 字符串来生成 dest 的值。
 如果没有提供长选项字符串，则 dest 将通过接受第一个短选项字符串并去掉开头的 - 字符来获得。 
任何内部的 - 字符都将被转换为 _ 字符以确保字符串是有效的属性名称。 下面的例子显示了这种行为:
>>> parser = argparse.ArgumentParser()
>>> parser.add_argument('-f', '--foo-bar', '--foo')
>>> parser.add_argument('-x', '-y')
>>> parser.parse_args('-f 1 -x 2'.split())
Namespace(foo_bar='1', x='2')
>>> parser.parse_args('--foo 1 -y 2'.split())
Namespace(foo_bar='1', x='2')

要引用的时候， 必须只能使用 args.foo_bar

dest 允许提供自定义属性名称:
>>> parser = argparse.ArgumentParser()
>>> parser.add_argument('--foo', dest='bar')
>>> parser.parse_args('--foo XXX'.split())
Namespace(bar='XXX')

要引用的时候， 必须只能使用 args.bar

# 3 其他

1 参数组¶	
ArgumentParser.add_argument_group(title=None, description=None)

2 互斥	
ArgumentParser.add_mutually_exclusive_group(required=False)	
group = parser.add_mutually_exclusive_group()

让我们再介绍第三个方法 add_mutually_exclusive_group()。 它允许我们指定彼此相互冲突的选项。 让我们再更改程序的其余部分以便使用新功能更有意义：我们将引入 --quiet 选项，它将与 --verbose 正好相反:

group = parser.add_mutually_exclusive_group()	
group.add_argument("-v", "--verbose", action="store_true")
group.add_argument("-q", "--quiet", action="store_true")

$ python3 prog.py 4 2 -vq
usage: prog.py [-h] [-v | -q] x y
prog.py: error: argument -q/--quiet: not allowed with argument -v/--verbose
$ python3 prog.py 4 2 -v --quiet
usage: prog.py [-h] [-v | -q] x y
prog.py: error: argument -q/--quiet: not allowed with argument -v/--verbose


add_mutually_exclusive_group() 方法也接受一个 required 参数，表示在互斥组中至少有一个参数是需要的:
group = parser.add_mutually_exclusive_group(required=True)

# 4 args = parser.parse_args()

The parse_args() method actually returns some data from the options specified, in this case, echo.
之后 可以通过 arg.echo 调用这个变量 

比如说 
args = parser.parse_args()
print(args.echo)

这一变量是 argparse 免费施放的某种 “魔法”（即是说，不需要指定哪个变量是存储哪个值的）。
你也可以注意到，这一名称与传递给方法的字符串参数一致，都是 echo。

