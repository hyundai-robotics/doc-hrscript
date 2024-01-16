# 10.1.8 optime문

optime문은 가동시간의 측정을 시작하거나 갱신하는 프로시져입니다.

### 설명

일반적으로 기동 버튼에 의해 가동시간의 측정을 시작하고, 프로그램의 end를 실행하면 자동으로 가동시간을 갱신합니다. 그런데 end를 실행하지 않고 goto문에 의해 프로그램 선두로 이동하는 경우에는 가동시간이 계속 증가하기 때문에 가동시간의 모니터링 값이 의미가 없게 됩니다. 이 경우에 optime문을 사용하여 측정 시작과 측정 갱신 지점을 사용자가 지정할 수 있습니다.   


### 문법

```python
optime <파라미터>
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
      <td style="text-align:left">파라미터</td>
      <td style="text-align:left">
        <ul>
        <li>cycle_start: 측정 시작</li>
        <li>cycle_end: 측정 갱신</li>
        </ul>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
  *start
   optime cycle_start
   move P,spd=30%,accu=0,tool=1
   delay 0.5
   move P,spd=30%,accu=0,tool=1
   move L,spd=30mm/s,accu=0,tool=1
   move L,spd=30mm/s,accu=0,tool=1
   delay 0.5
   move P,spd=30%,accu=0,tool=1
   optime cycyl_end
   goto *start
   end
```
