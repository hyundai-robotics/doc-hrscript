# 10.1.10 count_dn Statement

The `count_dn` statement is a procedure that decrements the value of a specified variable by 1, and resets it to the init value when it becomes smaller than the preset value.

### Description

This statement decreases the value of the specified variable by 1 each time it is executed.  
If the variable value becomes less than the value specified by preset value, the variable is reset to the value specified by init value.

Executing  
```python
count_dn cnt, init=100, preset=0
```
produces the same result as executing the following four lines:

```python
cnt = cnt - 1
if cnt < 0
    cnt = 100
endif
```

### Syntax
```python
count_dn <variable>, init=<initial value>, preset=<final value>
```

### Parameters
| Item     | Description                                                                        | Remarks |
| -------- | ---------------------------------------------------------------------------------- | ------- |
| Variable | The variable whose value will be decremented as a counter                          |         |
| init     | The initial value to assign when the variable becomes less than the `preset` value |         |
| preset   | The minimum value of the variable                                                  |         |


### Example
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
