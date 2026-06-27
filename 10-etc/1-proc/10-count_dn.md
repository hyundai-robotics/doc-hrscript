# 10.1.10 `count_dn` 语句

`count_dn` 语句是一个过程，它将指定变量的值减少 1，当该值小于预设值时，将其重置为初始值。

### 描述

该语句每次执行时将指定变量的值减少 1。  
如果变量值小于预设值，则变量被重置为初始值指定的值。

执行  
```python
count_dn cnt, init=100, preset=0
```
的结果与执行以下四行代码的结果相同：

```python
cnt = cnt - 1
if cnt < 0
    cnt = 100
endif
```

### 语法
```python
count_dn <variable>, init=<initial value>, preset=<final value>
```

### 参数
| 项目     | 描述                                                                 | 备注 |
| -------- | ---------------------------------------------------------------------- | ----- |
| 变量     | 将作为计数器减少值的变量                                             |       |
| init     | 当变量小于 `preset` 值时要分配的初始值                             |       |
| preset   | 变量的最小值                                                          |       |


### 示例
```python
   global work_no
   move P,spd=30%,accu=0,tool=1
   delay 0.5
   move P,spd=30%,accu=0,tool=1
   move L,spd=30mm/s,accu=0,tool=1
   move L,spd=30mm/s,accu=0,tool=1
   delay 0.5
   move P,spd=30%,accu=0,tool=1
   count_dn work_no,init=99,preset=0
   end
```