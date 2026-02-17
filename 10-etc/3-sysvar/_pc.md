# `_pc`

### 描述

`_pc` 用于获取当前程序计数器信息。 <br>
程序计数器由程序编号、步骤编号和功能编号组成。

### 语法

```python
var sno=_pc.cur_sno  # 分配当前步骤编号
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">项</th>
      <th style="text-align:left">含义</th>
      <th style="text-align:left">其他</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">cur_sno</td>
      <td style="text-align:left">
         光标当前所在的步骤编号
      </td>
      <td style="text-align:left">变量</td>
    </tr>
  </tbody>
</table>




### `cur_sno` 示例：如果未满足条件，则移动到上一个步骤。

```python
   S6 move P,spd=50%,accu=3,tool=1,until di6
      if (result()==0)
        goto S[_pc.cur_sno-1]
      endif
   S7 move P,spd=50%,accu=3,tool=1,until di7
      if (result()==0)
        goto S[_pc.cur_sno-1]
      endif
   S8 move P,spd=50%,accu=3,tool=1,until di8
      if (result()==0)
        goto S[_pc.cur_sno-1]
      endif
   ...
```
