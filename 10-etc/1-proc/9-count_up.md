# 10.1.9 count_up

The `count_up` statement is a procedure that increments the value of a specified variable by 1, and resets it to the init value when it exceeds the preset value.

### Description

This statement increases the value of the specified variable by 1 each time it is executed.  
If the variable value exceeds the value specified by preset value, the variable is reset to the value specified by init value.

Executing  
```python
count_up cnt, init=0, preset=100`  
```
produces the same result as executing the following four lines:

```python
cnt = cnt + 1
if cnt > 100
    cnt = 0
endif
```

### Syntax
```python
count_up <variable>, init=<initial value>, preset=<final value>
```

### Parameters
| Item     | Description                                                              | Remarks |
| -------- | ------------------------------------------------------------------------ | ------- |
| Variable | The variable whose value will be incremented as a counter                |         |
| init     | The initial value to assign when the variable exceeds the preset value   |         |
| preset   | The maximum value of the variable                                        |         |

### Example
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