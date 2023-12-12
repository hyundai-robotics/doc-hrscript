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
triggout <출력변수>,val=<출력값>,dist=<선출/후출 거리>,j=<tcp 또는 축방향 상대거리>
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
        (-)인 경우 목표위치 도달 전 신호가 출력되며 (+)인 경우 도달 후 출력됩니다.
      </td>
      <td style="text-align:left">산술식</td>
    </tr>
    <tr>
      <td style="text-align:left">선출/후출 거리</td>
      <td style="text-align:left">
        -3000 ~ 3000 [mm]<br>
        (-)인 경우 목표위치 도달 전 신호가 출력되며 (+)인 경우 도달 후 출력됩니다.
      </td>
      <td style="text-align:left">산술식</td>
    </tr>
    <tr>
      <td style="text-align:left">x, y, z방향 절대위치</td>
      <td style="text-align:left">
        -3000 ~ 3000 [mm]<br>
        (-)인 경우 목표위치 도달 전 신호가 출력되며 (+)인 경우 도달 후 출력됩니다.
      </td>
      <td style="text-align:left">산술식</td>
    </tr>
    <tr>
      <td style="text-align:left">tcp 또는 축방향 상대거리<br>
      tcp : j=0인 경우,<br>
      축방향 : j=1 이상인 경우
      </td>
      <td style="text-align:left">
        tcp : -3000 ~ 3000 [mm], 축방향 : -3000 ~ 3000 [mm] or [deg]<br>
        (-)인 경우 상대거리 도달 전 신호가 출력되며 (+)인 경우 도달 후 출력됩니다.
      </td>
      <td style="text-align:left">산술식</td>
    </tr>
  </tbody>
</table>

<br>

### 사용 예

```python
   move L,spd=300mm/s,accu=3,tool=1
   triggout do1,val=1,time=-0.5  #스텝도달 0.5초전에 do1을 on
   triggout do1,val=1,dist=-100.0,j=0  #tcp가 스텝위치와 상대거리 -100mm 도달시 do1을 on
   triggout do1,val=1,dist=-3.0,j=1  #1축이 스텝위치와 상대거리 -3.0deg 도달시 do1을 on
   triggout do1,val=1,x=-100.0  #X좌표값이 -100mm 도달시 do1을 on
   triggout do1,val=1,x=-100.0,y=-100.0  #X, Y의 좌표값이 -100mm 도달시 do1을 on
   move L,spd=30%,accu=2,tool=1
   end
```
