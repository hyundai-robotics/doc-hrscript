# recv

### 설명

설정된 이더넷 객체로 값들을 수신합니다.

### 문법

&lt;ENet객체&gt;.recv \[, &lt;대기시간&gt;\]\[, &lt;퇴피주소&gt;\]



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

### 사용 예

```python
enet_to_sensor.recv
enet_to_sensor.recv 5000
enet_to_sensor.recv 5000,*TimeOut
```

