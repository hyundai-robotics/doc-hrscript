# 6.1.4 pulse문

pulse문은 펄스 형태의 신호 출력을 위해 사용하는 프로시져 입니다.

### 설명

tlag 시간 후에, ton 시간 동안 On(High), toff 시간 동안 Off(Low) 형태의 펄스가 cnt 횟수만큼 출력됩니다.


### 문법

```python
pulse <신호>,tlag=<지연 시간>,ton=<On 시간>,toff=<Off 시간>,cnt=<출력 횟수>
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
      <td style="text-align:left">신호</td>
      <td style="text-align:left">
        펄스 형태로 출력할 출력신호명<br>
        (fb.do 신호만을 지원합니다.)
      </td>
      <td style="text-align:left">문자열</td>
    </tr>
    <tr>
      <td style="text-align:left">지연 시간</td>
      <td style="text-align:left">
        프로시져 수행 후 펄스 신호가 시작될 때까지 대기할 시간<br>
        (0.0 ~ 100.0[sec])
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">On 시간</td>
      <td style="text-align:left">
        신호를 On(High) 상태로 출력할 시간<br>
        (0.0 ~ 100.0[sec])
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">Off 시간</td>
      <td style="text-align:left">
        신호를 Off(Low) 상태로 출력할 시간<br>
        (0.0 ~ 100.0[sec])
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">출력 횟수</td>
      <td style="text-align:left">
        펄스 주기를 반복할 횟수
        (0 ~ 1000)
      </td>
      <td style="text-align:left">변수</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
   pulse do10,tlag=0.0,ton=1.5,toff=0.5,cnt=5
   end
```