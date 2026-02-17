# 3.5. 嵌套流程控制语句

### 描述

在控制语句块中，可以放置另一个控制语句块，如下例所示。在以下形式中，显示了两个嵌套级别，但可以根据需要进行多个嵌套级别。

### 语法

```python
if <bool expression>
	if <bool expression>
		<statement A>
		...
	else
		<statement B>
		...
	endif
endif
```

### 示例

```python
var pressure=95, limit=90, inject_on=true
if inject_on
	if pressure > limit
		print "warning: pressure is high."
	else
		print "in normal operation."
	endif
endif
end
```