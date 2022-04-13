# 4.4 Call-by-reference and call-by-value

In the description of call statements and jump statements given in Section 3.4, the concepts of formal parameters and actual parameters were explained. When an actual parameter has been transported to a sub-program, if the sub-program ends after changing the value of the parameter, will it be reflected to the main program?

For example, let’s assume that a sub-program 0005\_pow3.job raises a value to the third power as follows:



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
        <p>var x=2
          <br />
        </p>
        <p>call 0005_pow3,x
          <br />
        </p>
        <p>print x
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0005_pow3.job</td>
      <td style="text-align:left">
        <p>param p
          <br />
        </p>
        <p>var t=p
          <br />
        </p>
        <p>p=t*t*t # (1)
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Result</td>
      <td style="text-align:left">2</td>
    </tr>
  </tbody>
</table>

Although we expected that 8 is output because 2×2×2 is 8, the result is 2. It is because, when a numeric-type actual parameter is transported to a sub-program, the value is copied as a parameter. In other words, in \(1\), because the value raised to the third power was assigned to the copied version, it did not affect the value of the original parameter, x.

Therefore, the teaching program should be corrected so that the resulting value is transported by a return statement.



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
        <p>var x=2
          <br />
        </p>
        <p>call 0005_pow3,x
          <br />
        </p>
        <p>x=result()
          <br />
        </p>
        <p>print x
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0005_pow3.job</td>
      <td style="text-align:left">
        <p>param p
          <br />
        </p>
        <p>var t=p
          <br />
        </p>
        <p>p=t*t*t
          <br />
        </p>
        <p>return p
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Result</td>
      <td style="text-align:left">8</td>
    </tr>
  </tbody>
</table>

On the other hand, in the case of arrays or objects, the reference of actual parameters, not the copied versions, will be transported. A reference refers to the position of a parameter.

In the following example, where the sub-program 0006\_pow3.job raises each element of an array to the third power, the values of the elements of the actual parameter array are changed.



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
        <p>var x=[3, 2, 4]
          <br />
        </p>
        <p>call 0006_pow3,x
          <br />
        </p>
        <p>print x
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0006_pow3.job</td>
      <td style="text-align:left">
        <p>param p
          <br />
        </p>
        <p>var t
          <br />
        </p>
        <p>for i=0 to len(arr)-1
          <br />
        </p>
        <p>t=p[i]
          <br />
        </p>
        <p>p[i] = t*t*t
          <br />
        </p>
        <p>next
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Result</td>
      <td style="text-align:left">[27, 8, 64]</td>
    </tr>
  </tbody>
</table>

When a sub-program is called, if the copied version of the value of an actual parameter is transported, it is referred to as call-by-value; and if a reference is transported, it is referred to as call-by-reference. Whether it will be call-by-value or call-by-reference is determined by the type of values as follows:

|  |  |
| :--- | :--- |
| call-by-value | Boolean, numeric, and string types |
| call-by-reference | Array and object types |

![](../_assets/image%20%283%29%20%281%29.png)



