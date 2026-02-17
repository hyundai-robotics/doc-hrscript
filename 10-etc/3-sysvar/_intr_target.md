# `_intr.target`

`_intr.target` 系统变量调整机器人的目标位置达成状态。

### 描述

在移动语句中，当发生中断并在调用程序执行结束后返回到上一个程序的位置时，用于调整位置。

### 语法

```python
_intr_target=1
```

### 示例

```python
- _intr.target=-1
```

![](../../_assets/intr_target_1.png)


```python
- _intr.target=1 or 0
```
![](../../_assets/intr_target_2.png)