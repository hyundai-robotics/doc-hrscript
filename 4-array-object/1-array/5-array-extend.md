# 4.1.5 `extend_arr` Procedure for Adding All Elements of One Array to Another

Supported from V60.32-00

The `extend_arr` procedure can be used to add all elements of an array to another.

```python
var arr = [1, 2]
var brr = [3, 4]
extend_arr arr, brr
print arr   # [1, 2, 3, 4]
```

It can be used like below.

```python
var arr = [1, 2]
extend_arr arr, [3, 4, 5]
print arr   # [1, 2, 3, 4, 5]
```
