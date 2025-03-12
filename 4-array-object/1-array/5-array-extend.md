# 4.1.5 Extend Procedure for Adding All Elements of One Array to Another

Supported from V60.32-01

The extend procedure can be used to add all elements of an array to another.

```python
var arr = [1, 2]
var brr = [3, 4]
extend arr, brr
print arr   # [1, 2, 3, 4]
```

A temporary array can be used as a parameter.

```python
var arr = [1, 2]
extend arr, [3, 4, 5]
print arr   # [1, 2, 3, 4, 5]
```
