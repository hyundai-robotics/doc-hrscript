# 6.2.1 Constructor

### Description

It creates an Ethernet object and returns the reference

### Syntax

ENet\(&lt;protocol&gt;\)

### Parameter

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">protocol</td>
      <td style="text-align:left">
        <p>&quot;tcp&quot; : TCP communication
          <br />
        </p>
        <p>&quot;udp&quot; : UDP communication
          <br />
        </p>
        <p>
          <br />
        </p>
        <p>
          <br />
        </p>
      </td>
      <td style="text-align:left">If omitted, it will be recognized as &quot;udp.&quot;</td>
    </tr>
  </tbody>
</table>

### Return Value

Reference of the created object

### Example

```python
enet0 = ENet()
var tcp = ENet("tcp")
```



