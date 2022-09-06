# 6.2.2 ENet 멤버변수

<table>
  <thead>
    <tr>
      <th style="text-align:left">변수명</th>
      <th style="text-align:left">데이터형</th>
      <th style="text-align:left">설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">ip_addr</td>
      <td style="text-align:left">문자열</td>
      <td style="text-align:left">
        <p>읽기/쓰기 가능.
          <br />
        </p>
        <p>통신상대의 IP 주소를 지정하거나
          얻습니다.
          <br />
        </p>
        <p>open문 호출 시에만 적용됩니다.
          <br
          />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">rport</td>
      <td style="text-align:left">숫자</td>
      <td style="text-align:left">
        <p>읽기/쓰기 가능.
          <br />
        </p>
        <p>통신상대(Remote)의 포트번호를
          지정하거나 얻습니다.
          <br
          />
        </p>
        <p>open문 호출 시에만 적용됩니다.
          <br
          />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">lport</td>
      <td style="text-align:left">숫자</td>
      <td style="text-align:left">
        <p>읽기/쓰기 가능.
          <br />
        </p>
        <p>UDP 통신에서 사용되며,
          TCP 통신에서는 무시됩니다.
          <br
          />
        </p>
        <p>제어기 자신의(Local)의 포트번호를
          지정하거나 얻습니다.
          <br
          />
        </p>
        <p>디폴트 값은 0이며(지정하지
          않은 경우), 이 경우에는
          자신의 포트번호는 자동
          생성됩니다.
          <br />
        </p>
        <p>open문 호출 시에만 적용됩니다.
          <br
          />
        </p>
      </td>
    </tr>
  </tbody>
</table>

