# 10.2.6 sigout 함수

sigout 함수를 사용하면 출력 신호의 특정 범위를 int형 값으로 지정하여 출력할 수 있습니다.

V70.02-00부터 지원됩니다.

### 설명
- 시작으로 사용할 출력 신호의 이름을 입력합니다.
- 몇개의 비트에 출력할 지 설정합니다.
- 출력할 값을 설정합니다.

### 문법

```python
result=sigout(<출력 신호명>,<비트 수>,<출력 값>)
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
      <td style="text-align:left">출력 신호명</td>
      <td style="text-align:left">
        출력 신호명 (비트)
      </td>
      <td style="text-align:left">출력 신호</td>
    </tr>
    <tr>
      <td style="text-align:left">비트 수</td>
      <td style="text-align:left">
        출력 신호명을 시작으로 출력할 신호의 비트의 수
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">출력 값</td>
      <td style="text-align:left">
        출력할 값
      <td style="text-align:left">변수</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
     var result1,result2,result3
     result1=sigout(do4,4,7)
     result2=sigout(fb2.do0,2,2)
     result3=sigout(fn1.do24,8,55)
     end
```

