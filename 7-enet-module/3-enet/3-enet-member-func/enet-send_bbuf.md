# `send_bbuf`

### Description

发送 [BBuf](../../4-bbuf/README.md) 对象到以太网对象。


### Syntax

`{ENet object}.send_bbuf {BBuf object}`


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
      <td style="text-align:left">BBuf object</td>
      <td style="text-align:left">
        要发送的二进制缓冲区对象。
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>


### Return value

发送的字节数。


### Example

```python
var bbuf=enet.BBuf()
var arr=[ -3, 0, 1 ]
bbuf.append("s4", arr)
var nitem=cli.send_bbuf(bbuf)
```