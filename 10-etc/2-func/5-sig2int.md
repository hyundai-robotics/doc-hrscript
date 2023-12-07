# 10.2.5 sig2int

Using the sig2int function, a specific range of input/output signals can be expressed as an int type value.

### Description
- Enter the name of the input/output signal to be expressed in int type.
- Set how many bits to read from input/output signals.

### Syntax

```python
result=sig2int(<input/output signal>,<number of bits>)
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
      <td style="text-align:left">input/output signal</td>
      <td style="text-align:left">
        input/output signal variable name
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">number of bits</td>
      <td style="text-align:left">
        Number of bits to read from input/output signals
      <td style="text-align:left">variable</td>
    </tr>
  </tbody>
</table>

### Sample

```python
     var result1,result2,result3
     result1=sig2int(di4,4)
     result2=sig2int(fb2.0,1)
     result3=sig2int(fn1.24,8)
     end
```

