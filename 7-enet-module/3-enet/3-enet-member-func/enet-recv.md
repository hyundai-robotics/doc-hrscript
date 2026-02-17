# `recv`

### 描述

从以太网对象接收字符串数据。接收到的字符串可以从返回值或 `result()` 函数中获取。

### 语法

`{ENet object}.recv [{等待时间}][,{超时地址}]`

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">名称</th>
      <th style="text-align:left">含义</th>
      <th style="text-align:left">其他</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>等待时间</td>
      <td>
        超时。如果超时，继续下一个命令或跳转到超时地址。<br>
        如果未指定，则无限期等待。
      </td>
      <td>毫秒</td>
    </tr>
    <tr>
      <td>超时地址</td>
      <td>
        超时后跳转的地址。<br>
        如果未指定，继续下一个命令。
      </td>
      <td>地址</td>
    </tr>
  </tbody>
</table>

### 返回值

接收到的字符串。

### 示例
```python
var msg
msg=enet_to_sensor.recv
msg=enet_to_sensor.recv(5000)
msg=enet_to_sensor.recv(5000,*TimeOut)
end

*TimeOut
print "超时！传感器没有响应"
end
```