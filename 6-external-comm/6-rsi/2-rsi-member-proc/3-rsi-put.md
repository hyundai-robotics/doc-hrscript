# put

### Description

您可以通过执行 RSI put() 函数更改现有标签的值或添加选项标签。


### Syntax

&lt;RSI object&gt;.put("cmd_po") <br>
&lt;RSI object&gt;.put("trigger", 1) <br>

### Return Value
- 1: 更改现有标签的值
- 0: 添加选项标签
- -1: 当函数只有一个参数时，输入参数不是系统标签

### Example

```python
var ret
ret=rsi.put("cmd_po")  # 包含 "cmd_po" 标签到输出中。
ret=rsi.put("trigger", 1)  # 将触发器标签的值更改为 1
ret=rsi.put("MyValue1", 789)  # 添加 MyValue1 标签以设置整数值 789
ret=rsi.put("MyValue2", 1.2345)  # 添加 MyValue2 标签以设置浮点值 1.2345
ret=rsi.put("MyValue3", "hello")  # 添加 MyValue3 标签以指定字符串 "hello"
```