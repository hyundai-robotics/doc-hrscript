# `read_nums`

### Description

从二进制缓冲区的指定位置读取指定数量的数值，并以数组格式返回。


### Syntax

`{BBuf object}.read_num  {format},{offset},{n.item}`


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
      <td style="text-align:left">
			二进制数据格式<sup>*</sup><br>
      例如 "U4", "s2"
      </td>
      <td style="text-align:left">string</td>
    </tr>
	  <tr>
      <td style="text-align:left">offset</td>
      <td style="text-align:left">
        读取数据的位置（基于0的字节偏移量）
      </td>
      <td style="text-align:left">integer</td>
    </tr>
    <tr>
      <td style="text-align:left">n.item</td>
      <td style="text-align:left">
        要读取的数据数量
      </td>
      <td style="text-align:left">integer</td>
    </tr>
  </tbody>
</table>

<br>


\* 请参阅 [7.4.2 Supported format](../2-format.md).
<br>
<br>


### Return value

* 读取的数值数组。
* 如果缓冲区中的数据数量少于指定的数量，则仅读取可用的数量。
* 如果在读取数据类型时发生错误，则返回空数组。


### Example

```python
var bbuf=enet.BBuf()
bbuf.append("F8", 9.80665)
bbuf.append("U4", [2, 3, 5, 7, 11, 13])
print bbuf.read_nums("U4", 12, 3) # "[3, 5, 7]"
print bbuf.read_num("U4", 12, 6) # "[3, 5, 7, 11, 13]"
```