# 3.3.1 `goto`

### 描述

使得能够转到指定地址。

### 语法

goto &lt;address&gt;

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">address</td>
      <td style="text-align:left">
        分支地址<br/>
        对于行号，可以使用算术表达式。
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### 示例

```python
goto 99
goto addr
goto *err_hdl
```