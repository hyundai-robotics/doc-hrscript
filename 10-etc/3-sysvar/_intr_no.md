# `_intr.no`

`_intr.no`系统变量是发生的中断编号。

### Description

当因为`intr_def`过程中的条件表达式满足而发生中断时，您可以使用`_intr.no`来确定程序是由哪个中断编号调用的。

### Syntax

```python
var res
res = _intr.no
```

### Sample

```python
   ...
   if _intr.no==1  # 如果发生中断编号 1
   print "通过传感器 1 激活，发生中断。"
   else if _intr.no==2 # 如果发生中断编号 2
   print "通过传感器 2 激活，发生中断。"
   stop # robot stops
   endif
   ...
   end
```