# 3.4.3 `if`-`else`-`endif` 语句

### 描述

如果表达式为假，并且 `if` 有要执行的语句，则使用以下形式：

如果表达式为真，则执行语句 A。如果为假，则执行语句 B。

### 语法

```python
if <bool expression>
	<statement A>
	...
else
	<statement B>
	...
endif
```

### 示例

```python
var pressure=95, limit=90, exceed
if pressure > limit
	exceed = pressure - limit
	print "warning: pressure is too high."
else
	print "in normal operation."
endif
end
```