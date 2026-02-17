# `_task.enable`

### 描述

一个系统变量，用于确定子任务是否处于活动状态。


### 语法

```python
var res
res = _task[1].enable
```


### 示例

```python
   ...
   if _task[1].enable==1  # 如果子任务 1 处于活动状态
   print "Subtask 1 is active"
   endif
   ...
   end
```