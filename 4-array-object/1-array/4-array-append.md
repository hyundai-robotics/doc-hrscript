# 4.1.4 Append Procedure for Adding an Element to an Array

Supported from V60.32-00

The append procedure can be used to add an element to an array

```python
var arr = [1, 2]
append_arr arr, 3   # Adding 3 as an element of arr
print arr       # [1, 2, 3]
```

Any value, including another array, can be appended as an element because an array can contain elements of different types.

```python
var arr = [1, 2]
append_arr arr, [3, 4]  # Appending [3, 4] as an element of arr
print arr           # [1, 2, [3, 4]]
```
