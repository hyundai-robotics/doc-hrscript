# `set_send_trail_null`

### Description

当使用 `ENet.send()` 函数发送字符串时，它设置是否附加终止空字符发送。（默认值为 false）

### Syntax

`{ENet object}.set_send_trail_null(true|false)`

### Return value

无。

### Example

```python
enet_to_sensor.set_send_trail_null(true)
enet_to_sensor.send "ACK"
enet_to_sensor.set_send_trail_null(false)
```