# open

### Description

Execute Sci's open() function to open the serial port.

The serial port is opened with the preset contents through the controller settings, and there is no need to separately open the port unless the port was previously closed.(default: open)


### Syntax

&lt;Sci object&gt;.open()

### Return Value
- 0: Success
- <0: Fail


### Example

```python
var ret
ret=sci2.open()
if ret<0
  print "open error"
  stop
endif
```



