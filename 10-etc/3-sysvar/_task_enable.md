# `_task.enable`

### Description

A system variable to determine whether a subtask is active.


### Syntax

```python
var res
res = _task[1].enable
```


### Sample

```python
   ...
   if _task[1].enable==1  # If subtask 1 is active
   print "Subtask 1 is active"
   endif
   ...
   end
```


