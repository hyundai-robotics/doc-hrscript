# 3.4.4. `if`-`elseif`-`else`-`endif`

### 描述

在多个条件的情况下，可以以以下形式使用 `elseif` 语句。

### 语法

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

### 示例

```python
var pressure=95, limit_h=90, limit_m=80
if pressure > limit_h
	print "warning : pressure is too high."
elseif pressure > limit_m
	print "notification: pressure is high."
else
	print "in normal operation."
endif
end
```