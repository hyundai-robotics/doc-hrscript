# `_spd_rate`

获取或设置播放速度。

### Description

与 cond.set 相同的设置 - 播放速度。

- 单位 : %
- 范围 : 1 到 100
- 默认值 : 100

### Syntax

```python
var res
res = _spd_rate
```

### Sample

```python
   ...
   # 如果播放速度小于 50%，提高到 100%。
   if _spd_rate<50
     _spd_rate=100
   ...
   end
```