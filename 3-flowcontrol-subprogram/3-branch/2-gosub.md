# 3.3.2 gosub~retsub 문

### 설명

gosub문을 만나면 지정한 주소로 분기합니다. retsub문을 만나면 gosub문 다음 위치로 복귀합니다.  
gosub를 여러 단계로 내포할 수도 있으며 내포 횟수의 제약은 없습니다.

### 문법

```python
gosub <주소>
...
end
  
<address>
...  
retsub
```

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">주소</td>
      <td style="text-align:left">
        <p>분기할 주소</p>
        <p>행 번호인 경우 산술식도 가능</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### 사용 예

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
