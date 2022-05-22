# 3.4.3 if-else-endif Statement

### Description

If the expression is false and if there are statements to be executed, the following form is used:

If the expression is true, statement A will be executed. If false, statement B will be executed.

### Syntax

```python
if <bool expression>
	<statement A>
	…
else
	<statement B>
	…
endif
```

### Example

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



