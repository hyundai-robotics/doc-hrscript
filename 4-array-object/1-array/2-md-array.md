# 4.1.2 Multidimensional Arrays

An array can also be nested as an element of an array. When accessing the elements of a multidimensional array, you can use the `[ ]` operator consecutively. In the following example, `arr_y` is a two-dimensional array. \(1\)

`arr_y[1]` is an array of elements of index 1, namely `["abc", "jqk", "xyz"]`, and it is assigned to the new variable `arr_x`. \(2\)

So, `arr_x[1]` is `jqk`, and `arr_y[1][2]` is `xyz` because it points to `[2]` of `arr_y[1]`.



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
        <p>var arr_y = [ [10,20], [&quot;abc&quot;,&quot;jqk&quot;, &quot;xyz&quot;]
          ] # (1)
          <br />
        </p>
        <p>var arr_x=arr_y[1] # (2)
          <br />
        </p>
        <p>print arr_x[1]
          <br />
        </p>
        <p>print arr_y[1][2]
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Result</td>
      <td style="text-align:left">
        <p>jqk
          <br />
        </p>
        <p>xyz
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

