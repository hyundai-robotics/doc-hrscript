# 3.2.4 wait

### Description

Makes it possible to move to the next command statement after waiting until a designated condition becomes true.

### Syntax

wait &lt;condition&gt;\[,&lt;timeout&gt;,&lt;timeout address&gt;\]

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
      <td style="text-align:left">Condition</td>
      <td style="text-align:left">Conditions in which waiting is required</td>
      <td style="text-align:left">Conditional expr</td>
    </tr>
    <tr>
      <td style="text-align:left">Timeout</td>
      <td style="text-align:left">Maximum time limit during which waiting will occur when the condition
        is false (timeout)</td>
      <td style="text-align:left">
        <p>Arithmetic expression</p>
        <p>0.1~60.0 sec</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">timeout address</td>
      <td style="text-align:left">Address to which branching will be made when the timeout is exceeded.</td>
      <td
      style="text-align:left">address</td>
    </tr>
  </tbody>
</table>

### Example

```python
wait sensor_ok
wait (sensor_ok and pos_ok),10,*timeout
```

