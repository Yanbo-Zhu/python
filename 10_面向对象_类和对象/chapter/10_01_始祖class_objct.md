
 `object`  
- Objects have data attributes (a state) and procedural attributes (methods: how to work with the state)  
- The most basic object in Python is `object`

# 1 List attributes of `object`
```
dir(object)


['__class__',
 '__delattr__',
 '__dir__',
 '__doc__',
 '__eq__',
 '__format__',
 '__ge__',
 '__getattribute__',
 '__getstate__',
 '__gt__',
 '__hash__',
 '__init__',
 '__init_subclass__',
 '__le__',
 '__lt__',
```


# 2 attribute opeartrion

`getattr` get the definition description of attribute 
 `setattr` sets attribute, 
 `delattr` deletes attribute, 
 `hasattr` checks for existence  
 
```python
We now print attribute names (using `dir`) and values (using `getattr`). 
`slot wrapper` are wrappers around C code that are exposed to the Python layer:

for v in dir(object)[::3]:  
    print(f'{v}:\n{getattr(object, v)}\n')  
# `setattr` sets attribute, `delattr` deletes attribute, `hasattr` checks for existence  
# [::3] is a slice: it takes every third element of the list


```

output 
```
__init_subclass__:
<built-in method __init_subclass__ of type object at 0x00007FFE4F719710>

__ne__:
<slot wrapper '__ne__' of 'object' objects>

__reduce_ex__:
<method '__reduce_ex__' of 'object' objects>

__sizeof__:
<method '__sizeof__' of 'object' objects>
```


