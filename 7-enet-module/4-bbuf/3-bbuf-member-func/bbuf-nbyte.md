# `nbyte`

### Syntax

`{BBuf object}.nbyte`


### Return value

二进制数据的字节数


### Example

```python
var bbuf=enet.BBuf()
bbuf.append("s4", 20)
bbuf.append("s4", -10)
print bbuf.nbyte() # "8"
```