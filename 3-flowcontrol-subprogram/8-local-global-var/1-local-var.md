# 3.8.1 局部变量

### 描述

示例仅使用 var 语句定义的局部变量进行描述。局部变量是在一个作业程序中通过 var 语句创建的，并在程序结束后自动销毁。此外，其他程序无法读取或写入它们的值。

### 示例

"main\_v" 是一个仅在 0001.job 中可访问的局部变量，"sub\_v" 是一个仅在 0107.job 中可访问的局部变量。从其他程序尝试访问它会导致错误。

局部变量 "x" 同时在 0001.job 和 0107.job 中定义。在两个程序中分别定义的局部变量 "x" 同名但不同。因此，在子程序 0107 中为变量 "x" 设置的值 5，在返回主程序 0001 后将打印 3，而不是 5。

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
        <p>打印 sub_v # ok
          <br />
        </p>
        <p>打印 main_v # error
          <br />
        </p>
        <p>x=5
          <br />
        </p>
        <p>结束</p>
      </td>
    </tr>
  </tbody>
</table>