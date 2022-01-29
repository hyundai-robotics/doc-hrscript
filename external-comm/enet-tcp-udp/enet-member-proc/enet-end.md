# send

### 설명

설정된 이더넷 객체로 값들을 송신합니다.

### 문법

&lt;ENet객체&gt;.send &lt;값&gt;, &lt;값&gt;, …



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
      <td style="text-align:left">값</td>
      <td style="text-align:left">
        <p>출력할 데이터 값.
          <br />
        </p>
        <p>쉼표로 분리된 인수들은
          공백으로 나뉘어 출력.
          <br
          />
        </p>
        <p>
          <br />
        </p>
        <p>
          <br />
        </p>
      </td>
      <td style="text-align:left">모든 데이터형</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
enet_to_sensor.send "rob:", 10, ", command:"+cmd, "\n"
```



