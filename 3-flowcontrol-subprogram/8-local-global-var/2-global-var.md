# 3.8.2 全局变量

### 描述

另一方面，定义为全局的全局变量可以始终从所有作业程序中访问。如果全局变量已经定义，即使通过结束语句或主程序的 R0 \[Enter\] 操作重置程序循环，也不会被清除。

### 示例

如果首先执行全局 x，将创建一个变量 x，并将其值初始化为默认值 0。然后，它将在下一行增加到 1。如果在下一个程序循环中再次执行全局 x，则不会再次定义，而是保留值 1，因为 x 已经被定义。另一方面，全局 y=10 将进行定义和赋值，因此当在下一个程序循环中执行时，变量 y 的值将重置为 10。

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
        <p>end
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

因此，如果要将全局变量用作程序循环次数的计数器，则不应在定义时赋值。

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
        <p>end
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
        <p>global count
          <br />
        </p>
        <p>count=count+1
          <br />
        </p>
        <p>&#x2026;
          <br />
        </p>
        <p>end</p>
      </td>
    </tr>
  </tbody>
</table>