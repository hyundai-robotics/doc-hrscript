# 2.9.4 构造函数

这些函数接收参数输入，然后创建并返回一个对象。

<table>
  <thead>
    <tr>
      <th style="text-align:left">函数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">用法示例</th>
      <th style="text-align:left">结果</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>Array(n)</p>
        <p>Array(a, b, c)</p>
      </td>
      <td style="text-align:left">
        <p>创建并返回一个包含“n”个元素的数组</p>
        <p>元素的初始值为0。</p>
        <p>如果指定两个或更多元素，则会创建一个多维数组。</p>
        <p>参见 &quot;<a href="../../4-array-object/1-array/3-array-creator">4.1.3 数组构造函数 - Array()</a>&quot;。</p>
      </td>
      <td style="text-align:left">
        <p>Array(900)</p>
        <p>Array(3,4)</p>
      </td>
      <td style="text-align:left">
        <p>Array [900]</p>
        <p>Array [3] [4]</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Pose(element)</td>
      <td style="text-align:left">
        <p>创建并返回一个姿态对象</p>
        <p>参见 &quot;<a href="../../5-moving-robot/1-pose.md">5.1 姿态</a>&quot;。</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">姿态对象</td>
    </tr>
    <tr>
      <td style="text-align:left">Shift(element)</td>
      <td style="text-align:left">
        <p>创建并返回一个位移对象</p>
        <p>参见 &quot;<a href="../../5-moving-robot/2-shift.md">5.2 位移</a>&quot;。</p>
      </td>
      <td style="text-align:left"></td>
<td style="text-align:left">移动对象</td>
    </tr>
  </tbody>
</table>