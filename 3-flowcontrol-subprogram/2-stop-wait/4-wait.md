# 3.2.4 wait문

### 설명

지정한 조건이 참이 될 때까지 대기한 후 다음 명령문으로 진행합니다.

### 문법

wait &lt;조건&gt;\[,&lt;제한시간&gt;,&lt;timeout 주소&gt;\]

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
      <td style="text-align:left">조건</td>
      <td style="text-align:left">대기할 조건</td>
      <td style="text-align:left">조건식</td>
    </tr>
    <tr>
      <td style="text-align:left">제한시간</td>
      <td style="text-align:left">조건이 거짓일 경우 대기할
        최대 제한 시간 (timeout)</td>
      <td style="text-align:left">
        <p>산술식
          <br />
        </p>
        <p>0.1~60.0 sec
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">timeout 주소</td>
      <td style="text-align:left">제한시간 초과 시, 분기할
        주소</td>
      <td style="text-align:left">주소</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
wait sensor_ok
wait (sensor_ok and pos_ok),10,*timeout
```

