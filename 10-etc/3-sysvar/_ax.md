# `_ax`

用于通过轴名称读取轴索引。

### Description

轴索引是通过参考值0获得的。然而，如果轴不存在，则分配-1。指定跟随"_ax."的字符串作为轴名称。轴名称支持小写和大写字母。

支持版本 V70.02-00

### Syntax

```python
var res
res = _ax.v # 获取 V 轴索引
```

### Sample

```python
   ...
   # 打印 R1 轴的当前位置信息。
   global po
   po=cpo("joint")
   print po.j[_ax.R1]
   ...
   end
```