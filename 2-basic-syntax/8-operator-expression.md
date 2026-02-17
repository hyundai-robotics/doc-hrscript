# 2.8 操作符和表达式

在以下示例中，变量 margin 被添加到数字值 500，得到的值被除以 2。这样，计算出的值被赋值给一个名为 "height" 的变量。

```python
var height, margin=10
height=(500+margin)/2
print height
```

通过 print 语句，可以检查到表达式的结果 255 被赋值给 "height"。

通过这种方式，可以通过使用各种操作符连接操作数（即值或变量）来创建表达式，并将结果赋值给变量或用作语句的参数。

如果像下面这样在没有分组的情况下同时使用加号和乘号，首先会执行什么操作？由于存在操作顺序，即所谓的 "操作符优先级"，乘法和除法会在加法和减法之前执行。因为乘法的操作符优先级高于加法，即使乘号位于较后的位置，乘法也会首先执行。

print 10+10\*2

当对字符串使用 \(+\) 操作符时，字符串将被连接。

```python
var name="axis1", type="rotational"
print name + ":" + type
```

HRScript 支持的操作符如下。越往上，操作符优先级越高。 \(换句话说，优先级高的操作符会首先执行。\)

<table>
  <thead>
    <tr>
      <th style="text-align:left">操作符</th>
      <th style="text-align:left">含义</th>
      <th style="text-align:left">示例</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">( )</td>
      <td style="text-align:left">分组</td>
      <td style="text-align:left">(10+10)*2 ; 40</td>
    </tr>
    <tr>
<td style="text-align:left">[ ]</td>
<td style="text-align:left">访问数组元素</td>
<td style="text-align:left">arr[3]</td>
</tr>
<tr>
<td style="text-align:left">**</td>
<td style="text-align:left">指数运算</td>
<td style="text-align:left">10**3 ; 1000</td>
</tr>
<tr>
<td style="text-align:left">+x, -x</td>
<td style="text-align:left">符号</td>
<td style="text-align:left">-300</td>
</tr>
<tr>
<td style="text-align:left">*, /, mod</td>
<td style="text-align:left">乘法，除法，余数</td>
<td style="text-align:left">300/3 ; 100, 8 mod 3 ; 2</td>
</tr>
<tr>
<td style="text-align:left">+, -</td>
<td style="text-align:left">加法，减法</td>
<td style="text-align:left">300-100 ; 200</td>
</tr>
<tr>
<td style="text-align:left">~</td>
<td style="text-align:left">按位非</td>
<td style="text-align:left">
<p>~0b11010010</p>
<p>; 0b11111111111111111111111100101101</p>
</td>
</tr>
<tr>
<td style="text-align:left">
<p>&amp;</p>
<p>^</p>
<p>|</p>
<p>&lt;&lt;</p>
<p>&gt;&gt;</p>
</td>
<td style="text-align:left">
<p>按位与</p>
<p>按位异或</p>
<p>按位或</p>
<p>左移</p>
<p>右移（保持符号）</p>
</td>
<td style="text-align:left">
<p>0b11010010 &amp; 0b11110000 ; 0xd0</p>
<p>0b11010010 ^ 0b11110000 ; 0x22</p>
<p>0b11010010 | 0b11110000 ; 0xf2</p>
<p>0b11010010 &lt;&lt; 2 ; 0b1101001000</p>
<p>0b11010010 &gt;&gt; 2 ; 0b00110100</p>
</td>
</tr>
<tr>
  <td style="text-align:left">
    <p>&lt;, &lt;=, &gt;, &gt;=,</p>
    <p>!=, ==</p>
  </td>
  <td style="text-align:left">
    <p>比较操作</p>
    <p>(!=)表示不同，(==)表示相等。</p>
  </td>
  <td style="text-align:left">
    <p>30 &lt;= 29 ; false</p>
    <p>response != &quot;ok&quot;</p>
  </td>
</tr>
<tr>
  <td style="text-align:left">not x</td>
  <td style="text-align:left">逻辑操作 NOT</td>
  <td style="text-align:left">not error_state</td>
</tr>
<tr>
  <td style="text-align:left">
    <p>和</p>
    <p>或</p>
  </td>
  <td style="text-align:left">
    <p>逻辑操作 AND</p>
    <p>逻辑操作 OR</p>
  </td>
  <td style="text-align:left">
    <p>height&gt;100 and invert==false</p>
    <p>timeout or work_count&gt;3</p>
  </td>
</tr>
</tbody>
</table>

当操作数为数字或布尔值时，比较和逻辑操作的结果为布尔数据类型，而其他操作的结果类型为数字数据类型。

在没有使用比较运算符的情况下，布尔类型的操作数表示其值是否等于 true。例如，下面的两行具有相同的含义。

```python
var result= timeout
var result= (timeout==true)
```
可以用于字符串的操作符有加法 \(+\)、比较 \(!=, ==\) 和赋值 \(=\)。字符串加法使得可以连接操作数字符串，如前所示。

比较操作决定一个字符串是否不同或相等。

```python
var response="ok"
print response=="ok"
print response=="ng"
```

有时，操作数的数据类型可能在操作过程中自动改变。

当一个数字与一个字符串使用比较操作符进行比较时，它们将被视为字符串进行比较。

```python
print 123=="123" # true
```

当数字作为逻辑操作符的操作数时，如果它为0，结果将被视为false；如果不是0，结果将被视为true。

```python
var count_a=1, count_b=0, height=100
print count_a and height>99
print count_b and height>99
```

“按位取反”和“左移/右移”是在32位长度基础上计算的。