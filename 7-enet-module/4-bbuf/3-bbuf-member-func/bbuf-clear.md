# 清除 (clear)

### 描述

删除存储在二进制缓冲区中的所有数据。


### 语法

`{BBuf object}.clear()`


### 参数

无


### 示例

```python
var bbuf=enet.BBuf()
bbuf.append("s4", 20)
bbuf.append("s4", -10)
bbuf.clear()
```