# 6.2.1 생성자

### 설명

이더넷 객체를 생성합니다. 참조를 리턴합니다.

### 문법

ENet\(&lt;프로토콜&gt;\)

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
      <td style="text-align:left">프로토콜</td>
      <td style="text-align:left">
        <p>&quot;tcp&quot; : TCP 통신
          <br />
        </p>
        <p>&quot;udp&quot; : UDP 통신
          <br />
        </p>
        <p>
          <br />
        </p>
      </td>
      <td style="text-align:left">생략하면 &quot;udp&quot;로 인식</td>
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



