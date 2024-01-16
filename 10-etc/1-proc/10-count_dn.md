# 10.1.10 count_dn문

count_dn문은 지정된 변수의 값을 1씩 감소시키다 preset 보다 작은값이면 init값으로 초기화하는 프로시져입니다.

### 설명

지정된 변수의 값을 1씩 감소시키다 preset 보다 작은값이면 init값으로 변수값을 초기화 하는 동작을 수행합니다. <br>
count_dn cnt,init=100,preset=0를 실행하는 것은 하기의 4줄을 실행하는것과 동일한 결과를 얻을 수 있습니다. <br>
...<br>
cnt=cnt-1 <br>
if cnt<0 <br>
cnt=100 <br>
endif <br>

### 문법

```python
count_dn <변수>,init=<초기값>,preset=<최종값>
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
      <td style="text-align:left">변수</td>
      <td style="text-align:left">
      카운터를 감소시킬 변수
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
  <tbody>
  <tr>
      <td style="text-align:left">init</td>
      <td style="text-align:left">
      변수값이 preset에 지정된 값 미만인 경우 초기값 지정
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
  <tbody>
  <tr>
      <td style="text-align:left">preset</td>
      <td style="text-align:left">
      변수의 최소값 지정
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
   global work_no
   move P,spd=30%,accu=0,tool=1
   delay 0.5
   move P,spd=30%,accu=0,tool=1
   move L,spd=30mm/s,accu=0,tool=1
   move L,spd=30mm/s,accu=0,tool=1
   delay 0.5
   move P,spd=30%,accu=0,tool=1
   count_dn work_no,init=99,preset=0
   end
```
