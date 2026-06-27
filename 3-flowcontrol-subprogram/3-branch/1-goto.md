# 3.3.1 `goto`

### Description

使能够跳转到指定地址。

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
        分支地址<br/>
        在行号的情况下，允许使用算术表达式。
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