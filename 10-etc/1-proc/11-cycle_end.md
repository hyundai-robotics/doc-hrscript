# 10.1.11 `cycle_end`

`cycle_end` 语句是一个过程，它清除因执行 `call` 语句而管理的所有调用堆栈。

### 描述

当程序在存在调用堆栈的情况下执行 `end` 语句时，程序执行返回到执行 `call` 语句的位置并继续运行。  
然而，当执行 `cycle_end` 语句时，所有管理的调用堆栈都会被清除。因此，程序不会返回到 `call` 语句的位置，而是停止执行。

### 语法

```python
cycle_end
```

### 示例

```python
   0001.job
   ...
   move P,spd=30%,accu=0,tool=1
   call 10
   move P,spd=30%,accu=0,tool=1
   move L,spd=30mm/s,accu=0,tool=1
   move L,spd=30mm/s,accu=0,tool=1
   delay 0.5
   move P,spd=30%,accu=0,tool=1
   end


   0010.job
   ...
   move P,spd=30%,accu=0,tool=1
   delay 0.5
   cycle_end


```