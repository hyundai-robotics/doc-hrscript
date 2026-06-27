# 4.1.2 多维数组

数组也可以作为数组的元素嵌套。当访问多维数组的元素时，可以连续使用`[ ]`运算符。在以下示例中，`arr_y`是一个二维数组。\(1\)

`arr_y[1]`是索引1的元素数组，即`["abc", "jqk", "xyz"]`，并将其分配给新变量`arr_x`。\(2\)

因此，`arr_x[1]`是`jqk`，而`arr_y[1][2]`是`xyz`，因为它指向`arr_y[1]`的`[2]`。

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
      <td style="text-align:left">结果</td>
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