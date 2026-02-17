# 10.1.8 `optime`

`optime`语句是一种用于启动或更新操作时间测量的程序。

### 描述

通常，当按下启动按钮时，操作时间测量开始，操作时间在程序执行`end`时自动更新。  
然而，如果程序在未执行`end`的情况下使用`goto`语句跳回开始，操作时间会继续增加。在这种情况下，监控的操作时间值变得毫无意义。

为了解决这种情况，`optime`语句允许用户明确指定操作时间测量开始和更新的点。

### 语法
```python
optime <parameter>
```
### 参数
| 项目      | 描述                                                               | 备注   |
| --------- | ------------------------------------------------------------------ | ------ |
| 参数      | - cycle_start: 开始测量<br>- cycle_end: 更新测量                 |        |

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