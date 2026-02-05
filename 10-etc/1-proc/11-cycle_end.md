# 10.1.11 cycle_end

The `cycle_end` statement is a procedure that clears all call stacks that are being managed as a result of executing `call` statements.

### Description

When a program executes the `end` statement while a call stack exists, program execution returns to the position where the `call` statement was executed and continues running.  
However, when the `cycle_end` statement is executed, all managed call stacks are cleared. As a result, the program does not return to the position of the `call` statement and instead stops execution.

### Syntax

```python
cycle_end
```

### Example

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
