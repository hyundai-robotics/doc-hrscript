# 4.1.4 `append_arr` 程序用于向数组添加元素

支持版本 V60.32-00

`append_arr` 程序可以用于向数组添加元素

```python
var arr = [1, 2]
append_arr arr, 3   # 添加 3 作为 arr 的元素
print arr       # [1, 2, 3]
```

任何值，包括另一个数组，都可以作为元素添加，因为数组可以包含不同类型的元素。

```python
var arr = [1, 2]
append_arr arr, [3, 4]  # 将 [3, 4] 作为 arr 的元素添加
print arr           # [1, 2, [3, 4]]
```