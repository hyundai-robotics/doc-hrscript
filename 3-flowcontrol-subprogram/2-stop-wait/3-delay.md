# 3.2.3 `时间延迟 (delay)`

### 描述

在等待指定时间后，可以进展到下一个命令语句。

### 语法

delay &lt;time&gt;

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
      <td style="text-align:left">时间</td>
      <td style="text-align:left">等待时间</td>
      <td style="text-align:left">
        <p>算术表达式
          <br />
        </p>
        <p>0.1~60.0 秒
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

### 示例

```python
delay 3.5
```