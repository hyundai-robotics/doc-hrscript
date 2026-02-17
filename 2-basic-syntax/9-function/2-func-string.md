# 2.9.2 字符串函数

执行带有 var str="hello, world" 的示例;

<table>
  <thead>
    <tr>
      <th style="text-align:left">函数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">用法示例</th>
      <th style="text-align:left">结果</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">bin(<b>a</b>)</td>
      <td style="text-align:left">返回数字 <b>a</b> 的二进制表示字符串</td>
      <td style="text-align:left">bin(0b0010)</td>
      <td style="text-align:left">&quot;10&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">chr(<b>a</b>)</td>
      <td style="text-align:left">返回字符串类型中 ASCII 码为 <b>a</b> 的字符</td>
      <td
      style="text-align:left">chr(65)</td>
        <td style="text-align:left">&quot;A&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">double(<b>s</b>)</td>
      <td style="text-align:left">返回实际数字字符串 <b>s</b> 的实数类型值（只解释到可以解释的位置，丢弃其余部分。）</td>
      <td style="text-align:left">double(&quot;29.38E-2&quot;)</td>
      <td style="text-align:left">0.2938</td>
    </tr>
    <tr>
      <td style="text-align:left">hex(<b>a</b>)</td>
      <td style="text-align:left">返回数字 <b>a</b> 的十六进制表示字符串</td>
      <td
      style="text-align:left">hex(0x7A2F)</td>
        <td style="text-align:left">&quot;7A2F&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">int(<b>s</b>)</td>
      <td style="text-align:left">返回整数字符串 <b>s</b> 的整数类型值（只解释到可以解释的位置，丢弃其余部分。）</td>
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
      <td style="text-align:left">返回字符串<b>s</b>的前<b>n</b>个字符的字符串
      </td>
      <td style="text-align:left">left(str, 3)</td>
      <td style="text-align:left">&quot;hel&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">len(<b>s</b>)</td>
      <td style="text-align:left">如果<b>s</b>是一个字符串，则返回字符串的长度；如果<b>s</b>是一个数组，则返回数组中的元素数量</td>
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
      <td style="text-align:left">返回从字符串<b>s</b>的第<b>i</b>个字符开始的<b>n</b>个字符的字符串（第一个字符的位置为0。）</td>
      <td
      style="text-align:left">mid(str, 3, 5)</td>
      <td style="text-align:left">&quot;lo, w&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">mirror(<b>s</b>)</td>
      <td style="text-align:left">返回从字符串<b>s</b>反转后的字符串
      </td>
      <td style="text-align:left">mirror(&quot;HELLO&quot;)</td>
      <td style="text-align:left">&quot;OLLEH&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">right(<b>s</b>, <b>n</b>)</td>
      <td style="text-align:left">返回字符串<b>s</b>的最后<b>n</b>个字符的字符串
      </td>
      <td style="text-align:left">right(str, 3)</td>
      <td style="text-align:left">&quot;rld&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">str(<b>a</b>)</td>
<td style="text-align:left">返回数字 <b>a</b> 的十进制表示字符串</td>
<td style="text-align:left">str(13.25)</td>
<td style="text-align:left">13.250000</td>
</tr>
<tr>
<td style="text-align:left">strpos(<b>s</b>, <b>p</b>)</td>
<td style="text-align:left">返回字符串 <b>s</b> 中匹配字符串 <b>p</b> 的第一个位置（如果没有匹配，则第一个字符位置将为 0 或 -1。）</td>
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