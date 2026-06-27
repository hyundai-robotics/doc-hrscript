# 7.3.1 `ENet` 创建者

### 描述

创建一个以太网对象。返回创建对象的引用。

### 语法

`ENet({protocol})`

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
      <td>protocol</td>
      <td>
        "tcp" : TCP 通信。<br>
        "udp" : UDP 通信。<br>
        如果省略，将被识别为 "udp"。</td>
    </tr>
  </tbody>
</table>

### 返回值

创建对象的引用。

### 示例

```python
enet0 = ENet()
var tcp = ENet("tcp")
```