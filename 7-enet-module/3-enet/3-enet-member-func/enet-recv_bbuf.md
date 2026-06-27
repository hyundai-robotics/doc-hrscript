# `recv_bbuf`

### Description

从以太网对象接收二进制数据并将其存储在 [BBuf](../../4-bbuf/README.md) 对象中。


### Syntax

`{ENet object}.recv_bbuf {BBuf onject}[,{waiting time}][,{address on timeout}]`


### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">名称</th>
      <th style="text-align:left">含义</th>
      <th style="text-align:left">杂项</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>BBuf object</td>
      <td>
        用于存储接收到的二进制数据的BBuf对象
      </td>
      <td></td>
    </tr>
    <tr>
      <td>waiting time</td>
      <td>
        超时。如果超时，则继续执行下一个命令或跳转到超时地址。<br>
        如果未指定，则无限等待。
      </td>
      <td>毫秒</td>
    </tr>
    <tr>
      <td>address on timeout</td>
      <td>
        超时后跳转到的地址。<br>
        如果未指定，继续执行下一个命令。
      </td>
      <td>地址</td>
    </tr>
  </tbody>
</table>


### Return value

接收到的数据数量。


### Example

```python
var bbuf=enet_to_sensor.BBuf()
enet_to_sensor.recv bbuf
enet_to_sensor.recv bbuf, 5000
var nitem=enet_to_sensor.recv(bbuf,5000,*TimeOut)
end

*TimeOut
print "超时！传感器无响应"
end
```