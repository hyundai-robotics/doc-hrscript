# 2.9.2 문자열 함수

var str="hello, world"가 실행된 상태에서의 예

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
      <td style="text-align:left">bin(a)</td>
      <td style="text-align:left">&#xC218;&#xCE58; a&#xC758; 2&#xC9C4; &#xD45C;&#xD604; &#xBB38;&#xC790;&#xC5F4;&#xC744;
        &#xB9AC;&#xD134;&#xD569;&#xB2C8;&#xB2E4;</td>
      <td style="text-align:left">bin(0b0010)</td>
      <td style="text-align:left">&quot;10&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">chr(a)</td>
      <td style="text-align:left">ASCII&#xCF54;&#xB4DC; a&#xC778; &#xBB38;&#xC790;&#xB97C; &#xBB38;&#xC790;&#xC5F4;&#xD615;&#xC73C;&#xB85C;
        &#xB9AC;&#xD134;&#xD569;&#xB2C8;&#xB2E4;.</td>
      <td style="text-align:left">chr(65)</td>
      <td style="text-align:left">&quot;A&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">double(s)</td>
      <td style="text-align:left">
        <p>&#xC2E4;&#xC218; &#xBB38;&#xC790;&#xC5F4;s&#xC758; &#xC2E4;&#xC218;&#xD615;&#xAC12;&#xC744;
          &#xB9AC;&#xD134;&#xD569;&#xB2C8;&#xB2E4;.
          <br />
        </p>
        <p>(&#xD574;&#xC11D;&#xB418;&#xB294; &#xC704;&#xCE58;&#xAE4C;&#xC9C0;&#xB9CC;
          &#xD574;&#xC11D;&#xD558;&#xACE0; &#xB098;&#xBA38;&#xC9C0;&#xB294; &#xBC84;&#xB9BC;)
          <br
          />
        </p>
      </td>
      <td style="text-align:left">double(&quot;29.38E-2&quot;)</td>
      <td style="text-align:left">0.2938</td>
    </tr>
    <tr>
      <td style="text-align:left">hex(a)</td>
      <td style="text-align:left">&#xC218;&#xCE58; a&#xC758; 16&#xC9C4; &#xD45C;&#xD604; &#xBB38;&#xC790;&#xC5F4;&#xC744;
        &#xB9AC;&#xD134; &#xD569;&#xB2C8;&#xB2E4;.</td>
      <td style="text-align:left">hex(0x7A2F)</td>
      <td style="text-align:left">&quot;7A2F&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">int(s)</td>
      <td style="text-align:left">
        <p>&#xC815;&#xC218; &#xBB38;&#xC790;&#xC5F4;s&#xC758; &#xC815;&#xC218;&#xD615;&#xAC12;&#xC744;
          &#xB9AC;&#xD134;&#xD569;&#xB2C8;&#xB2E4;.
          <br />
        </p>
        <p>(&#xD574;&#xC11D;&#xB418;&#xB294; &#xC704;&#xCE58;&#xAE4C;&#xC9C0;&#xB9CC;
          &#xD574;&#xC11D;&#xD558;&#xACE0; &#xB098;&#xBA38;&#xC9C0;&#xB294; &#xBC84;&#xB9BC;)
          <br
          />
        </p>
      </td>
      <td style="text-align:left">
        <p>int(&quot;13.25&quot;)
          <br />
        </p>
        <p>int(&quot;29.38E-2&quot;)
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>13
          <br />
        </p>
        <p>29
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">left(s, n)</td>
      <td style="text-align:left">&#xBB38;&#xC790;&#xC5F4; s&#xC758; &#xC55E;&#xBD80;&#xBD84; n&#xAC1C;&#xC758;
        &#xBB38;&#xC790;&#xB85C; &#xB41C; &#xBB38;&#xC790;&#xC5F4;&#xC744; &#xB9AC;&#xD134;&#xD569;&#xB2C8;&#xB2E4;.</td>
      <td
      style="text-align:left">left(str, 3)</td>
        <td style="text-align:left">&quot;hel&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">len(s)</td>
      <td style="text-align:left">
        <p>s&#xAC00; &#xBB38;&#xC790;&#xC5F4;&#xC774;&#xBA74; &#xBB38;&#xC790;&#xC5F4;&#xC758;
          &#xAE38;&#xC774;&#xB97C; &#xB9AC;&#xD134;&#xD569;&#xB2C8;&#xB2E4;.
          <br />
        </p>
        <p>s&#xAC00; &#xBC30;&#xC5F4;&#xC774;&#xBA74; &#xBC30;&#xC5F4;&#xC758; &#xC694;&#xC18C;
          &#xAC1C;&#xC218;&#xB97C; &#xB9AC;&#xD134;&#xD569;&#xB2C8;&#xB2E4;.
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>len(&quot;HELLO&quot;)
          <br />
        </p>
        <p>len([20, 30, 80])
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>5
          <br />
        </p>
        <p>3
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">mid(s, i, n)</td>
      <td style="text-align:left">&#xBB38;&#xC790;&#xC5F4; s&#xC758; i&#xBC88;&#xC9F8; &#xBB38;&#xC790;&#xBD80;&#xD130;
        n&#xAC1C;&#xC758; &#xBB38;&#xC790;&#xB85C; &#xB41C; &#xBB38;&#xC790;&#xC5F4;&#xC744;
        &#xB9AC;&#xD134;&#xD569;&#xB2C8;&#xB2E4;. (&#xCCAB; &#xBB38;&#xC790; &#xC704;&#xCE58;&#xB294;
        0.)</td>
      <td style="text-align:left">mid(str, 3, 5)</td>
      <td style="text-align:left">&quot;lo, w&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">mirror(s)</td>
      <td style="text-align:left">&#xBB38;&#xC790;&#xC5F4; s&#xB97C; &#xC5ED;&#xC804;&#xD55C; &#xBB38;&#xC790;&#xC5F4;&#xC744;
        &#xB9AC;&#xD134;&#xD569;&#xB2C8;&#xB2E4;.</td>
      <td style="text-align:left">mirror(&quot;HELLO&quot;)</td>
      <td style="text-align:left">&quot;OLLEH&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">right(s, n)</td>
      <td style="text-align:left">&#xBB38;&#xC790;&#xC5F4; s&#xC758; &#xB4B7;&#xBD80;&#xBD84; n&#xAC1C;&#xC758;
        &#xBB38;&#xC790;&#xB85C; &#xB41C; &#xBB38;&#xC790;&#xC5F4;&#xC744; &#xB9AC;&#xD134;&#xD569;&#xB2C8;&#xB2E4;.</td>
      <td
      style="text-align:left">right(str, 3)</td>
        <td style="text-align:left">&quot;rld&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">str(a)</td>
      <td style="text-align:left">&#xC218;&#xCE58; a&#xC758; 10&#xC9C4; &#xD45C;&#xD604; &#xBB38;&#xC790;&#xC5F4;&#xC744;
        &#xB9AC;&#xD134;&#xD569;&#xB2C8;&#xB2E4;.</td>
      <td style="text-align:left">str(13.25)</td>
      <td style="text-align:left">13.250000</td>
    </tr>
    <tr>
      <td style="text-align:left">strops(s, p)</td>
      <td style="text-align:left">s&#xBB38;&#xC790;&#xC5F4; &#xB0B4;&#xC5D0; p&#xBB38;&#xC790;&#xC5F4;&#xACFC;
        &#xC77C;&#xCE58;&#xD558;&#xB294; &#xCD5C;&#xCD08;&#xC758; &#xC704;&#xCE58;&#xB97C;
        &#xB9AC;&#xD134;&#xD569;&#xB2C8;&#xB2E4;.(&#xCCAB; &#xBB38;&#xC790; &#xC704;&#xCE58;&#xB294;
        0. &#xC5C6;&#xC73C;&#xBA74; -1.)</td>
      <td style="text-align:left">
        <p>strpos(str, &quot;llo&quot;)
          <br />
        </p>
        <p>strpos(str, &quot;hi&quot;)
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>2
          <br />
        </p>
        <p>-1
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>



