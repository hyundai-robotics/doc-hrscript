# set_send_trail_null


### Description

When sending a string with the `ENet.send()` function, it sets whether to send it with a terminating-null character attached. (default is false)


### Syntax

`{ENet object}.set_send_trail_null(true|false)`


### Return value

None.


### Example

```python
enet_to_sensor.set_send_trail_null(true)
enet_to_sensor.send "ACK"
enet_to_sensor.set_send_trail_null(false)
```
