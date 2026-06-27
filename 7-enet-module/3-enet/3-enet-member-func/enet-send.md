# `send`

### Description

将字符串数据发送到以太网对象。

### Syntax

`{ENet object}.send {msg}`

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
      <td style="text-align:left">msg</td>
      <td style="text-align:left">
        要发送的字符串
      </td>
      <td style="text-align:left">字符串</td>
    </tr>
  </tbody>
</table>

### Return value

发送的字节数。

### Example

```python
enet_to_sensor.send "rob:"+10+", command:"+cmd+"\n"
```