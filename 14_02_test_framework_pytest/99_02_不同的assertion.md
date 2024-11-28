


```python
import unittest
import avg

class TestAvg(unittest.TestCase):
    def test_1(self):
        actual = avg.avg((1, 2, 3))
        self.assertEqual(actual, 2)
    def test_3(self):
        self.assertEqual(avg.avg((1,)), 1)
    def test_4(self):
        self.assertRaises(Exception, avg.avg, ()) # without ()
    def test_5(self):
        self.assertAlmostEqual(avg.avg((1.22222, 1.333)), 1.2777, 3)
        
if __name__ == '__main__':
    unittest.main()
```


# 1 assertEqual

```python
import unittest  
  
class TestJar(unittest.TestCase):  
      
    def test_initialization_with_default_capacity(self):  
        ### BEGIN SOLUTION  
        jar = Jar()  
        self.assertEqual(jar.get_capacity(), 12)    # 如果不jar.get_capacity(), 12 这两个不equal , 就会 make a assertion 
        self.assertEqual(jar.get_size(), 0)  
        ### END SOLUTION
```


# 2 with self.assertRaises(ValueError):

期盼 代码在执行的时候 会 raise 某个 exception.  如果 raise 了这个 exception, 则这个 test 是成功的 , 否则 这个 test failed 


verify that a particular block of code raises a specified exception, in this case, a `ValueError`. If the code within the `with` block does not raise a `ValueError`, the test will fail.


```
def test_initialization_with_invalid_capacity(self):  
    ### BEGIN SOLUTION  
    with self.assertRaises(ValueError):  
        Jar(-5)  
    with self.assertRaises(ValueError):  
        Jar("invalid")  
    ### END SOLUTION
```


## 2.1 例子 

```python
import unittest

def divide(a, b):
    if b == 0:
        raise ValueError("Cannot divide by zero")
    return a / b

class TestDivideFunction(unittest.TestCase):
    def test_divide_by_zero(self):
        with self.assertRaises(ValueError):
            divide(10, 0)  # This should raise a ValueError

    def test_divide_normal(self):
        result = divide(10, 2)
        self.assertEqual(result, 5)

if __name__ == '__main__':
    unittest.main()
```


- `with self.assertRaises(ValueError):` checks if `divide(10, 0)` raises a `ValueError`.
- If `divide(10, 0)` raises the exception as expected, the test passes.
- If it doesn’t raise `ValueError`, the test fails, signaling that the function is not handling division by zero correctly.

Using `assertRaises` is a standard way to test for exceptions in unit tests, ensuring that your code properly handles error conditions.

# 3 assertIsInstance()


```python
# Use unittest asserts  
import unittest  
  
#from pygments.lexers.jsonnet import string_rules  
  
t = unittest.TestCase()  
from pprint import pprint


t.assertIsInstance(output, str)   检查  output 是不是 str 这个 类型的变量 

```

