# 3.7.1 call

### Description

There is no significant difference in format between the main program and the subprogram in HRScript. The first job executed by the start button or by a signal is the main program, and all other jobs called by the **call** statement are subprograms. 

### Syntax

```python
call <job number or file name> [,parameter 1,parameter 2,…]
```

Specify the job number of the job file name \(excluding the extension\) after the **call** statement. Then, while program A is being executed, if call B is encountered, A’s execution will be stopped, and the first statement of program B, a subprogram, will continue to be executed. If the **end** statement is encountered while B is being executed, program A’s execution will continue upon returning to the position of the next statement of program A’s **call** statement that was previously called.

### Example

The following shows an example and the result of a subprogram called by a **call** statement. It seems meaningless to divide the program into two because the subprogram must handle only one print statement. However, a more practical example will be shown later.

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
        <p>call 102_err
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
        <p>main job end
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

