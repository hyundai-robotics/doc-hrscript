# `set_send_trail_null`

### 描述

当使用 `ENet.send()` 函数发送字符串时，它设置是否附加终止空字符进行发送。（默认为 false）

### 语法

`{ENet object}.set_send_trail_null(true|false)`

### 返回值

无。

### 示例

```python
enet_to_sensor.set_send_trail_null(true)
enet_to_sensor.send "ACK"
enet_to_sensor.set_send_trail_null(false)
```