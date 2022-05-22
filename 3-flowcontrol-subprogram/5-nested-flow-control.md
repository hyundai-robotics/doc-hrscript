# 3.5. Nested Flow-Control Statements

### Description

In the control statement block, another control statement block can be placed, as shown in the following example. In the following form, two nesting  levels are shown, but multiple nesting levels can be made as much as necessary.

### Syntax

```python
if <bool expression>
	if <bool expression>
		<statement A>
		…
	else
		<statement B>
		…
	endif
endif
```

### Example

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



