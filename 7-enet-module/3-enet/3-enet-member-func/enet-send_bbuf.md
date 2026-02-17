# `send_bbuf`

### 描述

将 [BBuf](../../4-bbuf/README.md) 对象发送至以太网对象。


### 语法

`{ENet object}.send_bbuf {BBuf object}`


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
      <td style="text-align:left">BBuf 对象</td>
      <td style="text-align:left">
        要发送的二进制缓冲区对象。
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>


### 返回值

发送的字节数。


### 示例

```python
var bbuf=enet.BBuf()
var arr=[ -3, 0, 1 ]
bbuf.append("s4", arr)
var nitem=cli.send_bbuf(bbuf)
```