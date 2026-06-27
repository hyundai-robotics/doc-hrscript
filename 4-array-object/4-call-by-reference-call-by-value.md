# 4.4 引用调用和值调用

在第 3.4 节中给出的 `call` 语句和 `jump` 语句的描述中，解释了形式参数和实际参数的概念。当实际参数被传送到子程序时，如果子程序在更改参数的值后结束，这些更改会反映到主程序中吗？

例如，假设有一个子程序 `0005_pow3.job` 将一个值提升到立方，如下所示：

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
      <td style="text-align:left">结果</td>
      <td style="text-align:left">2</td>
    </tr>
  </tbody>
</table>

虽然我们预计输出应该是 8，因为 2x2x2 等于 8，但结果却是 2。这是因为，当一个数值类型的实际参数被传送到子程序时，值是作为参数被复制的。换句话说，在 \(1\) 中，由于立方的值被赋值给了复制版本，因此没有影响原参数 x 的值。

因此，教学程序应进行修正，以便通过返回语句传送结果值。

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
      <td style="text-align:left">结果</td>
      <td style="text-align:left">8</td>
    </tr>
  </tbody>
</table>

另一方面，在数组或对象的情况下，传送的是实际参数的引用，而不是复制版本。引用指的是参数的位置。

在下面的例子中，子程序 0006\_pow3.job 将数组的每个元素的立方值提升，实际参数数组的元素值被更改。

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
      <td style="text-align:left">结果</td>
      <td style="text-align:left">[27, 8, 64]</td>
    </tr>
  </tbody>
</table>

当调用子程序时，如果传送的是实际参数值的复制版本，则称为值调用；如果传送的是引用，则称为引用调用。是否为值调用或引用调用由以下值的类型决定：

|  |  |
| :--- | :--- |
| 值调用 | 布尔、数值和字符串类型 |
| 引用调用 | 数组和对象类型 |

![](../_assets/image_3.png)