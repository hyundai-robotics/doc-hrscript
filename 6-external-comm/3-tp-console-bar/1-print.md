# 6.3.1 `print`

### 描述

`print` 语句将字符串打印到教导挂件的导引条上。除了字符串常量外，任何类型的表达式（包括常量和变量）都会被转换为字符串并打印出来。如果指定多个表达式，则每个表达式之间以单个空格字符分隔。

### 语法

```python
print <expression>[,<expression>,<expression>...]
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

### 示例

```python
input work_no
input work_no,10
input work_no,10,*timeout
```