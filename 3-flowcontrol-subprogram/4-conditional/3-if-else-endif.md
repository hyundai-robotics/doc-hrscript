# 3.4.3 `如果 (if)`-`else`-`endif` 语句

### 描述

如果表达式为假，并且 `如果 (if)` 有要执行的语句，则使用以下形式：

如果表达式为真，将执行语句 A。如果为假，将执行语句 B。

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
	print "警告: 压力过高."
else
	print "处于正常运行中."
endif
end
```