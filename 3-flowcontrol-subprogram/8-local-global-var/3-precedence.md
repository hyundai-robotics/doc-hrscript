# 3.8.3 Precedence

When there are local variables and global variables with an identical name, the local variable will be accessed preferentially. For example, while 0005.job is executed, as shown below, the global variable x and the local variable x will exist concurrently. At this time, if you read the x value, the local variable will also be read. After 0005.job returns to 0001.job, if you read the x value, the global variable will be read because only the global variable is present.

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

