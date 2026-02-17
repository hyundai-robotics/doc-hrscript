# 10.1.9 `count_up`

`count_up` 声明是一个过程，它将指定变量的值增加 1，并在超过预设值时将其重置为初始值。

### 描述

此声明每次执行时将指定变量的值增加 1。  
如果变量值超过预设值所指定的值，则该变量将重置为初始值所指定的值。

执行  
```python
count_up cnt, init=0, preset=100`  
```
产生的结果与执行以下四行相同：

```python
cnt = cnt + 1
if cnt > 100
    cnt = 0
endif
```

### 语法
```python
count_up <variable>, init=<initial value>, preset=<final value>
```

### 参数
| 项目     | 描述                                                              | 备注 |
| -------- | ------------------------------------------------------------------------ | ------- |
| Variable | 将作为计数器的变量，其值将被增加                                    |         |
| init     | 当变量超过预设值时要分配的初始值                                     |         |
| preset   | 变量的最大值                                                         |         |

### 示例
```python
   global work_no
   move P, spd=30%, accu=0, tool=1
   delay 0.5
   move P, spd=30%, accu=0, tool=1
   move L, spd=30mm/s, accu=0, tool=1
   move L, spd=30mm/s, accu=0, tool=1
   delay 0.5
   move P, spd=30%, accu=0, tool=1
   count_up work_no, init=0, preset=99
   end
```