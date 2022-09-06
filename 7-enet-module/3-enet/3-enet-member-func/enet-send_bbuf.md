# send_bbuf

### 설명

이더넷 객체로 [BBuf](../../4-bbuf/README.md) 객체를 송신합니다.

### 문법

{ENet객체}.send_bbuf {BBuf객체}



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
      <td style="text-align:left">BBuf객체</td>
      <td style="text-align:left">
        송신할 Binary Buffer 객체.
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>


### 리턴값

송신한 데이터 개수


### 사용 예

```python
var bbuf=enet.BBuf()
var arr=[ -3, 0, 1 ]
bbuf.append("s4", arr)
var nitem=cli.send_bbuf(bbuf)
```



