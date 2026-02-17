# `nbyte`

### 语法

`{BBuf object}.nbyte`


### 返回值

二进制数据的字节数


### 示例

```python
var bbuf=enet.BBuf()
bbuf.append("s4", 20)
bbuf.append("s4", -10)
print bbuf.nbyte() # "8"
```