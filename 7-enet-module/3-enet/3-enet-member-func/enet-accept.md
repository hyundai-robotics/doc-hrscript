# `accept`

### Description

作为以太网 TCP 通信中的服务器，它等待来自客户端的连接请求。当请求发生时，创建连接。  
不用于 UDP 对等通信。


### Syntax

`{ENet object}.accept [{waiting time}] [, {address on timeout}]`


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
        超时。如果经过，则继续执行下一个命令或跳转到超时地址。<br>
        如果未指定，则无限期等待。
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>address on timeout</td>
      <td>
        超时时跳转的地址。<br>
        如果未指定，则继续执行下一个命令。
      </td>
      <td>address</td>
    </tr>
  </tbody>
</table>


### Return value

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
      <td>1</td>
      <td>
        OK (完成)
      </td>
      <td></td>
    </tr>  
    <tr>
      <td>0</td>
      <td>
        等待中
      </td>
      <td></td>
    </tr>
    <tr>
      <td>-1</td>
      <td>超时</td>
      <td></td>
    </tr>
    <tr>
      <td>-2</td>
      <td>错误</td>
      <td></td>
    </tr>    
  </tbody>
</table>


### Example

```python
enet_to_sensor.listen
var ret=enet_to_sensor.accept(5000)
```

```python
enet_to_sensor.listen
enet_to_sensor.accept 5000,*TimeOut
```