# 4.2 对象

如前所述，发现数组可以存储多个元素值，并通过索引访问。

对象与数组类似，都是存储多个元素值。不同之处在于，对象是通过键访问的，而不是通过索引。此外，键是字符串，而不是数字。

对象的定义方式为 `var` 或 `global`，与其他变量相同。对象的定义和访问格式如下。

|  |  |
| :--- | :--- |
| 定义 | var object name = { key : value, key : value, ...} |
| 访问 | 对象名 键 |




以下是一个定义和访问对象的示例。

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
        <p>var gap = { x:200, y:152.6 }</p>
        <p>gap.x = gap.x + 10</p>
        <p>print gap.x, gap.y</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">结果</td>
      <td style="text-align:left">210 152.6</td>
    </tr>
  </tbody>
</table>



对象的键必须是标识符格式，但元素的值可以是任何类型，也可以是不同类型。

对象可以包含其他对象或数组作为其元素。同样，数组也可以包含其他数组或对象作为其元素。在以下示例中，“work”是一个对象，包含“size”，这是一个对象，以及“heights”，这是一个数组。

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
        <p>var work = { part_no:3, name: &quot;齿轮&quot;, tested : false</p>
        <p>, size : { x : 150, y : 80 }</p>
        <p>, heights : [ 72.89, 74.91, 81.03, 87.60, 87.11 ] }</p>
        <p>print work.tested, work.size.y, work.heights[3]</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">结果</td>
      <td style="text-align:left">false, 80, 87.600000</td>
    </tr>
  </tbody>
</table>