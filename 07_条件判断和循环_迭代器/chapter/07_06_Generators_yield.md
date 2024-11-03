
Generators

* Generators are functions that return lazy iterators  
* keyword `yield` bears some similarity to `return`, but it does not terminate the function.  
  The function computation continues upon calling `next` on the function.  
* useful to define very large iterables without the need to store all data in memory

```
def counter():  
    n = 0  
    while True:  
        yield n  
        n += 1  
          
lazy_iter = counter()  
print(next(lazy_iter))  
print(next(lazy_iter))  
print(next(lazy_iter))

# 输出结果 
0
1
2
```
