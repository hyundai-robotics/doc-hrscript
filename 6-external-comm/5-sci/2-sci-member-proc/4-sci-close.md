# `close`

### Description

Execute `Sci`'s `close` to close the serial port.


### Syntax

&lt;Sci object&gt;.close()

### Return Value
- 0: Success
- -1: Fail

### Example

```python
var ret
ret=sci2.close()
if ret<0
  print "open error"
  stop
endif
```



