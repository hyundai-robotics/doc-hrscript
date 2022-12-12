# clear

### Description

Delete all data stored in the binary buffer.


### Syntax

`{BBuf object}.clear()`


### Parameters

None


### Example

```python
var bbuf=enet.BBuf()
bbuf.append("s4", 20)
bbuf.append("s4", -10)
bbuf.clear()
```
