# `关闭 (close)`

### 描述

执行 `Sci` 的 `关闭 (close)` 以关闭串口。

### 语法

&lt;Sci object&gt;.close()

### 返回值
- 0: 成功
- -1: 失败

### 示例

```python
var ret
ret=sci2.close()
if ret<0
  print "open error"
  stop
endif
```