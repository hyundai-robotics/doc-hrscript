# 6.6.1 Constructor

### Description

Creates a global variable for the `RSI` object.

### Syntax

com.RSI(enet object) <br>

Specifies the object used in the Ethernet communication settings. For example, if the name of the object used is "enet0", specify _enet0, and if it is "enet1", specify _enet1.  

### Return Value

Reference to created object

### Example

```python
global rsi
rsi=com.RSI(_enet0)  # _enet0 uses the "enet0" object in Ethernet communication settings 
```



