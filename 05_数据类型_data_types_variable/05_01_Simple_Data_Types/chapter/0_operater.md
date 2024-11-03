

# 1 Math Operators


```  
+       -       *       **      /       //      %      @  
<<      >>      &       |       ^       ~       :=  
<       >       <=      >=      ==      !=  
```


`Powers and roots: $\quad  3^2, \> \sqrt9, \> \frac{1}{\sqrt{4}}, \> \sqrt[3]{9^2}$`
```
3 ** 2, 9 ** 0.5,  4 ** -0.5, 9 ** (2 / 3) # power of two, square root, one over square root, etc...   
```



Floor division, modulo,  bit-wise shift
10 // 3, 5 % 3, 1 << 8 # (dual 1 -> 1 00 00 00 00)

# 2 All in-place operators are

```  
+=      -=      *=      /=      //=     %=      @=  
&=      |=      ^=      >>=     <<=     **=  
```



```
result = 3
result *= 3
print(result)

message = 'hi'
message += '!'
print(message)
```





# 3 Bitwise Operater

• & (and)
• | (or)
• ^ (xor)
• ~ (2-complement)
• <<,>> (binary shift)


# 4 Walrus Operator :=

• Combination of assignment and expression
赋值, 并且做判断 

```python

1. for zahl in zahlen:
    1. if factorization(zahl):
        1. print(factorization(zahl)) # calculate twice

5. for zahl in zahlen:
    1. f = factorization(zahl) # additional line of code
    2. if f:
        1. print(f)


10.for zahl in zahlen:
    1. if f := factorization(zahl): # walrus operator
        1. print(f)

```


# 5 Comparison Operators

```python
2 == 2, 2 == 4, 2 != 4, 2 >= 4, 3 <= 3, 43 < 3457
(True, False, True, False, True, True)


"hello" == "world", "hello ".strip() == "hello"
(False, True)

```


 the `is` operator checks for identity
```python
[1] == [1], [1] is [1]
(True, False)

x = 1; y = x
x is y
True
```







