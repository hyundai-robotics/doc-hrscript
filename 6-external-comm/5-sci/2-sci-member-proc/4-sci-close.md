# `关闭 (close)`

### Description

执行 `Sci` 的 `关闭 (close)` 以关闭串行端口。

### Syntax

&lt;Sci object&gt;.close()

### Return Value
- 0: 成功
- -1: 失败

### Example

```python
var ret
ret=sci2.close()
if ret<0
  print "open error"
  stop
endif
```