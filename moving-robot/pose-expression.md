# 5.3 Pose Expression

The expression in which the result value becomes a pose is called a “pose expression.” 

All the following forms are recognized as poses.

```python
Pose
Pose+Shift
Pose-Shift
Pose+Shift+Shift+…
```



Refer to the following example of assigning the result of a pose expression to another pose variable.

```python
var po1 = Pose(10, 90, 0, 0, -30, 0)
var po2 = Pose(1850, 0, 2010.5, 0, -90, 0, "base", "fl;r2")
var po3 = cpo("robot")
var sft1 = Shift(30, 0, 0, 0, -5.8, 0)
var po4 = po1-sft1
var po5 = po2+sft1+Shift(0, 0, 55.2, 0, -5, 0, "base")
```

