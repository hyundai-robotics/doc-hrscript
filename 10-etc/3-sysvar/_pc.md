# `_pc`

### Description

`_pc` 用于获取当前程序计数器信息。<br>
程序计数器由程序号、步骤号和功能号组成。

### Syntax

```python
var sno=_pc.cur_sno  # 分配当前步骤号
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">item</th>
      <th style="text-align:left">meaning</th>
      <th style="text-align:left">etc</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">cur_sno</td>
      <td style="text-align:left">
         光标当前所在的步骤号
      </td>
      <td style="text-align:left">变量</td>
    </tr>
  </tbody>
</table>




### `cur_sno` sample : 如果直到条件不满足，移动到上一个步骤。

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