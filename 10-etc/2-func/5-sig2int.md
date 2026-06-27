# 10.2.5 `sig2int`

使用 `sig2int` 函数，可以将特定范围的输入/输出信号表示为 `int` 类型值。

### 描述
- 输入要表示为 `int` 类型的输入/输出信号名称。
- 设置从输入/输出信号中读取多少位。

### 语法

```python
result=sig2int(<input/output signal>,<number of bits>)
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
      <td style="text-align:left">input/output signal</td>
      <td style="text-align:left">
        输入/输出信号变量名
      </td>
      <td style="text-align:left">输入/输出信号变量</td>
    </tr>
    <tr>
      <td style="text-align:left">number of bits</td>
      <td style="text-align:left">
        从输入/输出信号读取的位数
      <td style="text-align:left">变量</td>
    </tr>
  </tbody>
</table>

### 示例

```python
     var result1,result2,result3
     result1=sig2int(di4,4)
     result2=sig2int(fb2.do0,1)
     result3=sig2int(fn1.di24,8)
     end
```