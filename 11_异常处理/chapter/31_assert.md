
> Asserts will raise an exception when the evaluate to false

# 1 原理 

`assert`语句可能会引起`AssertionError`。其用法为：`assert <test>,<data>`。这等价于：
* `<test>`表达式用于计算真假，`<data>`表达式用于作为异常的参数。若`<test>`计算为假，则抛出`AssertionError`
```
if __debug__:
	if not <test>:	
	raise AssertionError(<data>)
```


  ![assert](../imgs/python_29_8.JPG)


```python
def calculate_average(numbers:list[int|float]) -> float:  
    """Calculate the average of a list of numbers."""  
    # When asserts evaluate to false they will execute the code left of the comma and will append the result to the error log.  
    # 如果 all(isinstance(num, (int, float)) for num in numbers) 是false, 则输出语句 All elements must be numbers.
    assert all(isinstance(num, (int, float)) for num in numbers), "All elements must be numbers."   
    return sum(numbers) / len(numbers)  
  
print(calculate_average([1, 2, 3]))  # 返回 2.0
print(calculate_average([1, 2, 3, 'a'])) # 返回语句 AssertionError: All elements must be numbers.
```

# 2 Assertions can be disabled (using python -O flag)

* 若执行时用命令行 `-0`标志位，则关闭`assert`功能（默认是打开的）。 `__debug__`是内置变量名。当有`-0`标志位时，它为0；否则为1

## 2.1 How it Works

When you use an `assert` statement, Python performs a check and raises an `AssertionError` if the condition is `False`. For example:

```python
def divide(a, b):
    assert b != 0, "Division by zero is not allowed"
    return a / b
```

If `b` is zero, this will raise an `AssertionError`. However, when running Python with `-O`, all `assert` statements are ignored. This can improve performance by skipping these checks.

## 2.2 Running Python with the -O Flag

To disable assertions, run the Python script with the `-O` flag like this:
```
python -O your_script.py
```

Or set the PYTHONOPTIMIZE environment variable:
```
export PYTHONOPTIMIZE=1
python your_script.py
```

## 2.3 Important Considerations

1. **Assertions Skipped**: Assertions are not executed at all when the `-O` flag is used, so any `AssertionError` that would normally be raised won’t occur.
2. **Code Reliability**: Avoid using assertions for essential error handling, as they should only be used for debugging purposes.


# 3 assert 和 raise 的比较 

Use assert when:  
* 通常`assert`用于给定约束条件，而不是用于捕捉程序的错误。  
- Checking internal assumptions in your code  
- Writing tests  
- Validating developer-controlled conditions that should never be false  
  
Use raise when:  
- Handling expected error conditions  
- Validating user input  
- Signaling problems that could occur during normal operation  
  
  
Reason:  
Assertions can be disabled (using python -O flag), while raised exceptions cannot. They are meant to catch programming errors, not expected errors.



