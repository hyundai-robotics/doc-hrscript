# 6.4.1 input문

### 설명

input문을 통해 티치펜던트의 키입력으로 문자열을 입력받아 변수에 저장합니다. 제한시간까지 입력되지 않으면 다음 명령문으로 진행하거나 timeout 주소로 분기합니다.

### 문법

input &lt;변수&gt;\[,&lt;제한시간&gt;,&lt;timeout 주소&gt;\]



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
        <p>입력을 받을 변수. 숫자도
          문자열 타입으로 입력받습니다.
          수치값이 필요하면 int(
          )나 double( ) 함수로 변환하십시오.
          <br
          />
        </p>
        <p>
          <br />
        </p>
        <p>
          <br />
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">제한시간</td>
      <td style="text-align:left">입력을 대기할 최대 제한
        시간 (timeout)</td>
      <td style="text-align:left">
        <p>산술식
          <br />
        </p>
        <p>0.1~60.0 sec
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">timeout 주소</td>
      <td style="text-align:left">제한시간 초과 시, 분기할
        주소</td>
      <td style="text-align:left">주소</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
input work_no
input work_no,10
input work_no,10,*timeout
```

![](../../_assets/image_6.png)



