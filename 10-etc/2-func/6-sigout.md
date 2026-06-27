# 10.2.6 `sigout`

使用 `sigout` 函数时，您可以通过将其指定为 `int` 类型值来输出输出信号的特定范围。

支持版本： V70.02-00

### 描述
- 输入要用作起始的输出信号名称。
- 设置要输出的位数。
- 设置要输出的值。

### 语法

```python
result=sigout(<output signal>,<number of bits>,<output value>)
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
      <td style="text-align:left">output signal</td>
      <td style="text-align:left">
        输出信号变量名称 (bit)
      </td>
      <td style="text-align:left">输出信号变量</td>
    </tr>
    <tr>
      <td style="text-align:left">number of bits</td>
      <td style="text-align:left">
        要输出的信号的位数
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">output value</td>
      <td style="text-align:left">
        要输出的值
      <td style="text-align:left">变量</td>
    </tr>
  </tbody>
</table>

### 示例

```python
     var result1,result2,result3
     result1=sigout(do4,4,7)
     result2=sigout(fb2.do0,2,2)
     result3=sigout(fn1.do24,8,55)
     end
```