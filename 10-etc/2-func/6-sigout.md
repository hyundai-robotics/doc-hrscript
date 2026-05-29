# 10.2.6 `sigout`

Using the `sigout` function, You can output a specific range of the output signal by specifying it as an `int` type value.

Supported from V70.02-00

### Description
- Enter the name of the output signal to use as the start.
- Set how many bits to output.
- Set the value to be output.

### Syntax

```python
result=sigout(<output signal>,<number of bits>,<output value>)
```

### Parameters
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
      <td style="text-align:left">output signal</td>
      <td style="text-align:left">
        output signal variable name (bit)
      </td>
      <td style="text-align:left">output signal variable</td>
    </tr>
    <tr>
      <td style="text-align:left">number of bits</td>
      <td style="text-align:left">
        Number of bits of the signal to be output
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">output value</td>
      <td style="text-align:left">
        Value to output
      <td style="text-align:left">variable</td>
    </tr>
  </tbody>
</table>

### Sample

```python
     var result1,result2,result3
     result1=sigout(do4,4,7)
     result2=sigout(fb2.do0,2,2)
     result3=sigout(fn1.do24,8,55)
     end
```

