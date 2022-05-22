# 3.8.1 Local Variables

### Description

Examples have been described only using the examples of local variables defined with the var statement. Local variables are created by a var statement in one job program and are automatically destroyed when the program ends after the encounter with the end statement. Moreover, their values cannot be read or written by other programs. 

### Example

“main\_v” is a local variable accessible only within 0001.job, and “sub\_v” is a local variable accessible only within 0107.job.   Attempting to access it from another program will cause an error. 

The local variable “x” is defined in both 0001.job and 0107.job. The local variable “x” respectively defined in both programs has the same name but are different. So the value 5 for the variable “x” is set in subprogram 0107, 3 will be printed instead of 5 after the return to main program 0001.



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
        <p>var main_v=10
          <br />
        </p>
        <p>var x=3
          <br />
        </p>
        <p>call 107
          <br />
        </p>
        <p>print main_v # ok
          <br />
        </p>
        <p>print sub_v # error
          <br />
        </p>
        <p>print x # 3 is printed
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0107.job</td>
      <td style="text-align:left">
        <p>var sub_v=20
          <br />
        </p>
        <p>var x
          <br />
        </p>
        <p>print sub_v # ok
          <br />
        </p>
        <p>print main_v # error
          <br />
        </p>
        <p>x=5
          <br />
        </p>
        <p>end</p>
      </td>
    </tr>
  </tbody>
</table>

