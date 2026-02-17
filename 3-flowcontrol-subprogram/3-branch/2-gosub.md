# 3.3.2 `gosub`~`retsub`

### 描述

当遇到 `gosub` 语句时，它会跳转到指定的地址。当遇到 `retsub` 语句时，它会返回到 `gosub` 语句之后的下一个位置。`gosub` 可以嵌套多层，并且没有嵌套的数量限制。

### 语法
```python
gosub <address>
...
end
  
<address>
...  
retsub
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
      <td style="text-align:left">address</td>
      <td style="text-align:left">
        <p>要跳转的地址</p>
        <p>在行号的情况下，可以使用算术表达式。</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### 示例

```python
var x=5
var y=6
var res
var sum=0
gosub *calc_dist1
gosub *calc_dist2
var total=sum
if near(total,18.8102)
  print "OK"
else
  print "NG"
endif
end
     
*calc_dist1
res=x*x+y*y
res=sqr(res)
gosub *calc_sum
retsub
     
*calc_dist2
res=x+y
gosub *calc_sum
retsub
     
*calc_sum
sum=sum+res
retsub
end
```
