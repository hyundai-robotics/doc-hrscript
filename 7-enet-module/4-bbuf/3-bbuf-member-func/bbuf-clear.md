# `初始化 (clear)`

### Description

删除存储在二进制缓冲区中的所有数据。


### Syntax

`{BBuf object}.clear()`


### Parameters

无


### Example

```python
var bbuf=enet.BBuf()
bbuf.append("s4", 20)
bbuf.append("s4", -10)
bbuf.clear()
```