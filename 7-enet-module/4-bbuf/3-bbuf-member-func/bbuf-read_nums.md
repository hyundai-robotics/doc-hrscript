# `read_nums`

### 描述

从二进制缓冲区中的指定位置读取指定数量的数值，并以数组格式返回它们。

### 语法

`{BBuf object}.read_num  {format},{offset},{n.item}`

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">名称</th>
      <th style="text-align:left">含义</th>
      <th style="text-align:left">杂项</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">format</td>
      <td style="text-align:left">
			二进制数据格式<sup>*</sup><br>
      例如 "U4", "s2"
      </td>
      <td style="text-align:left">字符串</td>
    </tr>
	  <tr>
      <td style="text-align:left">offset</td>
      <td style="text-align:left">
        读取数据的位置（基于0的字节偏移）
      </td>
      <td style="text-align:left">整数</td>
    </tr>
    <tr>
      <td style="text-align:left">n.item</td>
      <td style="text-align:left">
        要读取的数据数量
      </td>
      <td style="text-align:left">整数</td>
    </tr>
  </tbody>
</table>

<br>
\* 请参阅 [7.4.2 支持的格式](../2-format.md).
<br>
<br>


### 返回值

* 读取的数值数组。
* 如果缓冲区中的数据数量少于指定数量，则只读取可用数量。
* 如果在读取数据类型时发生错误，则返回空数组。


### 示例

```python
var bbuf=enet.BBuf()
bbuf.append("F8", 9.80665)
bbuf.append("U4", [2, 3, 5, 7, 11, 13])
print bbuf.read_nums("U4", 12, 3) # "[3, 5, 7]"
print bbuf.read_num("U4", 12, 6) # "[3, 5, 7, 11, 13]"
```