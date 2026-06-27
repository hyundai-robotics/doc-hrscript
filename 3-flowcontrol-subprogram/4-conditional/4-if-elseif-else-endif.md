# 3.4.4. `如果 (if)`-`elseif`-`else`-`endif`

### Description

在多个条件的情况下，可以使用以下形式的 `elseif` 语句。

### Syntax

```python
if <bool expression>
	<statement A>
	...
elseif <bool expression>
	<statement B>
	...
elseif <bool expression>
	<statement C>
	...
else
	<statement N>
	...
endif
```

### Example

```python
var pressure=95, limit_h=90, limit_m=80
if pressure > limit_h
	print "警告：压力过高。"
elseif pressure > limit_m
	print "通知：压力偏高。"
else
	print "处于正常运行状态。"
endif
end
```