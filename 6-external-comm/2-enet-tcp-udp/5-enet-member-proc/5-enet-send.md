﻿# send

### 설명

설정된 이더넷 객체로 문자열을 송신합니다.

### 문법

&lt;ENet객체&gt;.send &lt;msg&gt;



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
        출력할 문자열.
      </td>
      <td style="text-align:left">문자열형</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
enet_to_sensor.send "rob:" + 10 + ", command:"+cmd, "\n"
```


