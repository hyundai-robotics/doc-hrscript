# 6.3.2 `input`

### 描述

使用 `input` 语句作为教导挂件的按键输入字符串并将其存储在变量中。如果超时未输入，则继续执行以下语句或跳转到超时地址。

### 语法

```python
input <variable>;[,<timeout>,<timeout address>]
```

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
      <td style="text-align:left">variable</td>
      <td style="text-align:left">
        <p>接收输入的变量。数字也作为字符串类型输入。如果需要数值，请转换为 int( ) 或 double( ) 函数。
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">timeout</td>
      <td style="text-align:left">最大时间限制</td>
      <td style="text-align:left">0.1~60.0 秒
        <br />
      </td>
    </tr>
    <tr>
      <td style="text-align:left">timeout address</td>
      <td style="text-align:left">超时超过时跳转的地址</td>
      <td style="text-align:left">address</td>
    </tr>
  </tbody>
</table>

### 示例

```python
input work_no
input work_no,10
input work_no,10,*timeout
```
![](../../_assets/image_6.png)