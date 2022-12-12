# 7.3.1 ENet creator

### Description

Create an Ethernet object. Returns the reference of the created object.

### Syntax

`ENet({protocol})`

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
      <td>protocol</td>
      <td>
        "tcp" : TCP comm.<br>
        "udp" : UDP comm.<br>
        If omitted, recognized as "udp".</td>
    </tr>
  </tbody>
</table>

### Return value

Reference of the created object.

### Example

```python
enet0 = ENet()
var tcp = ENet("tcp")
```
