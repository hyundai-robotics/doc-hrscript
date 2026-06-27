# `listen`

### Description

作为以太网 TCP 通信中的服务器，它为客户端的连接请求做准备。 
在 UDP 点对点通信中未使用。


### Syntax

`{ENet object}.listen [{backlog}]`


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
      <td>backlog</td>
      <td>
        未被接受的待处理连接的允许连接数。<br>
        如果未指定，将无限期等待。
      </td>
      <td></td>
    </tr>
  </tbody>
</table>


### Return value

<table>
  <thead>
    <tr>
      <th style="text-align:left">Value</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Misc.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>
        OK
      </td>
      <td></td>
    </tr>
    <tr>
      <td>-1</td>
      <td>错误</td>
      <td></td>
    </tr>	 
  </tbody>
</table>


### Example

```python
enet_to_sensor.listen
enet_to_sensor.accept 5000,*TimeOut
```