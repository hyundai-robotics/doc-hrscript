# `添加 (append)`

### Description

将指定格式的数据附加到二进制缓冲区。

### Syntax

`{BBuf object}.append {format},{data}`

### Parameters

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
      <td style="text-align:left">format</td>
      <td style="text-align:left">二进制格式<sup>*</sup><br>
      例如 "U4", "s2"
      </td>
      <td style="text-align:left">字符串</td>
    </tr>
    <tr>
      <td style="text-align:left">data</td>
      <td style="text-align:left">
        要附加到二进制缓冲区的数据
      </td>
      <td style="text-align:left">原始数据,<br>或原始数据的1-D数组</td>
    </tr>
  </tbody>
</table>

<br>

* 请参阅 [7.4.2 支持的格式](../2-format.md)。
* 如果数据与指定格式类型不同，将自动隐式转换类型。例如，如果格式为 "s2"（2字节整数），而数据为浮点值 3.7，则整数值 3(0x0003) 将附加到缓冲区。相反，如果格式为 "f4"（4字节实数），而数据为整数值 -3，则实值 -3.0(0xC0400000) 将存储在缓冲区中。
* 如果格式为无符号，而数据为负数，则会发生错误，因此请小心。

<br>

### Return value

附加的数据数量。

### Example

```python
var bbuf=enet.BBuf()
bbuf.append("F8", 9.80665)
bbuf.append("U4", [2, 3, 5, 7, 11, 13])
```