# send

### Description

Transmits the values to the set Ethernet object

### Syntax

&lt;ENet object&gt;.send &lt;value&gt;, &lt;value&gt;, …



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
      <td style="text-align:left">Value</td>
      <td style="text-align:left">
        <p>Data value to be output.
          <br />
        </p>
        <p>Arguments separated by commas will be printed separated by spaces.
          <br
          />
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
      <td style="text-align:left">All data types</td>
    </tr>
  </tbody>
</table>

### Example

```python
enet_to_sensor.send "rob:", 10, ", command:"+cmd, "\n"
```



