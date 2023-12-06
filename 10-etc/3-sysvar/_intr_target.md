# 9.1.2 _intr.target

`_intr.target` system variable adjusts the robot's target position reach state.


### Description

In the move statement, this is used to adjust the position when the an interrupt occurs while moving and returns to the position of the previous program after the execution of the call program ends.


### Syntax

```python
_intr_target=1
```

### Sample

```python
- _intr.target=-1
```

![](../../_assets/intr_target_1.png)


```python
- _intr.target=1 or 0
```
![](../../_assets/intr_target_2.png)

