# `recv_bbuf`

### 描述

从以太网对象接收二进制数据并将其存储在 [BBuf](../../4-bbuf/README.md) 对象中。

### 语法

`{ENet object}.recv_bbuf {BBuf onject}[,{waiting time}][,{address on timeout}]`

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">名称</th>
      <th style="text-align:left">含义</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>BBuf 对象</td>
      <td>
        用于存储接收到的二进制数据的 BBuf 对象
      </td>
      <td></td>
    </tr>
    <tr>
      <td>等待时间</td>
      <td>
        超时。如果超时，继续执行下一个命令或跳转到超时地址。<br>
        如果未指定，将无限期等待。
      </td>
      <td>毫秒</td>
    </tr>
    <tr>
      <td>超时地址</td>
      <td>
        超时时要跳转的地址。<br>
        如果未指定，则继续执行下一个命令。
      </td>
      <td>地址</td>
    </tr>
  </tbody>
</table>
### 返回值

接收到的数据数量。


### 示例

```python
var bbuf=enet_to_sensor.BBuf()
enet_to_sensor.recv bbuf
enet_to_sensor.recv bbuf, 5000
var nitem=enet_to_sensor.recv(bbuf,5000,*TimeOut)
end

*TimeOut
print "时间到！传感器没有响应"
end
```