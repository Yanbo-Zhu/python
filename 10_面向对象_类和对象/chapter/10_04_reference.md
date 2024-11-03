
- Python does not require explicit deletion of objects  
- objects simply cease to exist (are garbage collected) once they are no longer referenced by anything  
- for instance, reassigning a variable removes the reference to its previous value


# 1 How does Python know when an object is not referenced anymore?

Python keeps track of the number of references by using a **reference counter**


- garbage collection is not always instantanious
- there are some objects that are immortal, like `None` or low integers, which have very high reference counters

```python
from sys import getrefcount  # do not rely on this function, it is for educational purposes only

def func():  
    obj = DeleteMe('Amy')  
    print('After creation:', getrefcount(obj))  
    obj2 = obj  
    print('New reference:', getrefcount(obj))  
    del obj2  
    print('Remove new reference:', getrefcount(obj))  
  
func()


print(getrefcount(None))

```


# 2 What counts as a reference?

- variables  
- attributes  
- membership in any container type

```python
class A: pass  


def func():  
    obj = DeleteMe('Leo')  
    print(getrefcount(obj))  
    var_ref = obj  
    print(getrefcount(obj))  
    A.obj = obj  
    print(getrefcount(obj))  
    con = (1, 2, obj)  
    print(getrefcount(obj))  
    del A.obj  


func()


```

