# `_intr.no`

`_intr.no` 系统变量是发生的中断号。

### 描述

当因为 `intr_def` 程序中的条件表达式被满足而发生中断时，您可以使用 `_intr.no` 来确定程序是由哪个中断号调用的。


### 语法

```python
var res
res = _intr.no
```


### 示例

```python
   ...
   if _intr.no==1  # 如果发生中断号 1 
   print "通过传感器 1 的激活，发生中断。"
   else if _intr.no==2 # 如果发生中断号 2 
   print "通过传感器 2 的激活，发生中断。"
   stop # 机器人停止
   endif
   ...
   end
```