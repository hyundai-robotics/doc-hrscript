# 10.2.4 `rand`

您可以使用 `rand` 函数生成随机数。

### 描述
根据函数的参数，它生成一个介于 0 和 1 之间的随机实数，或者在指定范围内生成随机整数。

### 语法
```python
# 介于 0 和 1 之间的随机实数
v0=rand() 
```

```python
# 在指定范围内的随机整数
v1=rand(<minimum value>,<maximum value>) 
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
      <td style="text-align:left">minimum value</td>
      <td style="text-align:left">
        要生成的最小随机整数
      </td>
      <td style="text-align:left">整数常量</td>
    </tr>
    <tr>
      <td style="text-align:left">maximum value</td>
      <td style="text-align:left">
        要生成的最大随机整数
      <td style="text-align:left">整数常量</td>
    </tr>
  </tbody>
</table>

### 示例

```python
     var v0, v1
     var min=1
     var max=100
     v0=rand()          # 生成介于 0 和 1 之间的随机实数
     v1=rand(min,max)   # 生成介于 1 和 100 之间的随机整数
     end
```
