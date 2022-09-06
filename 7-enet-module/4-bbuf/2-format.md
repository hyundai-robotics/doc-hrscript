# 7.4.2 지원 형식 (format)

멤버함수인 append()나 read_num()는 인수로 형식을 지정해야 합니다.  

형식은 Signed/Unsigned/Floating-point 를 의미하는 영문자 1개와 byte 수를 의미하는 숫자 1개로 구성됩니다.<br>
영문자가 대문자이면 big endian, 소문자이면 little endian입니다.			



<table>
  <thead>
    <tr>
      <th>형식</th>
      <th>endian</th>
      <th>타입</th>
      <th>바이트수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>"S1"</td>
      <td>big endian<br>
      <td>부호있는 정수 (signed integer)<br>
      <td>1byte<br>
    </tr>
    <tr>
      <td>"S2"</td>
      <td>big endian<br>
      <td>부호있는 정수 (signed integer)<br>
      <td>2byte<br>
    </tr>
    <tr>
      <td>"S4"</td>
      <td>big endian<br>
      <td>부호있는 정수 (signed integer)<br>
      <td>4byte<br>
    </tr>
    <tr>
      <td>"U1"</td>
      <td>big endian<br>
      <td>부호없는 정수 (unsigned integer)<br>
      <td>1byte<br>
    </tr>
    <tr>
      <td>"U2"</td>
      <td>big endian<br>
      <td>부호없는 정수 (unsigned integer)<br>
      <td>2byte<br>
    </tr>
    <tr>
      <td>"U4"</td>
      <td>big endian<br>
      <td>부호없는 정수 (unsigned integer)<br>
      <td>4byte<br>
    </tr>
    <tr>
      <td>"F4"</td>
      <td>big endian<br>
      <td>단정도 실수 (single-precision real)<br>
      <td>4byte<br>
    </tr>
    <tr>
      <td>"F8"</td>
      <td>big endian<br>
      <td>배정도 실수 (double-precision real)<br>
      <td>8byte<br>
    </tr>
    <tr>
      <td>"s1"</td>
      <td>little endian<br>
      <td>부호있는 정수 (signed integer)<br>
      <td>1byte<br>
    </tr>
    <tr>
      <td>"s2"</td>
      <td>little endian<br>
      <td>부호있는 정수 (signed integer)<br>
      <td>2byte<br>
    </tr>
    <tr>
      <td>"s4"</td>
      <td>little endian<br>
      <td>부호있는 정수 (signed integer)<br>
      <td>4byte<br>
    </tr>
    <tr>
      <td>"u1"</td>
      <td>little endian<br>
      <td>부호없는 정수 (unsigned integer)<br>
      <td>1byte<br>
    </tr>
    <tr>
      <td>"u2"</td>
      <td>little endian<br>
      <td>부호없는 정수 (unsigned integer)<br>
      <td>2byte<br>
    </tr>
    <tr>
      <td>"u4"</td>
      <td>little endian<br>
      <td>부호없는 정수 (unsigned integer)<br>
      <td>4byte<br>
    </tr>
    <tr>
      <td>"f4"</td>
      <td>little endian<br>
      <td>단정도 실수 (single-precision real)<br>
      <td>4byte<br>
    </tr>
    <tr>
      <td>"f8"</td>
      <td>little endian<br>
      <td>배정도 실수 (double-precision real)<br>
      <td>8byte<br>
    </tr>
	 <tr>

  </tbody>
</table>