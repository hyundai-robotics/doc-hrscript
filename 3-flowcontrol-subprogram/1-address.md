# 3.1 地址

在程序中不按顺序执行下一行而跳转到另一个位置称为“分支”。
地址是分支的目标。

定义地址有三种方式：

<table>
  <thead>
    <tr>
      <th style="text-align:left">类型</th>
      <th style="text-align:left">格式</th>
      <th style="text-align:left">示例</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">行号</td>
      <td style="text-align:left">
        介于 1~9999 之间的整数。可以附加在语句的左侧，而不是步骤上。
      </td>
      <td style="text-align:left">99</td>
    </tr>
    <tr>
      <td style="text-align:left">标签</td>
      <td style="text-align:left">
        标签不是你附加在语句上的语法，而是它本身就是一条语句。<br>
        形式为 * 后跟 <a href="../2-basic-syntax/2-identifier">标识符</a>。但是，标识符不能超过 128 个字符。
      </td>
      <td style="text-align:left">*timeout</td>
    </tr>
    <tr>
      <td style="text-align:left">步骤号</td>
      <td style="text-align:left">
        步骤号会自动附加在递增一步的步骤上。<br>
        形式为 S 后跟步骤的数字。你可以指定 S1~S999。
      </td>
      <td style="text-align:left">S15</td>
    </tr>
  </tbody>
</table>


在下面的示例中，` (10)` 在第二条语句中是行号，`*err_handle` 是标签，`S12` 是步骤号。

```python
     move P,po3,spd=80%,accu=1,tool=3 until do33
  10 z_pos = (base_height+offset)*1.05
     # 机器人必须等待传感器2的输入
     *err_handle
S12  move P,spd=80%,accu=1,tool=3
```