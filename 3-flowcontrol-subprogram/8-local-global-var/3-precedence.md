# 3.8.3 优先级

当存在具有相同名称的局部变量和全局变量时，将优先访问局部变量。例如，在执行 0005.job 时，如下所示，全局变量 x 和局部变量 x 将同时存在。这时，如果读取 x 的值，将读取局部变量。之后，0005.job 返回到 0001.job 时，如果读取 x 的值，将读取全局变量，因为此时只有全局变量存在。

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
        <p>global x=100
          <br />
        </p>
        <p>call 5
          <br />
        </p>
        <p>print x # 100
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0005.job</td>
      <td style="text-align:left">
        <p>var x=&quot;hello&quot;
          <br />
        </p>
        <p>print x # hello
          <br />
        </p>
        <p>end</p>
      </td>
    </tr>
  </tbody>
</table>