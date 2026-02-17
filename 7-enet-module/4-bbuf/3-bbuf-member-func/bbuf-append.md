# `附加 (append)`

### 描述

将指定格式的数据附加到二进制缓冲区。

### 语法

`{BBuf object}.append {format},{data}`

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

* 查看[7.4.2 支持的格式](../2-format.md)。
* 如果数据类型与指定格式不同，则会隐式执行自动类型转换。例如，如果格式为"s2"（2字节整数）且数据为浮点值3.7，则整数值3(0x0003)将附加到缓冲区。反之，如果格式为"f4"（4字节实数）且数据为整数值-3，则实值-3.0(0xC0400000)将存储在缓冲区中。
* 如果格式为无符号且数据为负数，则会发生错误，因此请小心。

<br>
### 返回值

附加的数据数量。


### 示例

```python
var bbuf=enet.BBuf()
bbuf.append("F8", 9.80665)
bbuf.append("U4", [2, 3, 5, 7, 11, 13])
```