# `clr_rbuf`

### Description

Initialize `Sci`'s received buffer.


### Syntax

&lt;Sci object&gt;.clr_rbuf()

### Return Value
- 0: Receive buffer initialization success
- -1: Fail

### Example

```python
var ret
ret=sci2.clr_rbuf()
if ret<0
  print "receive buffer clear error"
  stop
endif
```



