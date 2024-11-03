

1
0, 0.0, empty strings and empty containers evaluate to `False`, everything else evaluates to `True`

```python
print(bool(0), bool(0.0), bool(''), bool([]), bool({}), bool(()))
print(bool(1), bool(0.01), bool(' '), bool([1]), bool({3}), bool((6,)))


False False False False False False
True True True True True True
```


2 
 `and`, `or`, and `not` work as expected on bools, but when used on other objects, will return the first operand that decides the result (first `True` value or last `False` in `or`, last `True` value or first `False` value in `and`)



3 
`and`, `or`, and `not` work as expected on bools, but when used on other objects, will return the first operand that decides the result (first `True` value or last `False` in `or`, last `True` value or first `False` value in `and`)

```python
0 or '', '' or 0, 1 and 'a', '' and 1, 0 or 'tree' or 5, 6 and [] or [5], a and 6

('', 0, 'a', '', 'tree', [5], 6)
```


