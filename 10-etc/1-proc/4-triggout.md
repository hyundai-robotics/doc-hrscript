# 10.1.4 triggout문

triggout문은 신호출력 시점을 선출(-) 혹은 후출(+)할 수 있게 조정할 수 있는 프로시져입니다.

### 설명

contpath 1이나 2로 설정되어 명령어를 연속 처리하는 구간에서 지령위치가 목표위치(Accuracy OK)에 도착하면  발생하는 신호출력 시점을 선출(-) 혹은 후출(+)할 수 있게 조정할 수 있습니다.   


### 문법

```python
triggout <출력변수>,val=<출력값>,time=<선출/후출 시간>
triggout <출력변수>,val=<출력값>,dist=<선출/후출 거리>,x=<X방향 절대위치>
triggout <출력변수>,val=<출력값>,dist=<선출/후출 거리>,y=<Y방향 절대위치>
triggout <출력변수>,val=<출력값>,dist=<선출/후출 거리>,z=<Z방향 절대위치>
triggout <출력변수>,val=<출력값>,time=<선출/후출 거리>,j=<축방향 절대위치>
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
      <td style="text-align:left">출력변수</td>
      <td style="text-align:left">
        출력신호에 대응하는 변수<br>
        <ul>
        <li>범용출력에 대응하는 do, dob, dow, dol, dof 변수</li>
        <li>전용출력에 대응하는 so, sob, sow, sol, sof 변수</li>
        </ul>
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">출력값</td>
      <td style="text-align:left">
        산술식,<br>
        단일신호 출력(do, so)의 경우 0이면 off, 0이 아니면 on
      </td>
      <td style="text-align:left">산술식</td>
    </tr>
    <tr>
      <td style="text-align:left">선출/후출 시간</td>
      <td style="text-align:left">
        -10.00 ~ 2.00 [s]<br>
        (-)인 경우 목표위치 도달전 신호가 출력되며 (+)인 경우 도달후 출력됩니다.
      </td>
      <td style="text-align:left">산술식</td>
    </tr>
    <tr>
      <td style="text-align:left">선출/후출 거리</td>
      <td style="text-align:left">
        -3000 ~ 3000 [mm]<br>
        목표위치 도달시 신호가 출력됩니다.
      </td>
      <td style="text-align:left">산술식</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
   move L,spd=300mm/s,accu=3,tool=1
   triggout do1,val=1,time=-0.5
   move L,spd=30%,accu=2,tool=1
   end
```
