# 6.3.1 `print`

### Description

`print` 语句将字符串打印到教导挂件的引导条上。除了字符串常量外，任何类型的表达式（包括常量和变量）结果都将转换为字符串并打印出来。如果指定多个表达式，则每个表达式之间用一个空格字符分隔打印。

### Syntax

```python
print <expression>[,<expression>,<expression>...]
```

### Parameter

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">expression</td>
      <td style="text-align:left">
        <p>要打印的表达式。<br>
        支持所有类型的布尔值、数字、字符串、数组、对象。
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### Example

```python
input work_no
input work_no,10
input work_no,10,*timeout
```