# 2.9 函数

将角度 60° 转换为弧度值的过程是什么，或者如何找到变量 mystr 所包含的字符串的长度？

HRScript 提供了各种函数，这些函数通过参数接收输入，执行一些处理，并返回结果值。

函数可以作为表达式的一部分使用，如下所示。

```python
var dg=60, rd
rd=deg2rad(dg)

var limit=40, message="Input your code number"
var validity= len(message) < limit
```

HRScript 提供的函数列表如下。\(表格按名称的升序排列。\)