# 2.8 연산자와 수식

아래의 예를 보면 숫자 값 500에 변수 margin을 더한 후 2로 나누어 height라는 변수에 대입하고 있습니다.

```python
var height, margin=10
height=(500+margin)/2
print height
```

height에는 수식의 결과 값인 255가 대입된 것을 print문으로 확인할 수 있습니다.

이와 같이 값이나 변수인 피연산자\(operand\)들을 다양한 연산자\(operator\)로 연결하여 수식\(expression\)을 작성할 수 있고 그 결과를 변수에 대입하거나, 명령문의 파라미터로 사용할 수 있습니다.



아래와 같이 덧셈과 곱셈을 괄호없이 쓰면 어떤 연산이 먼저 수행될까요? 덧셈, 뺄셈보다 곱셈, 나눗셈을 먼저 한다는 걸 알고 있지요? 이처럼 연산자들 사이에는 수행되는 순서가 있으며 이를 연산자 우선순위\(operator precedence\)라고 합니다. 곱셈의 우선순위가 덧셈보다 높기 때문에 뒤에 있지만 먼저 수행되는 것입니다.



print 10+10\*2



문자열에 대해서도 + 연산자를 사용하면 문자열들이 연결\(concatenate\)됩니다.



```python
var name="axis1", type="rotational"
print name + ":" + type
```

HRScript가 지원하는 연산자는 아래와 같습니다. 위에 있을수록 연산자 우선순위가 높습니다. \(즉, 먼저 수행됩니다.\)

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#xC5F0;&#xC0B0;&#xC790;</th>
      <th style="text-align:left">&#xC758;&#xBBF8;</th>
      <th style="text-align:left">&#xC608;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">( )</td>
      <td style="text-align:left">&#xAD04;&#xD638; (grouping)</td>
      <td style="text-align:left">(10+10)*2 ; 40</td>
    </tr>
    <tr>
      <td style="text-align:left">[ ]</td>
      <td style="text-align:left">&#xBC30;&#xC5F4; &#xC694;&#xC18C; &#xC811;&#xADFC;</td>
      <td style="text-align:left">arr[3]</td>
    </tr>
    <tr>
      <td style="text-align:left">**</td>
      <td style="text-align:left">&#xC2B9; (exponentiation)</td>
      <td style="text-align:left">10**3 ; 1000</td>
    </tr>
    <tr>
      <td style="text-align:left">+x, -x</td>
      <td style="text-align:left">&#xBD80;&#xD638; (sign)</td>
      <td style="text-align:left">-300</td>
    </tr>
    <tr>
      <td style="text-align:left">*, /, mod</td>
      <td style="text-align:left">&#xACF1;&#xC148;, &#xB098;&#xB217;&#xC148;, &#xB098;&#xBA38;&#xC9C0;</td>
      <td
      style="text-align:left">300/3 ; 100, 8 mod 3 ; 2</td>
    </tr>
    <tr>
      <td style="text-align:left">+, -</td>
      <td style="text-align:left">&#xB367;&#xC148;, &#xBE84;&#xC148;</td>
      <td style="text-align:left">300-100 ; 200</td>
    </tr>
    <tr>
      <td style="text-align:left">~</td>
      <td style="text-align:left">bitwise NOT</td>
      <td style="text-align:left">
        <p>~0b11010010
          <br />
        </p>
        <p>; 0b11111111111111111111111100101101
          <br />
        </p>
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
        <p>bitwise AND
          <br />
        </p>
        <p>bitwise XOR
          <br />
        </p>
        <p>bitwise OR
          <br />
        </p>
        <p>shift left
          <br />
        </p>
        <p>shift right (&#xBD80;&#xD638;&#xC720;&#xC9C0;)
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>0b11010010 &amp; 0b11110000 ; 0xd0
          <br />
        </p>
        <p>0b11010010 ^ 0b11110000 ; 0x22
          <br />
        </p>
        <p>0b11010010 | 0b11110000 ; 0xf2
          <br />
        </p>
        <p>0b11010010 &lt;&lt; 2 ; 0b1101001000
          <br />
        </p>
        <p>0b11010010 &gt;&gt; 2 ; 0b00110100
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&lt;, &lt;=, &gt;, &gt;=,
          <br />
        </p>
        <p>!=, ==
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>&#xBE44;&#xAD50;&#xC5F0;&#xC0B0;
          <br />
        </p>
        <p>!=&#xB294; &#xB2E4;&#xB974;&#xB2E4;. ==&#xB294; &#xAC19;&#xB2E4;.
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>30 &lt;= 29 ; false
          <br />
        </p>
        <p>response != &quot;ok&quot;
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">not x</td>
      <td style="text-align:left">&#xB17C;&#xB9AC;&#xC5F0;&#xC0B0; NOT</td>
      <td style="text-align:left">not error_state</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>and
          <br />
        </p>
        <p>or
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>&#xB17C;&#xB9AC;&#xC5F0;&#xC0B0; AND
          <br />
        </p>
        <p>&#xB17C;&#xB9AC;&#xC5F0;&#xC0B0; OR
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>height&gt;100 and invert==false
          <br />
        </p>
        <p>timeout or work_count&gt;3
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

피연산자가 수치나 bool값일 경우, 비교연산과 논리연산의 결과는 bool자료형이며, 나머지 연산의 결과 형은 숫자 자료형입니다.



bool형의 피연산자를 비교연산자 없이 그대로 쓰면, 그 값이 true와 같은지를 뜻합니다. 예를 들어 아래의 두 행은 의미가 같습니다.

```python
var result= timeout
var result= (timeout==true)
```



문자열에 대해 사용할 수 있는 연산자는 덧셈\(+\)과 비교연산\(!=, ==\), 대입연산\(=\)입니다. 문자열 덧셈은 피연산자 문자열들을 연결\(concatenate\)하며, 앞서 예를 보인 바 있습니다.

비교연산은 문자열이 다른지 같은지를 판단합니다.

```python
var response="ok"
print response=="ok"
print response=="ng"
```

간혹, 연산과정에서 피연산자의 자료형이 자동으로 바뀌는 경우도 있습니다.

논리연산자의 피연산자로 수치를 사용할 경우, 수치가 0이면 false, 0이 아니면 true로 간주합니다.

```python
var count_a=1, count_b=0, height=100
print count_a and height>99
print count_b and height>99
```

bitwise NOT과 shift left/right는 32bit 길이를 기반으로 계산합니다.

