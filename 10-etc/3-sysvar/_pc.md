# `_pc`

### Description

`_pc` is used to obtain current program counter information. <br>
The program counter consists of a program number, a step number, and a function number.

### Syntax

```python
var sno=_pc.cur_sno  # Assign the current step number
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">item</th>
      <th style="text-align:left">meaning</th>
      <th style="text-align:left">etc</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">cur_sno</td>
      <td style="text-align:left">
         Step number where the cursor is currently located
      </td>
      <td style="text-align:left">variable</td>
    </tr>
  </tbody>
</table>




### `cur_sno` sample : If the until condition is not satisfied, move to the previous step.

```python
   S6 move P,spd=50%,accu=3,tool=1,until di6
      if (result()==0)
        goto S[_pc.cur_sno-1]
      endif
   S7 move P,spd=50%,accu=3,tool=1,until di7
      if (result()==0)
        goto S[_pc.cur_sno-1]
      endif
   S8 move P,spd=50%,accu=3,tool=1,until di8
      if (result()==0)
        goto S[_pc.cur_sno-1]
      endif
   ...
```

