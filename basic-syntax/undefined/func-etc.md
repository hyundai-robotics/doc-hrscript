# 기타 함수



<table>
  <thead>
    <tr>
      <th style="text-align:left">&#xD568;&#xC218;</th>
      <th style="text-align:left">&#xC124;&#xBA85;</th>
      <th style="text-align:left">&#xC0AC;&#xC6A9; &#xC608;</th>
      <th style="text-align:left">&#xACB0;&#xACFC;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">cpo(crd, mode)
        <br />
      </td>
      <td style="text-align:left">
        <p>&#xBD07;&#xC774; &#xCDE8;&#xD558;&#xACE0; &#xC788;&#xB294; &#xD604;&#xC7AC;
          &#xC790;&#xC138;(current pose)&#xB97C; crd&#xC88C;&#xD45C;&#xACC4;&#xB85C;
          &#xB9AC;&#xD134;&#xD569;&#xB2C8;&#xB2E4;.
          <br />
        </p>
        <p>crd &#xC778;&#xC218;&#xB85C; &#xC0AC;&#xC6A9;&#xD560; &#xC218; &#xC788;&#xB294;
          &#xAC12;&#xB294; 5.1&#xC808;&#xC758; &#xD45C;&#xB97C; &#xCC38;&#xC870;&#xD558;&#xC2ED;&#xC2DC;&#xC624;.
          <br
          />
        </p>
        <p>mode&#xAC00; &quot;cmd&quot;&#xC774;&#xBA74; &#xC9C0;&#xB839;&#xAC12;,
          &quot;cur&quot;&#xC774;&#xBA74; &#xD604;&#xC7AC;&#xAC12;&#xC785;&#xB2C8;&#xB2E4;.
          <br
          />
        </p>
        <p>crd, mode &#xD30C;&#xB77C;&#xBBF8;&#xD130;&#xB97C; &#xC0DD;&#xB7B5; &#xAC00;&#xB2A5;&#xD558;&#xBA70;
          &#xB514;&#xD3F4;&#xD2B8;&#xAC12;&#xC740; &#xAC01;&#xAC01; &#x201C;base&#x201D;,
          &#x201D;cur&#x201D; &#xC785;&#xB2C8;&#xB2E4;.
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
      <td style="text-align:left">&#xB85C;&#xBD07;&#xC758; &#xC9C0;&#xB839;&#xAC12;&#xC744; &#xCD95;&#xC88C;&#xD45C;&#xACC4;&#xB85C;
        &#xBCF4;&#xAD00;&#xD558;&#xB294; &#xD3EC;&#xC988;*</td>
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
        <p>n&#xBC88; &#xC0AC;&#xC6A9;&#xC790;&#xC88C;&#xD45C;&#xACC4; &#xAC1D;&#xCCB4;&#xB97C;
          &#xC0DD;&#xC131;&#xD558;&#xC5EC; &#xB4F1;&#xB85D;&#xD569;&#xB2C8;&#xB2E4;.
          <br
          />
        </p>
        <p>5.5&#xC808;&#xC744; &#xCC38;&#xC870;&#xD558;&#xC2ED;&#xC2DC;&#xC624;.
          <br
          />
        </p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>0 : OK
          <br />
        </p>
        <p>&lt;0 : &#xC5D0;&#xB7EC;&#xCF54;&#xB4DC;
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">result()</td>
      <td style="text-align:left">&#xC77C;&#xBD80; &#xD504;&#xB85C;&#xC2DC;&#xC838;&#xB294; &#xC218;&#xD589;
        &#xACB0;&#xACFC;&#xB97C; &#xD655;&#xC778;&#xD574;&#xC57C; &#xD560; &#xACBD;&#xC6B0;&#xAC00;
        &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;. &#xD504;&#xB85C;&#xC2DC;&#xC838; &#xC218;&#xD589;
        &#xC9C1;&#xD6C4; result( ) &#xD568;&#xC218;&#xB97C; &#xD638;&#xCD9C;&#xD558;&#xBA74;,
        &#xC218;&#xD589; &#xACB0;&#xACFC;&#xB97C; &#xB9AC;&#xD134; &#xBC1B;&#xC744;
        &#xC218; &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;.</td>
      <td style="text-align:left">result()</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

\* 포즈\(pose\)는 로봇의 자세 혹은 툴 끝의 위치를 나타내는 데이터형입니다. 이후의 5.1절에서 자세히 설명합니다.

