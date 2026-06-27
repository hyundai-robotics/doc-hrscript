# `read_num`

### Description

从二进制缓冲区的指定位置读取数值，并返回该值。

### Syntax

`{BBuf object}.read_num {format},{offset}`

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
      <td style="text-align:left">format</td>
      <td style="text-align:left">二进制数据格式<sup>*</sup><br>
      例如 "U4", "s2"<br>
      </td>
      <td style="text-align:left">string</td>
    </tr>
	 <tr>
      <td style="text-align:left">offset</td>
      <td style="text-align:left">
        读取数据的位置 (0-based byte offset)
      </td>
      <td style="text-align:left">integer</td>
    </tr>
  </tbody>
</table>

<br>

\* 请参见 [7.4.2 Supported format](../2-format.md).
<br>
<br>

### Return value

* 读取的数值
* 如果在读取数据类型时发生错误，则返回 0。

### Example

```python
var bbuf=enet.BBuf()
bbuf.append("F8", 9.80665)
bbuf.append("U4", [2, 3, 5, 7, 11, 13])
print bbuf.read_num("F8", 0) # "9.80665"
print bbuf.read_num("U4", 12) # "3"
print bbuf.read_num("U4", 16) # "5"
```