# 3.3.1 goto

### Description

Makes it possible to go to a designated address.

### Syntax

goto &lt;address&gt;

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
      <td style="text-align:left">address</td>
      <td style="text-align:left">
        Address to branch<br/>
        An arithmetic expression is possible in the case of a line number.
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### Example

```python
goto 99
goto addr
goto *err_hdl
```



