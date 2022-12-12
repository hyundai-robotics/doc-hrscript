# nbyte

### Syntax

`{BBuf object}.nbyte`


### Return value

The number of bytes of binary data


### Example

```python
var bbuf=enet.BBuf()
bbuf.append("s4", 20)
bbuf.append("s4", -10)
print bbuf.nbyte() # "8"
```
