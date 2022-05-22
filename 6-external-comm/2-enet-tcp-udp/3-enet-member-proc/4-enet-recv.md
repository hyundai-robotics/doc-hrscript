# recv

### Description

Receives the values to the set Ethernet object

### Syntax

&lt;ENet object&gt;.recv &lt;variable&gt;\[, &lt;waiting time&gt;\]



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
      <td style="text-align:left">Variable</td>
      <td style="text-align:left">A variable to which the received string is to be passed</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Waiting time</td>
      <td style="text-align:left">
        <p>Time of time-out
          <br />
        </p>
        <p>
          <br />
        </p>
        <p>
          <br />
        </p>
        <p>
          <br />
        </p>
      </td>
      <td style="text-align:left">msec</td>
    </tr>
  </tbody>
</table>

### Example

```python
enet_to_sensor.recv  msg, 5000
```

