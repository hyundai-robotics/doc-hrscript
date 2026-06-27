# `open`

### Description

执行 `Sci` 的 `open()` 函数以打开串口。

通过控制器设置以预设内容打开串口，除非之前关闭了端口，否则无需单独打开该端口。(默认：打开)

### Syntax

&lt;Sci object&gt;.open()

### Return Value
- 0: 成功
- <0: 失败

### Example

```python
var ret
ret=sci2.open()
if ret<0
  print "open error"
  stop
endif
```