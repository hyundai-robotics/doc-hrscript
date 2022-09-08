# recv

### 설명

Sci의 recv 를 호출하여 문자열을 수신합니다.


### 문법

&lt;Sci객체&gt;.recv \[{대기시간}\] \[, {퇴피주소}\]


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
      <td>대기시간</td>
      <td>
        timeout 시간. 경과하면 다음 명령문, 혹은 퇴피스텝으로 진행한다.<br>
        지정하지 않으면 무한 대기한다.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>퇴피주소</td>
      <td>
        timeout 일 때 분기할 주소.<br>
        지정하지 않으면 다음 주소로 진행한다.
      </td>
      <td>주소</td>
    </tr>
  </tbody>
</table>

### 리턴값

수신한 문자열

### 사용 예

```python
   var msg = sci2.recv(5000, 99)
99 print "error"
```



