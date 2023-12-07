# 10.2.5 sig2int 함수

sig2int 함수를 사용하면 입출력 신호의 특정 범위를 int형 값으로 표현할 수 있습니다.

### 설명
- int형으로 표현할 입/출력 신호의 이름을 입력합니다.
- 입/출력 신호로부터 몇개의 비트를 읽을 지 설정합니다.

### 문법

```python
result=sig2int(<입/출력 신호명>,<비트 수>)
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
      <td style="text-align:left">입/출력 변수명</td>
      <td style="text-align:left">
        입/출력 신호명
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">비트 수</td>
      <td style="text-align:left">
        입/출력 신호로부터 읽을 비트의 수
      <td style="text-align:left">변수</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
     var result1,result2,result3
     result1=sig2int(di4,4)
     result2=sig2int(fb2.0,1)
     result3=sig2int(fn1.24,8)
     end
```

