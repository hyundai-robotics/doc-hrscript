# 3.4.4. if-elseif-else-endif

### Description

In the case of multiple conditions, the elseif statement can be used in the following form.

### Syntax

```python
if <bool expression>
	<statement A>
	…
elseif <bool expression>
	<statement B>
	…
elseif <bool expression>
	<statement C>
	…
else
	<statement N>
	…
endif
```

### Example

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



