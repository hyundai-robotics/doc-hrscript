# 10.1.9 `count_up`

`count_up` 语句是一个过程，它将指定变量的值增加 1，当超过预设值时将其重置为初始值。

### 描述

每次执行该语句时，它会将指定变量的值增加 1。  
如果变量值超过预设值，则将变量重置为指定的初始值。

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
| 项目     | 描述                                                                   | 备注    |
| -------- | ---------------------------------------------------------------------- | ------- |
| 变量     | 作为计数器，其值将被增加的变量                                        |         |
| init     | 当变量超过预设值时分配的初始值                                        |         |
| preset   | 变量的最大值                                                          |         |

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