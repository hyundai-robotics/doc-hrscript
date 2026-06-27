# 5.3 姿态表达

结果值成为姿态的表达式称为 `姿态表达式`。

以下所有形式都被识别为姿态。

```python
Pose
Pose+Shift
Pose-Shift
Pose+Shift+Shift+...
```

请参考以下将姿态表达式的结果分配给另一个姿态变量的示例。

```python
var po1 = Pose(10, 90, 0, 0, -30, 0)
var po2 = Pose(1850, 0, 2010.5, 0, -90, 0, "base", "fl;r2")
var po3 = cpo("robot")
var sft1 = Shift(30, 0, 0, 0, -5.8, 0)
var po4 = po1-sft1
var po5 = po2+sft1+Shift(0, 0, 55.2, 0, -5, 0, "base")
```