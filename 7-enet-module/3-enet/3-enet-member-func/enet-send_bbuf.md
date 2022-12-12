# send_bbuf

### Description

Send [BBuf](../../4-bbuf/README.md) object to ethernet object.


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
        binary buffer object to send.
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>


### Return value

The number of bytes sent.


### Example

```python
var bbuf=enet.BBuf()
var arr=[ -3, 0, 1 ]
bbuf.append("s4", arr)
var nitem=cli.send_bbuf(bbuf)
```
