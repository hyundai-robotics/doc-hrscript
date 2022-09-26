# 2.9.5 기타 함수



<table>
  <thead>
    <tr>
      <th style="text-align:left">함수</th>
      <th style="text-align:left">설명</th>
      <th style="text-align:left">사용 예</th>
      <th style="text-align:left">결과</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">cpo(crd, mode)
        <br />
      </td>
      <td style="text-align:left">
        <p>로봇이 취하고 있는 현재
          자세(current pose)를 crd좌표계로
          리턴합니다.
          <br />
        </p>
        <p>crd 인수로 사용할 수 있는
          값은 &quot;<a href="../../moving-robot/pose.md">5.1 포즈 (pose)</a>&quot;의
          표를 참조하십시오.
          <br />
        </p>
        <p>mode가 &quot;cmd&quot;이면 지령값,
          &quot;cur&quot;이면 현재값입니다.
          <br
          />
        </p>
        <p>crd, mode 파라미터를 생략 가능하며
          디폴트값은 각각 “base”,
          ”cur” 입니다.
          <br />
        </p>
        <p>
          <br />
        </p>
        <p>
          <br />
        </p>
      </td>
      <td style="text-align:left">cpo(&quot;joint&quot;, &quot;cmd&quot;)
        <br />
      </td>
      <td style="text-align:left">로봇의 지령값을 축좌표계로
        보관하는 포즈*</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>mkucs(n,po)
          <br />
        </p>
        <p>mkucs(n,po1,po2
          <br />
        </p>
        <p>,po3)
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>n번 사용자좌표계 객체를
          생성하여 등록합니다.
          <br
          />
        </p>
        <p>&quot;<a href="../../moving-robot/ucs.md">5.5 사용자좌표계 (UCS ; User Coordinate System)</a>&quot;를
          참조하십시오.
          <br />
        </p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>0 : OK
          <br />
        </p>
        <p>&lt;0 : 에러코드
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">result()</td>
      <td style="text-align:left">일부 프로시져는 수행
        결과를 확인해야 할 경우가
        있습니다. 프로시져 수행
        직후 result( ) 함수를 호출하면,
        수행 결과를 리턴 받을
        수 있습니다.</td>
      <td style="text-align:left">result()</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

\* 포즈\(pose\)는 로봇의 자세 혹은 툴 끝의 위치를 나타내는 데이터형입니다. 이후의 "[5.1 포즈 \(pose\)](../../5-moving-robot/1-pose.md)"에서 자세히 설명합니다.

