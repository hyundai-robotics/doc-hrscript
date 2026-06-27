# 10.1.11 `cycle_end`

`cycle_end` 语句是一个过程，清除所有由于执行 `call` 语句而被管理的调用堆栈。

### 描述

当程序在调用堆栈存在时执行 `end` 语句，程序执行将返回到执行 `call` 语句的位置并继续运行。  
但是，当执行 `cycle_end` 语句时，所有管理的调用堆栈都会被清除。因此，程序不会返回到 `call` 语句的位置，而是停止执行。

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