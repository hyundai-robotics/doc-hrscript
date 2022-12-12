# 7.4.2 Supported format

The member function `append()` or `read_num()` requires a type to be specified as an argument.

The format consists of 1 alphabet meaning Signed/Unsigned/Floating-point and 1 digit meaning the number of bytes.<br>
If the alphabet is uppercase it is big endian, and lowercase it is little endian.

<table>
  <thead>
    <tr>
      <th>Format</th>
      <th>Endian</th>
      <th>Type</th>
      <th>The number of bytes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>"S1"</td>
      <td>big endian<br>
      <td>signed integer<br>
      <td>1byte<br>
    </tr>
    <tr>
      <td>"S2"</td>
      <td>big endian<br>
      <td>signed integer<br>
      <td>2byte<br>
    </tr>
    <tr>
      <td>"S4"</td>
      <td>big endian<br>
      <td>signed integer<br>
      <td>4byte<br>
    </tr>
    <tr>
      <td>"U1"</td>
      <td>big endian<br>
      <td>unsigned integer<br>
      <td>1byte<br>
    </tr>
    <tr>
      <td>"U2"</td>
      <td>big endian<br>
      <td>unsigned integer<br>
      <td>2byte<br>
    </tr>
    <tr>
      <td>"U4"</td>
      <td>big endian<br>
      <td>unsigned integer<br>
      <td>4byte<br>
    </tr>
    <tr>
      <td>"F4"</td>
      <td>big endian<br>
      <td>single-precision real<br>
      <td>4byte<br>
    </tr>
    <tr>
      <td>"F8"</td>
      <td>big endian<br>
      <td>double-precision real<br>
      <td>8byte<br>
    </tr>
    <tr>
      <td>"s1"</td>
      <td>little endian<br>
      <td>signed integer<br>
      <td>1byte<br>
    </tr>
    <tr>
      <td>"s2"</td>
      <td>little endian<br>
      <td>signed integer<br>
      <td>2byte<br>
    </tr>
    <tr>
      <td>"s4"</td>
      <td>little endian<br>
      <td>signed integer<br>
      <td>4byte<br>
    </tr>
    <tr>
      <td>"u1"</td>
      <td>little endian<br>
      <td>unsigned integer<br>
      <td>1byte<br>
    </tr>
    <tr>
      <td>"u2"</td>
      <td>little endian<br>
      <td>unsigned integer<br>
      <td>2byte<br>
    </tr>
    <tr>
      <td>"u4"</td>
      <td>little endian<br>
      <td>unsigned integer<br>
      <td>4byte<br>
    </tr>
    <tr>
      <td>"f4"</td>
      <td>little endian<br>
      <td>single-precision real<br>
      <td>4byte<br>
    </tr>
    <tr>
      <td>"f8"</td>
      <td>little endian<br>
      <td>double-precision real<br>
      <td>8byte<br>
    </tr>
	 <tr>

  </tbody>
</table>