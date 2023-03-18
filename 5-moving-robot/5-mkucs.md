# 5.5 mkucs함수 - 사용자좌표계

### 설명

세 개의 포즈 혹은 한 개의 포즈로 사용자좌표계를 생성하는 명령어입니다.   

- 세 개의 포즈로 생성시 원점포즈, X축포즈, XY평면포즈로 사용자 좌표계를 생성합니다.
- 한 개의 포즈로 생성시 원점포즈로 사용자 좌표계를 생성하며 위치/방향은 해당 포즈 값을 기준으로 생성합니다.
- 계산할 수 없는 경우, 에러가 발생하면서 job 실행이 중단됩니다.


### 문법

```python
<결과변수> = mkucs(<사용자좌표계 번호>,<원점포즈>,<X방향포즈>,<XY평면포즈>)
또는
<결과변수> = mkucs(<사용자좌표계 번호>,<원점포즈>)
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
      <td style="text-align:left">결과변수</td>
      <td style="text-align:left">
        백그라운드 수행 결과<br>
        <ul>
        <li>0: 성공적으로 완료됨.</li>
        <li>-1: 사용자 좌표계 생성 실패함.</li>
        </ul>
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">사용자좌표계 번호</td>
      <td style="text-align:left">
        생성할 사용자좌표계의 번호
      </td>
      <td style="text-align:left">[1~20]</td>
    </tr>
    <tr>
      <td style="text-align:left">원점포즈</td>
      <td style="text-align:left">
        원점에 위치한 포즈
      </td>
      <td style="text-align:left">포즈변수</td>
    </tr>
    <tr>
      <td style="text-align:left">X방향포즈</td>
      <td style="text-align:left">
        X축에 위치한 포즈
      </td>
      <td style="text-align:left">포즈변수</td>
    </tr>
    <tr>
      <td style="text-align:left">XY평면포즈</td>
      <td style="text-align:left">
        XY 평면에 위치한 포즈
      </td>
      <td style="text-align:left">포즈변수</td>
    </tr>
  </tbody>
</table>

### 리턴값


<table>
  <thead>
    <tr>
      <th style="text-align:left">값</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>
        성공
      </td>
      <td></td>
    </tr>  
  </tbody>
</table>


### 에러 가이드

- E14613 : 티칭 된 포즈의 개수가 부족할때 발생합니다. 1개 혹은 3개의 포즈를 입력하여 주십시오.
- E14614 : 사용자좌표번호가 숫자가 아닐때 발생합니다. 사용자좌표번호를 다시 지정하십시오.
- E14615 : 사용자좌표번호가 1~20 사이의 숫자가 아닐 때 발생합니다. 사용자좌표번호를 변경하십시오.
- E1011 : 티칭 된 포즈간 거리가 너무 가까울때 발생합니다. 각 점간 거리가 1mm이하일 때 발생합니다. 포즈간 거리값을 수정하여 주십시오.
- E1012 : 티칭 된 세 개의 포즈가 일직선상에 있을때 발생합니다. 


### 사용 예

```python
   var p_origin=Pose(0,0,0,0,0,0,"base")
   var p_xaxis=Pose(100,0,0,0,0,0,"base")
   var p_xyplane_=Pose(100,100,0,0,0,0,"base")
   var uc1 = mkucs(1,p_origin,p_xaxis,p_xyplane)
   var uc2 = mkucs(2,p_origin)
   end
```

![](../../_assets/mkucs.png)

