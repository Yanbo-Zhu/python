

• & (and)
• | (or)
• ^ (xor)
• ~ (2-complement)
• <<,>> (binary shift)


# 1 Walrus Operator :=

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
