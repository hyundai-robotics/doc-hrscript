# 10.2.1 rducs함수 - 사용자좌표계

생성된 사용자좌표계를 포즈로 읽는 명령어입니다.

### 설명

- 생성된 사용자 좌표계의 위치/방향이 해당 포즈 값으로 복사합니다.
- 생성되지 않았거나 파라미터가 유효하지 않은 경우, 에러가 발생하면서 job 실행이 중단됩니다.


### 문법

```python
<결과변수> = rducs(<사용자좌표계 번호>,<포즈변수>)
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
        </ul>
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">사용자좌표계 번호</td>
      <td style="text-align:left">
        읽을 사용자좌표계의 번호
      </td>
      <td style="text-align:left">[1~20]</td>
    </tr>
    <tr>
      <td style="text-align:left">포즈변수</td>
      <td style="text-align:left">
        위치/방향을 전달받을 변수
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

- E14613 : 실 파라미터가 형식 파라미터와 형식이 맞지 않을 때 발생합니다. 실 파라미터를 확인하십시오.
- E14614 : 사용자좌표번호가 숫자가 아닐때 발생합니다. 사용자좌표번호를 다시 지정하십시오.
- E14615 : 사용자좌표번호가 1~20 사이의 숫자가 아닐 때 발생합니다. 사용자좌표번호를 변경하십시오.
- E1336 : 등록되지 않은 사용자좌표번호인 경우에 발생합니다. 사용자좌표번호를 변경하십시오.


### 사용 예

```python
   var p_uc2=Pose(0,0,0,0,0,0,"base")
   var res=rducs(2,p_uc2)
   end
```

![](../../_assets/rducs.png)

