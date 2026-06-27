# `_soft_limit`

读取或设置软件限制的值。

### Description

单位是线性轴的毫米和旋转轴的度数。您可以在指定的最小值和最大值范围内设置值。

### Syntax

```python
var res
res = _soft_limit[2].min
```

### Sample

```python
   ...
   # 将第一个轴的软件限制的最小值设置为 -90 度。
   print _soft_limit[0].min
   _soft_limit[0].min=-90
   ...
   end
```