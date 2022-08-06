# 3.7.3 jump

### Description

This format is completely identical to that of call statements, and its action is also similar to that of **call** statements.

The only difference is that, while a **call** statement returns to the main program using an end program, a **jump** statement does not.

### Syntax

```python
jump <job number or file name> [,parameter 1,parameter 2,…]
```



### Example

If the jump statement of this example program is replaced with a **call** statement, the result of the replaced program will be as follows. When the **end** of the sub-program \(0102\_err\) is encountered, the action cycle will end. If the next action cycle is executed, the main program \(0001\) will be executed from the start.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>print &quot;main job start&quot;
          <br />
        </p>
        <p>jump 102_err
          <br />
        </p>
        <p>print &quot;main job end&quot;
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0102_err.job</td>
      <td style="text-align:left">
        <p>print &quot;sub-program&quot;
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Result</td>
      <td style="text-align:left">
        <p>main job start
          <br />
        </p>
        <p>sub-program
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>



