# `accept`

### 描述

作为以太网 TCP 通信中的服务器，它等待来自客户端的连接请求。当请求发生时创建连接。
在 UDP 对等通信中不使用。


### 语法

`{ENet object}.accept [{等待时间}] [, {超时地址}]`


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
        超时。如果经过时间，执行下一个命令或跳转到超时地址。<br>
        如果未指定，则无限等待。
      </td>
      <td>毫秒</td>
    </tr>
    <tr>
      <td>超时地址</td>
      <td>
        超时后跳转的地址。<br>
        如果未指定，则执行下一个命令。
      </td>
      <td>地址</td>
    </tr>
  </tbody>
</table>


### 返回值

<table>
  <thead>
    <tr>
      <th style="text-align:left">名称</th>
<table>
  <thead>
    <tr>
      <th style="text-align:left">含义</th>
      <th style="text-align:left">其他</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>
        OK（完成）
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


### 示例

enet_to_sensor.listen
var ret=enet_to_sensor.accept(5000)

enet_to_sensor.listen
enet_to_sensor.accept 5000,*TimeOut