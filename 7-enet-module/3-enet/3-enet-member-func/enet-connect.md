# `连接 (connect)`

### 描述


作为以太网TCP通信中的客户端，它尝试连接到服务器。
在UDP点对点通信中不使用。

### 语法

`{ENet object}.connect [{等待时间}] [, {超时地址}]`


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
        超时。如果经过，继续下一个命令或跳转到超时地址。<br>
        如果未指定，则无限期等待。
      </td>
      <td>毫秒</td>
    </tr>
    <tr>
      <td>超时地址</td>
      <td>
        超时后跳转到的地址。<br>
        如果未指定，则继续下一个命令。
      </td>
      <td>地址</td>
    </tr>
  </tbody>
</table>


### 返回值

<table>
  <thead>
    <tr>
      <th style="text-align:left">值</th>
      <th style="text-align:left">意义</th>
      <th style="text-align:left">其他</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>
        OK (已完成)
      </td>
      <td></td>
    </tr>  
    <tr>
      <td>0</td>
      <td>
        等待
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

```python
var ret=enet_to_sensor.connect(5000)
```

```python
enet_to_sensor.connect 5000,*TimeOut
```