# 10.1.8 optime

The `optime` statement is a procedure used to start or update the measurement of operating time.

### Description

Normally, the measurement of operating time starts when the start button is pressed, and the operating time is automatically updated when the program executes `end`.  
However, if the program jumps back to the beginning using a `goto` statement without executing `end`, the operating time continues to increase. In this case, the monitored operating-time value becomes meaningless.

To address this situation, the `optime` statement allows the user to explicitly specify the points at which operating-time measurement starts and is updated.

### Syntax
```python
optime <parameter>
```
### Parameters
| Item      | Description                                                             | Remarks |
| --------- | ----------------------------------------------------------------------- | ------- |
| Parameter | - cycle_start: Start measurement<br>- cycle_end: Update measurement     |         |

```python
  *start
   optime cycle_start
   move P, spd=30%, accu=0, tool=1
   delay 0.5
   move P, spd=30%, accu=0, tool=1
   move L, spd=30mm/s, accu=0, tool=1
   move L, spd=30mm/s, accu=0, tool=1
   delay 0.5
   move P, spd=30%, accu=0, tool=1
   optime cycle_end
   goto *start
   end
```