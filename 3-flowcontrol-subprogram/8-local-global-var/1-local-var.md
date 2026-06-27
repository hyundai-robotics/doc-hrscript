# 3.8.1 局部变量

### 描述

例子仅使用通过 var 语句定义的局部变量的例子来描述。局部变量是在一个作业程序中通过 var 语句创建的，当程序在遇到结束语句后结束时，它们会被自动销毁。此外，其他程序无法读取或写入它们的值。

### 例子

"main\_v" 是一个仅在 0001.job 内部可访问的局部变量，而 "sub\_v" 是一个仅在 0107.job 内部可访问的局部变量。从另一个程序访问它将导致错误。

局部变量 "x" 在 0001.job 和 0107.job 中都被定义。分别在两个程序中定义的局部变量 "x" 名称相同但不同。因此，在子程序 0107 中为变量 "x" 设置的值 5 返回到主程序 0001 后将打印 3，而不是 5。

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