# `_task.enable`

### Description

一个系统变量，用于确定子任务是否处于活动状态。

### Syntax

```python
var res
res = _task[1].enable
```

### Sample

```python
   ...
   if _task[1].enable==1  # 如果子任务 1 活动
   print "子任务 1 活动"
   endif
   ...
   end
```