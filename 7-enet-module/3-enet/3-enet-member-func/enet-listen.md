# `listen`

### 描述

作为以太网 TCP 通信中的服务器，它为来自客户端的连接请求做好准备。  
在 UDP 点对点通信中不使用。

### 语法

`{ENet object}.listen [{backlog}]`

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
      <td>backlog</td>
      <td>
        未被接受的待处理连接的允许连接数。<br>
        如果不指定，则无限期等待。
      </td>
      <td></td>
    </tr>
  </tbody>
</table>

### 返回值

<table>
  <thead>
    <tr>
      <th style="text-align:left">值</th>
      <th style="text-align:left">含义</th>
      <th style="text-align:left">其他</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>
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


### 示例

```python
enet_to_sensor.listen
enet_to_sensor.accept 5000,*TimeOut
```