# 4.1.5 `extend_arr` 过程将一个数组的所有元素添加到另一个数组

支持版本：V60.32-00

`extend_arr` 过程可用于将一个数组的所有元素添加到另一个数组。

```python
var arr = [1, 2]
var brr = [3, 4]
extend_arr arr, brr
print arr   # [1, 2, 3, 4]
```

它可以像下面这样使用。

```python
var arr = [1, 2]
extend_arr arr, [3, 4, 5]
print arr   # [1, 2, 3, 4, 5]
```