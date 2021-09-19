# state

### Description

Returns the state of the Ethernet object

### Syntax

&lt;ENet object&gt;.state\(\)



### Return Value

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
      <td style="text-align:left">1</td>
      <td style="text-align:left">
        <p>Connected
          <br />
        </p>
        <p>(In the case of UDP, just opening it will be considered a connection.
          In the case of TCP, connecting after opening will be considered a connection.)
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
        <p>
          <br />
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">0</td>
      <td style="text-align:left">Not connected</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">-1</td>
      <td style="text-align:left">Failed to create the Ethernet socket</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">-2</td>
      <td style="text-align:left">Failed to bind the Ethernet device</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### Example

```python
ret = enet_to_sensor.state()
```

