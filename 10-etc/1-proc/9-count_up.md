# 10.1.9 count_up문

count_up문은 지정된 변수의 값을 1씩 증가시키다 preset값을 초과하면 init값으로 초기화하는 프로시져입니다.

### 설명

지정된 변수의 값을 1씩 증가시키다 preset값을 초과하면 init값으로 변수값을 초기화 하는 동작을 수행합니다. <br>
count_up cnt,init=0,preset=100를 실행하는 것은 하기의 4줄을 실행하는것과 동일한 결과를 얻을 수 있습니다. <br>
...<br>
cnt=cnt+1 <br>
if cnt>100 <br>
cnt=0 <br>
endif <br>

### 문법

```python
count_up <변수>,init=<초기값>,preset=<최종값>
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
      카운터를 증가시킬 변수
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
  <tbody>
  <tr>
      <td style="text-align:left">init</td>
      <td style="text-align:left">
      변수값이 preset에 지정된 값을 초과하는 경우 초기값 지정
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
  <tbody>
  <tr>
      <td style="text-align:left">preset</td>
      <td style="text-align:left">
      변수의 최대값 지정
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
   count_up work_no,init=0,preset=99
   end
```
