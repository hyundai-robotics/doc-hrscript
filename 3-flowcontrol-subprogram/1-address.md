# 3.1 Address

Moving to another position in the program without executing the next line in order is called a "branch."
The address is the destination of the branch.

There are three ways to define addresses:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Format</th>
      <th style="text-align:left">Example</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">line-number</td>
      <td style="text-align:left">
        An integer between 1~9999. It can be attached to the left of a statement, not a step.
      </td>
      <td style="text-align:left">99</td>
    </tr>
    <tr>
      <td style="text-align:left">label</td>
      <td style="text-align:left">
        A label is not a syntax you attach to a statement, it is a statement in itself.<br>
        It is in the form of \* followed by [identifier](2-identifier.md). However, the identifier must not be longer than 128 characters.
      </td>
      <td style="text-align:left">*timeout</td>
    </tr>
    <tr>
      <td style="text-align:left">step number</td>
      <td style="text-align:left">
        Step number is automatically attached on steps being incremented by one.<br>
        It is in the form of S followed by a number of step. You can specify S1~S999.
      </td>
      <td style="text-align:left">S15</td>
    </tr>
  </tbody>
</table>


In the example below, `10` in the second statement is the line-number, `*err_handle` is the label, and `S12` is the step number.

```python
     move P,po3,spd=80%,accu=1,tool=3 until do33
  10 z_pos = (base_height+offset)*1.05
     # robot has to wait sensor2 input
     *err_handle
S12  move P,spd=80%,accu=1,tool=3
```



