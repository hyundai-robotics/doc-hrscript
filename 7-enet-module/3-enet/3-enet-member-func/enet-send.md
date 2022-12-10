# send

### 설명

이더넷 객체로 문자열을 송신합니다.

### 문법

{ENet객체}.send {msg}



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
      <td style="text-align:left">msg</td>
      <td style="text-align:left">
        송신할 문자열.
      </td>
      <td style="text-align:left">문자열형</td>
    </tr>
  </tbody>
</table>


### 리턴값

송신한 바이트 수


### 사용 예

```python
enet_to_sensor.send "rob:" + 10 + ", command:"+cmd, "\n"
```



