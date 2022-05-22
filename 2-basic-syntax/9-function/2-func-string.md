# 2.9.2 String Functions

Examples with var str="hello, world" executed;

<table>
  <thead>
    <tr>
      <th style="text-align:left">Function</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Example of usage</th>
      <th style="text-align:left">Result</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">bin(<b>a</b>)</td>
      <td style="text-align:left">Returns the string of number <b>a</b> in binary representation</td>
      <td style="text-align:left">bin(0b0010)</td>
      <td style="text-align:left">&quot;10&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">chr(<b>a</b>)</td>
      <td style="text-align:left">Returns the character with <b>a</b> of the ASCII code in string type</td>
      <td
      style="text-align:left">chr(65)</td>
        <td style="text-align:left">&quot;A&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">double(<b>s</b>)</td>
      <td style="text-align:left">Returns the real number type value of the real number string <b>s</b> (Interpret
        only up to the position where interpretation is possible, and discard the
        rest.)</td>
      <td style="text-align:left">double(&quot;29.38E-2&quot;)</td>
      <td style="text-align:left">0.2938</td>
    </tr>
    <tr>
      <td style="text-align:left">hex(<b>a</b>)</td>
      <td style="text-align:left">Returns the string of number <b>a</b> in hexadecimal representation</td>
      <td
      style="text-align:left">hex(0x7A2F)</td>
        <td style="text-align:left">&quot;7A2F&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">int(<b>s</b>)</td>
      <td style="text-align:left">Returns the integer type value of the integer string <b>s</b> (Interpret
        only up to the position where interpretation is possible, and discard the
        rest.)</td>
      <td style="text-align:left">
        <p>int(&quot;13.25&quot;)</p>
        <p>int(&quot;29.38E-2&quot;)</p>
      </td>
      <td style="text-align:left">
        <p>13</p>
        <p>29</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">left(<b>s</b>, <b>n</b>)</td>
      <td style="text-align:left">Returns a string of the first <b>n</b> characters of the string <b>s</b>
      </td>
      <td style="text-align:left">left(str, 3)</td>
      <td style="text-align:left">&quot;hel&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">len(<b>s</b>)</td>
      <td style="text-align:left">Returns the length of the string if <b>s</b> is a string and returns the
        number of elements in the array if <b>s</b> is an array</td>
      <td style="text-align:left">
        <p>len(&quot;HELLO&quot;)</p>
        <p>len([20, 30, 80])</p>
      </td>
      <td style="text-align:left">
        <p>5</p>
        <p>3</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">mid(<b>s</b>, <b>i</b>, <b>n</b>)</td>
      <td style="text-align:left">Returns a string of <b>n</b> characters starting from the <b>i</b>-th character
        of the string <b>s</b> (The position of the first character is 0.)</td>
      <td
      style="text-align:left">mid(str, 3, 5)</td>
        <td style="text-align:left">&quot;lo, w&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">mirror(<b>s</b>)</td>
      <td style="text-align:left">Returns the string inverted from the string <b>s</b>
      </td>
      <td style="text-align:left">mirror(&quot;HELLO&quot;)</td>
      <td style="text-align:left">&quot;OLLEH&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">right(<b>s</b>, <b>n</b>)</td>
      <td style="text-align:left">Returns a string of the last <b>n</b> characters of the string <b>s</b>
      </td>
      <td style="text-align:left">right(str, 3)</td>
      <td style="text-align:left">&quot;rld&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">str(<b>a</b>)</td>
      <td style="text-align:left">Returns a string of number <b>a</b> in decimal representation</td>
      <td style="text-align:left">str(13.25)</td>
      <td style="text-align:left">13.250000</td>
    </tr>
    <tr>
      <td style="text-align:left">strops(<b>s</b>, <b>p</b>)</td>
      <td style="text-align:left">Returns the first position in the string <b>s</b> that matches the string <b>p</b> (The
        first character position will be 0 or -1 if there is none.)</td>
      <td style="text-align:left">
        <p>strpos(str, &quot;llo&quot;)</p>
        <p>strpos(str, &quot;hi&quot;)</p>
      </td>
      <td style="text-align:left">
        <p>2</p>
        <p>-1</p>
      </td>
    </tr>
  </tbody>
</table>





