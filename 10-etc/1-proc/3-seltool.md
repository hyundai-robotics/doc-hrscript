# 10.1.3 seltool문

seltool문은 툴번호를 변경하는 프로시져입니다.

### 설명

툴은 로봇 플랜지에 부착되어 있는 로봇툴과 로봇과는 별도로 설치되어 있는 정치툴로 구분되며 이에 대한 각각의 툴번호를 변경합니다.   


### 문법

```python
seltool <툴번호>,<툴타입>
```

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
      <td style="text-align:left">툴번호</td>
      <td style="text-align:left">
        변경을 원하는 툴번호<br>
        <ul>
        <li>로봇툴: 0 ~ 31</li>
        <li>정치툴: 0 ~ 3</li>
        </ul>
      </td>
      <td style="text-align:left">산술식</td>
    </tr>
    <tr>
      <td style="text-align:left">툴타입</td>
      <td style="text-align:left">
        변경을 원하는 툴타입<br>
        <ul>
        <li>로봇툴: robot</li>
        <li>정치툴: station</li>
        </ul>
      </td>
      <td style="text-align:left">문자열식 (robot/station)</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
   move P,spd=30%,accu=0,tool=1
   seltool 0,station
   move SP,spd=30%,accu=0,tool=1
   move SL,spd=30mm/s,accu=0,tool=1
   move SL,spd=30mm/s,accu=0,tool=1
   delay 0.5
   move P,spd=30%,accu=0,tool=1
   end
```

![](../../_assets/seltool.png)

