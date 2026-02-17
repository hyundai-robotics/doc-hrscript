# 3.8.2 全局变量

### 描述

另一方面，定义为全局的全局变量始终可以从所有作业程序中访问。如果一个全局变量被定义，它在程序周期通过结束语句或主程序的 R0 \[Enter\] 操作重置时不会被清除。

### 示例

如果全局 x 首次被执行，变量 x 将被创建，并且值将初始化为默认值 0。然后，它将在下一行增加到 1。如果在下一个程序周期再次执行全局 x，它不会再次被定义，值 1 将被保留，因为 x 已经被定义。另一方面，global y=10 将执行定义和赋值，因此当它在下一个程序周期中被执行时，变量 y 的值将重置为 10。

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
        <p>global x
          <br />
        </p>
        <p> 在 x=2 的情况下
          <br />
        </p>        
        <p>x=x+1 # 3
          <br />
        </p>
        <p>call 107
          <br />
        </p>
        <p>print x, y # 4, 10
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
        <p>global y=10
          <br />
        </p>
        <p>print x, y # 3, 10
<br />
        </p>
        <p>x=x+1 # 4
          <br />
        </p>
        <p>结束
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

因此，如果要将全局变量用作程序循环次数的计数器，则不应在定义时分配任何值。

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>错误
          <br />
        </p>
        <p>教学
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>global count=0
          <br />
        </p>
        <p>count=count+1
          <br />
        </p>
        <p>&#x2026;
          <br />
        </p>
        <p>结束
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>正确
          <br />
        </p>
        <p>教学
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>全局计数
          <br />
        </p>
        <p>count=count+1
          <br />
        </p>
        <p>&#x2026;
          <br />
        </p>
        <p>结束</p>
      </td>
    </tr>
  </tbody>
</table>