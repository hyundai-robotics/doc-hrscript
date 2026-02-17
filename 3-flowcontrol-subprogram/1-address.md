# 3.1 地址

在程序中移动到另一个位置而不按顺序执行下一行称为“分支”。
地址是分支的目的地。

定义地址有三种方法：

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
        介于 1~9999 之间的整数。可以附加在语句的左侧，而不是步骤。
      </td>
      <td style="text-align:left">99</td>
    </tr>
    <tr>
      <td style="text-align:left">标签</td>
      <td style="text-align:left">
        标签不是附加在语句上的语法，而是语句本身。<br>
        其形式为 \* 后跟 [标识符](2-identifier.md)。但标识符不得超过 128 个字符。
      </td>
      <td style="text-align:left">*timeout</td>
    </tr>
    <tr>
      <td style="text-align:left">步骤编号</td>
      <td style="text-align:left">
        步骤编号在步骤递增时自动附加。<br>
        其形式为 S 后跟步骤编号。可以指定 S1~S999。
      </td>
      <td style="text-align:left">S15</td>
    </tr>
  </tbody>
</table>


在下面的示例中，第二个语句中的 `10` 是行号，`*err_handle` 是标签，`S12` 是步骤编号。

```python
     move P,po3,spd=80%,accu=1,tool=3 until do33
  10 z_pos = (base_height+offset)*1.05
     # robot has to wait sensor2 input
     *err_handle
S12  move P,spd=80%,accu=1,tool=3
```
