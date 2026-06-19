# put

### Description

You can change the value of an existing tag or add a option tags by executing the RSI put() function.


### Syntax

&lt;RSI object&gt;.put("cmd_po") <br>
&lt;RSI object&gt;.put("trigger", 1) <br>

### Return Value
- 1: Change the value of the existing tag
- 0: Add option tag
- -1: When there is only one argument to the function, the input argument is not a system tag

### Example

```python
var ret
ret=rsi.put("cmd_po")  # Include the "cmd_po" tag in the output.
ret=rsi.put("trigger", 1)  # Change the value of the trigger tag to 1
ret=rsi.put("MyValue1", 789)  # Add the MyValue1 tag to set the integer value 789
ret=rsi.put("MyValue2", 1.2345)  # Add the MyValue2 tag to set the floating-point value 1.2345
ret=rsi.put("MyValue3", "hello")  # Add the MyValue3 tag to specify the string "hello"
```



