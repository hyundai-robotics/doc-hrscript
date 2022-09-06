# 7.3.1 ENet 생성자

### 설명

이더넷 객체를 생성합니다. 참조를 리턴합니다.

### 문법

ENet\({프로토콜}\)

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
      <td>프로토콜</td>
      <td>
        "tcp" : TCP 통신<br>
        "udp" : UDP 통신<br>
        생략하면 "udp"로 인식</td>
    </tr>
  </tbody>
</table>

### 리턴값

생성된 객체의 참조

### 사용 예

```python
enet0 = ENet()
var tcp = ENet("tcp")
```
