# 2.8 Operators and Expressions

In the following example, the variable margin is added to the number value 500, and the resulting value is divided by 2. Thus, the calculated value is assigned to a variable called “height.”

```python
var height, margin=10
height=(500+margin)/2
print height
```

Through the print statement, it is possible to check that 255, which is the result of the expression, is assigned to “height.”

In this way, an expression can be created by concatenating operands, which are values or variables, using various operators, and the result can be assigned to a variable or be used as a parameter of a statement.



What operation will be performed first if the addition sign and multiplication sign are used without grouping, as shown below? Multiplication and division will be performed first before addition and subtraction because there is an operation order in which operators are applied, which is called “operator precedence.” Because the operator precedence of multiplication is higher than that of addition, multiplication will be performed first even though the multiplication sign is located at a later place.



print 10+10\*2



Strings will be concatenated when the \(+\) operator is used for them.

```python
var name="axis1", type="rotational"
print name + ":" + type
```

The operators supported by HRScript are as follows. The higher it is, the higher the operator precedence. \(In other words, operators with higher operator precedence will be executed first.\)



<table>
  <thead>
    <tr>
      <th style="text-align:left">Operator</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">( )</td>
      <td style="text-align:left">Grouping</td>
      <td style="text-align:left">(10+10)*2 ; 40</td>
    </tr>
    <tr>
      <td style="text-align:left">[ ]</td>
      <td style="text-align:left">Accessing array elements</td>
      <td style="text-align:left">arr[3]</td>
    </tr>
    <tr>
      <td style="text-align:left">**</td>
      <td style="text-align:left">Exponentiation</td>
      <td style="text-align:left">10**3 ; 1000</td>
    </tr>
    <tr>
      <td style="text-align:left">+x, -x</td>
      <td style="text-align:left">Sign</td>
      <td style="text-align:left">-300</td>
    </tr>
    <tr>
      <td style="text-align:left">*, /, mod</td>
      <td style="text-align:left">Multiplication, division, remainder</td>
      <td style="text-align:left">300/3 ; 100, 8 mod 3 ; 2</td>
    </tr>
    <tr>
      <td style="text-align:left">+, -</td>
      <td style="text-align:left">Addition, subtraction</td>
      <td style="text-align:left">300-100 ; 200</td>
    </tr>
    <tr>
      <td style="text-align:left">~</td>
      <td style="text-align:left">Bitwise NOT</td>
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
        <p>Bitwise AND</p>
        <p>Bitwise XOR</p>
        <p>Bitwise OR</p>
        <p>Shift left</p>
        <p>Shift right (sign maintained)</p>
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
        <p>Comparison operation</p>
        <p>(!=) means different, (==) means equal.</p>
      </td>
      <td style="text-align:left">
        <p>30 &lt;= 29 ; false</p>
        <p>response != &quot;ok&quot;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">not x</td>
      <td style="text-align:left">Logical operation NOT</td>
      <td style="text-align:left">not error_state</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>and</p>
        <p>or</p>
      </td>
      <td style="text-align:left">
        <p>Logical operation AND</p>
        <p>Logical operation OR</p>
      </td>
      <td style="text-align:left">
        <p>height&gt;100 and invert==false</p>
        <p>timeout or work_count&gt;3</p>
      </td>
    </tr>
  </tbody>
</table>



When operands are number or Boolean values, the result of comparison and logical operations is a Boolean data type, and the result type of other operations is a number data type.



In cases where an operand of Boolean type is used without a comparison operator, it means whether its value is equal to true. For example, the two lines below have the same meaning.

```python
var result= timeout
var result= (timeout==true)
```

Operators that can be used for strings are addition \(+\), comparison \(!=, ==\), and assignment \(=\). String addition makes it possible to concatenate operand strings, as previously shown. 

A comparison operation determines whether a string is different or equal.



```python
var response="ok"
print response=="ok"
print response=="ng"
```

Sometimes, the data type of an operand may change automatically during the process of operation.

When a number is used as an operand of a logical operator, the result will be regarded as false if it is 0 and true if it is not.

```python
var count_a=1, count_b=0, height=100
print count_a and height>99
print count_b and height>99
```

“bitwise NOT” and “shift left/right” are calculated on a 32-bit length basis.

