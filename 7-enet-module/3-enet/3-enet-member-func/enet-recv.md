# `recv`

### Description

从以太网对象接收字符串数据。接收到的字符串可以通过返回值或 `result()` 函数获取。


### Syntax

`{ENet object}.recv [{waiting time}][,{address on timeout}]`


### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Misc.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>waiting time</td>
      <td>
        超时。如果超时，则执行下一个命令或跳转到超时的地址。<br>
        如果未指定，则无限期等待。
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>address on timeout</td>
      <td>
        超时后跳转的地址。<br>
        如果未指定，则执行下一个命令。
      </td>
      <td>address</td>
    </tr>
  </tbody>
</table>


### Return value

接收到的字符串。


### Example

```python
var msg
msg=enet_to_sensor.recv
msg=enet_to_sensor.recv(5000)
msg=enet_to_sensor.recv(5000,*TimeOut)
end

*TimeOut
print "超时！来自传感器没有响应"
end
```