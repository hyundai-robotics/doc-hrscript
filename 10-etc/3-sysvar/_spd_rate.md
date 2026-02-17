# `_spd_rate`

获取或设置播放速度。

### 描述

与 cond.set 相同的设置 - 播放速度。

- 单位 : %
- 范围 : 1 到 100
- 默认值 : 100

### 语法

```python
var res
res = _spd_rate
```

### 示例

```python
   ...
   # 如果播放速度低于 50%，则将其提高到 100%。
   if _spd_rate<50
     _spd_rate=100
   ...
   end
```