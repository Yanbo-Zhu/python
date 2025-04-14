

# 1 Variables
- all data in a Python program is represented by objects or by relations between objects  
- every object has an identity, a type and a value    每个变量都有一个 id, type
- assigning variables binds objects to names (similar to pointers in C/C++)


```python
x = "Hello World!"
print(id(x))
print(type(x))

y = "Hello World!"
print(id(y))
print(type(y))

z = x
print(id(z))
print(type(z))

# 结果 
1262120679856
<class 'str'>
1262120671280
<class 'str'>
1262120679856
<class 'str'>



```


# 2 Mutability  
- Python distinguishes between mutable and immutable types  
  - e.g. numeric types (`int`, `float`) and `str` are immutable, i.e. they never change their value  
  - e.g. `list` is mutable

```python
x = 1; y = x
print(x, id(x), y, id(y))
x += 1
print(x, id(x), y, id(y))

1 140708895476152 1 140708895476152
2 140708895476184 1 140708895476152



x = "Hello World"; y = x
print(x, id(x), y, id(y))
x += "!"
print(x, id(x), y, id(y))

Hello World 1262120671152 Hello World 1262120671152
Hello World! 1262121011376 Hello World 1262120671152



x = [1,2,3]; y = x
print(x, id(x), y, id(y))
x += [4]
print(x, id(x), y, id(y))

[1, 2, 3] 1262119827008 [1, 2, 3] 1262119827008
[1, 2, 3, 4] 1262119827008 [1, 2, 3, 4] 1262119827008

```




