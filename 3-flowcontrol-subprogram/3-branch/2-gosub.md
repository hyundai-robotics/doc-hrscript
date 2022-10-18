# 3.3.2 gosub~retsub

### Description

When the gosub statement is encountered, it branches to the specified address.
When the retsub statement is encountered, it returns to the next position after the gosub statement.
Gosub can be nested into several level, and there is no limit on the number of nesting.

### Syntax
```python
gosub <address>
...
end
  
<address>
...  
retsub
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
      <td style="text-align:left">address</td>
      <td style="text-align:left">
        <p>Address to branch</p>
        <p>An arithmetic expression is possible in the case of a line number.</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### Example

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
