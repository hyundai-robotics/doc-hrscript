# 3.2.4 `等待 (wait)`

### 描述

在指定条件变为真之前，等待后使其能够移动到下一个命令语句。

### 语法

wait &lt;condition&gt;\[,&lt;timeout&gt;,&lt;timeout address&gt;\]

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
      <td style="text-align:left">条件</td>
      <td style="text-align:left">需要等待的条件</td>
      <td style="text-align:left">条件表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">超时</td>
      <td style="text-align:left">当条件为假时，等待发生的最大时间限制（超时）</td>
      <td style="text-align:left">
        <p>算术表达式</p>
        <p>0.1~60.0 秒</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">超时地址</td>
      <td style="text-align:left">超时超过时将跳转到的地址。</td>
      <td
      style="text-align:left">地址</td>
    </tr>
  </tbody>
</table>

### 示例

```python
wait sensor_ok
wait (sensor_ok and pos_ok),10,*timeout
```