# recv

### 설명

이더넷 객체로 문자열을 수신합니다. 수신된 문자열은 리턴값이나 `result()` 함수로 얻을 수 있습니다.

### 문법

`{ENet객체}.recv [{대기시간}][,{퇴피주소}]`



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
        timeout 시간. 경과하면 다음 명령문, 혹은 퇴피스텝으로 진행.<br>
        지정하지 않으면 무한 대기.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>퇴피주소</td>
      <td>
        timeout 일 때 분기할 주소.<br>
        지정하지 않으면 다음 주소로 진행.
      </td>
      <td>주소</td>
    </tr>
  </tbody>
</table>

### 리턴값

수신한 문자열

### 사용 예

```python
var msg
msg=enet_to_sensor.recv
msg=enet_to_sensor.recv(5000)
msg=enet_to_sensor.recv(5000,*TimeOut)
end

*TimeOut
print "Time out! No response from sensor"
end
```
