# `send`

### 描述

将字符串数据发送到以太网对象。


### 语法

`{ENet object}.send {msg}`



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
      <td style="text-align:left">msg</td>
      <td style="text-align:left">
        要发送的字符串
      </td>
      <td style="text-align:left">字符串</td>
    </tr>
  </tbody>
</table>


### 返回值

发送的字节数。


### 示例

```python
enet_to_sensor.send "rob:"+10+", command:"+cmd+"\n"
```