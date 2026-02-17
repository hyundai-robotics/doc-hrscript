# `clr_rbuf`

### 描述

初始化 `Sci` 的接收缓冲区。

### 语法

&lt;Sci 对象&gt;.clr_rbuf()

### 返回值
- 0: 接收缓冲区初始化成功
- -1: 失败

### 示例

```python
var ret
ret=sci2.clr_rbuf()
if ret<0
  print "receive buffer clear error"
  stop
endif
```