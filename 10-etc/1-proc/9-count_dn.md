# 10.1.9 count_dn문

count_dn문은 지정한 정수타입 변수를 1씩 감소시키는 함수입니다.

### 설명

- 함수가 수행될 때마다 지정한 정수타입 변수를 1씩 감소시킵니다.
- 변수가 프리셋 값보다 작을 경우 초기값으로 변경합니다.

### 문법

```python
count_dn <변수>,init=<초기값>,presest=<프리셋 값>
```

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>      
      <th style="text-align:left">타입</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">변수</td>      
      <td style="text-align:left">정수형</td>
      <td style="text-align:left">
         감소시킬 변수
      </td>
    </tr>
    <tr>
      <td style="text-align:left">초기값</td>      
      <td style="text-align:left">정수형</td>
      <td style="text-align:left">
        변수의 값이 프리셋 값보다 작아진 경우 설정할 값
      </td>
    </tr>
    <tr>
      <td style="text-align:left">프리셋 값</td>
      <td style="text-align:left">정수형</td>
      <td style="text-align:left">
        변수 감소 하한값
      </td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
   var cnt
   count_dn cnt,init=100,preset=0
   end
```
