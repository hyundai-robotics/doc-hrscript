
[__SOURCE](README.md)
# ${cont_model} Controller Function Manual - Robot Language HRScript

[__SOURCE](0-about-this-manual/precautions.md)
# Precautions

{% include url="https://hrcontentsrelay-bmgae5hdbzapc4bc.koreacentral-01.azurewebsites.net/api/proxy?path=doc-common-pages/en/precautions.md" %}

[__SOURCE](1-intro/README.md)
# 1. Overview

  



[__SOURCE](1-intro/1-hrscript.md)
# 1.1 Introduction of HRScript

HD Hyundai Robotics' ${cont_model} Controller allows the user to program the robot's tasks in a robot language called HRScript. Created programs can be saved as several files with the extension .job.

HRScript is a scripting language that will be interpreted and executed line by line by the interpreter without a compilation procedure. It is similar to the Python or JavaScript languages but has a simpler syntax.




[__SOURCE](2-basic-syntax/README.md)
# 2. Basic Syntax

Described in this section are the basic terms of HRScript. The basic concept of the job program could be understood by following the method for defining a variable, constructing a simple expression using operators, and assigning the resulting value to a variable.


[__SOURCE](2-basic-syntax/1-statements.md)
# 2.1 Statements

The statement refers to each command string that becomes the execution unit of the job program. HRScript allows only one statement per line. Take note of how the four examples of statements are written below, particularly their appearances.

```python
     move P,po3,spd=80%,accu=1,tool=3 until do33
10   z_pos = (base_height+offset)*1.05
     # robot has to wait sensor2 input
     *err_handle
```

For statements other than a step statement \(move statements, etc.\) that moves the robot, you can optionally add a line number \(1 to 9999\) at the beginning of the line. The number 10 in the second line is an example of a line number.

It does not matter if there are any number of spaces or tabs before and after the statement.

Proper indentation in statements is recommended for readability. Both spaces and tabs are allowed for indentation and do not affect the operation during execution.






[__SOURCE](2-basic-syntax/2-identifier.md)
# 2.2 Identifiers

Names must be given to commands, variables, functions, and labels that are described. These names are collectively referred to as `identifiers.` When deciding an identifier, it must comply with the following rules for the HRScript's identifiers.

* It must consist only of uppercase and lowercase letters, numbers, and underscores.
* It is case-sensitive. (except for top-level array names in global variables)
* The first character must only be either a lowercase or uppercase letter or an underscore, not a number.
* It should not contain a space or tab.
* Identifiers already defined in the system, such as `if` and `for` cannot be used.
* There is no limit to the length.

The following shows correct and incorrect examples of identifiers:

```text
myvar (O) 
myvar2 (O)
_myvar (O)
MyVar (O)
310a (X) - Started with a number
move (X) - An identifier already defined in the system
v300$ (X) - Used a symbol other than an underscore ($)
my var (X) - Included a space
```

{% hint style="warning" %}

Exceptionally, the names of top-level arrays in global variables are not case-sensitive.
(It is because top-level global arrays are saved as .csv files, and file names are case-insensitive.)

For example, the following two variables cannot be used together:

    global MyArr = Array(10)
    global myarr = Array(10)

{% endhint %}

[__SOURCE](2-basic-syntax/3-statement-type/README.md)
# 2.3 Types of Statements

The four types of statements of HRScript are as follows:



* procedure
* assignment
* comment
* label




[__SOURCE](2-basic-syntax/3-statement-type/1-procedure.md)
# 2.3.1 Procedures

A procedure consists of a command and a 0-N number of parameters.

```python
move P,po3,spd=80%,accu=1,tool=3 until do33
```

The three types of procedure parameters are as follows:

| Type | Syntax | Example |
| :--- | :--- | :--- |
| Position parameter | &lt;value&gt; | P, po3 |
| Keyword parameter | &lt;keyword&gt; = &lt;value&gt; | spd=80%, accu=1, tool=3 |
| Preposition parameter | &lt;preposition&gt;  &lt;value&gt; | until do33 |

The position parameter"s role is determined by its position, so it should not be moved and must always be at the front of the procedure. 

Keyword parameters should be placed after position parameters. However, the order between keyword parameters does not affect the operation.



The preposition parameters are placed last.






[__SOURCE](2-basic-syntax/3-statement-type/2-assignment.md)
# 2.3.2 Assignment Statements

An assignment statement consists of the left side, the assignment operator \(=\), and the right side. The left side \(lvalue\) must be a variable that can store a value. No constants or expressions are allowed. 

On the other hand, constants, variables, and expressions are allowed on the right side \(rvalue\).



```python
height=(500+margin)/2
```


[__SOURCE](2-basic-syntax/3-statement-type/3-comment.md)
# 2.3.3 Comment Statements

A comment statement is used to describe the contents of the job program in a way that they can be understood easily. Even if the comment statement is executed, no operation is performed. As shown below, a description is attached after the hash sign \(\#\). It can be used as a single statement or attached after another statement.

```python
# robot has to wait sensor2 input
var work_w,work_h  # width and height of a workpiece
```




[__SOURCE](2-basic-syntax/3-statement-type/4-label.md)
# 2.3.4 Labels

A label is used to mark the target point to move to according to the goto statement. It consists of an asterisk \(\*\) and an identifier.


[__SOURCE](2-basic-syntax/4-hello-world.md)
# 2.4 First Program - Hello, World!

Let us create a simple job program that prints a string on the teach pendant screen. After creating a new job, record the print statement as shown below, and attach the string parameter "Hello, World!"

```python
print "Hello, World !"
```

The print statement is used to print the value at the bottom of the teach pendant's job panel. Now, when you run the program, you can see the text, "Hello, World!" printed at the bottom of the job panel.

[__SOURCE](2-basic-syntax/5-type/README.md)
# 2.5 Data Type


[__SOURCE](2-basic-syntax/5-type/1-type-string.md)
# 2.5.1 String Data Type

The first program in the previous paragraph used the data "Hello, World!" as the print statement"s parameter, a string data type. The value of the string data type begins and ends with double quotes. There is no limit for the length of the string.

```python
print "Welcome to the Robot World."
```

A sequence beginning with a backslash \(\\) represents double quotes or special characters in a string. This sequence is called the "escape character."

The supported escape characters are shown in the table below.



|  |  |
| :--- | :--- |
| \" | Double quotes |
| \\ | Backslash |
| \t | Tab |
| \n | New line character |

```python
print "Message:\nPlease, press \"OK\" button."

# Result of print
Message:
Please, press "OK" button.
```




[__SOURCE](2-basic-syntax/5-type/2-number-type.md)
# 2.5.2 Number Data Type

The number data type stores an integer or real number. Let us print using the print statement. If you list multiple values separated by commas \(,\) in the print statement, as shown in the example below, each value will be displayed separated by a space.

```python
280
3.141592
-99
print 280, -99
```

Inside the system, integers and real numbers are processed separately. Each data size is as follows:

| Data type | Data size \(byte\) |
| :--- | :--- |
| Integer | 4 |
| Real number | 8 |




[__SOURCE](2-basic-syntax/5-type/3-bool-type.md)
# 2.5.3 Boolean Data Type

There are only two values, true and false, as the result of the following logic and comparison operations.

```python
var x=true
print false and x
print 10 > 5
print 10 <= 5

# Result of print
false
true
false
```




[__SOURCE](2-basic-syntax/5-type/4-array-object-type.md)
# 2.5.4 Array Type and Object Type

In addition, there are array types and object types. These will be discussed in further detail in Sections 4.1 and 4.2.


[__SOURCE](2-basic-syntax/6-variable.md)
# 2.6 Variables

A variable can store values and has an identifier name. Variables are divided into global and local variables, and the difference between them will be described later. Examples of local variables are first described here.



Variables can be created with the var command, as shown in the following. This is called defining a variable. Multiple identifiers can be created at once by enumerating multiple identifiers after the var command.



```python
var myvar
var width, height, depth
```

Storing a value in a variable is called "assignment." The assignment may be performed while defining or after defining a variable. If the assignment is not performed while defining, the variable will have a number value of 0 by default.

```python
var myvar=0
var message, width=200
message="Invalid input value"
```

In HRScript, \(=\) does not mean equal. It is used as an assignment operator and means that the value on the operator"s right side is assigned to the variable on the left side. The value stored in the variable may be printed through the print statement.

```python
var myvar=0
var message, width=200
message="Invalid input value"
print width, message
```

A different value may be assigned to a variable to which a value has already been assigned. It is called a variable because its value can change.

```python
var width=200
width=300
```




[__SOURCE](2-basic-syntax/7-binary-hex-number.md)
# 2.7 Binary and Hexadecimal

All the number type values previously described as examples are interpreted as decimal numbers. It can represent binary or hexadecimal values just by adding 0b or 0x prefixes, respectively, as shown in the following.

```python
var binary = 0b10010011
var hexadecimal = 0xFF4A38C0
```


[__SOURCE](2-basic-syntax/8-operator-expression.md)
# 2.8 Operators and Expressions

In the following example, the variable margin is added to the number value 500, and the resulting value is divided by 2. Thus, the calculated value is assigned to a variable called "height."

```python
var height, margin=10
height=(500+margin)/2
print height
```

Through the print statement, it is possible to check that 255, which is the result of the expression, is assigned to "height."

In this way, an expression can be created by concatenating operands, which are values or variables, using various operators, and the result can be assigned to a variable or be used as a parameter of a statement.



What operation will be performed first if the addition sign and multiplication sign are used without grouping, as shown below? Multiplication and division will be performed first before addition and subtraction because there is an operation order in which operators are applied, which is called "operator precedence." Because the operator precedence of multiplication is higher than that of addition, multiplication will be performed first even though the multiplication sign is located at a later place.



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

When a number is compared with a string with the comparison operator, it compares them as strings.

```python
print 123=="123" # true
```

When a number is used as an operand of a logical operator, the result will be regarded as false if it is 0 and true if it is not.

```python
var count_a=1, count_b=0, height=100
print count_a and height>99
print count_b and height>99
```

"bitwise NOT" and "shift left/right" are calculated on a 32-bit length basis.


[__SOURCE](2-basic-syntax/9-function/README.md)
# 2.9 Functions

What is the process of converting the angle 60° to a radian value or finding the length of the string that the variable mystr contains? 

HRScript provides various functions that receive inputs through parameters, perform some processing, and return the result values. 

Functions can be used as part of an expression, as shown below.

```python
var dg=60, rd
rd=deg2rad(dg)

var limit=40, message="Input your code number"
var validity= len(message) < limit
```

The list of functions provided in HRScript is as follows. \(The tables are sorted in the ascending order of names.\)


[__SOURCE](2-basic-syntax/9-function/1-func-math.md)
# 2.9.1 Math Functions

<table style="text-align:left">
  <thead>
    <tr>
      <th>Function</th>
      <th>Description</th>
      <th>Example of usage</th>
      <th>Result</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>abs(<b>a</b>)</td>
      <td>Returns the absolute value of <b>a</b>
      </td>
      <td>abs(-300)</td>
      <td>300</td>
    </tr>
    <tr>
      <td>acos(<b>a</b>)</td>
      <td>Returns the arc cosine value of <b>a</b> in radian format</td>
      <td>acos(0.5)</td>
      <td>1.0472</td>
    </tr>
    <tr>
      <td>asin(<b>a</b>)</td>
      <td>Returns the arc sine value of <b>a</b> in radian format</td>
      <td>asin(0.5)</td>
      <td>0.5236</td>
    </tr>
    <tr>
      <td>atan(<b>a</b>)</td>
      <td>Returns the arc tangent value of <b>a</b> in radian format</td>
      <td>atan(0.5)</td>
      <td>0.4636</td>
    </tr>
    <tr>
      <td>atan2(<b>a</b>, <b>b</b>)</td>
      <td>Returns the arc tangent value of a triangle with <b>a</b> for the y length
        and <b>b</b> for the x length in radian format</td>
      <td>atan2(2,1)</td>
      <td>1.1071</td>
    </tr>
		<tr>
			<td>ceil(x)</td>
			<td>Returns the rounded up value of <b>x</b>.</td>
			<td>
				ceil(3.1415)<br>
				ceil(-3.1415)
			</td>
				<td>
				4<br>
				-3
				</td>
		</tr>
    <tr>
      <td>cos(<b>r</b>)</td>
      <td>Returns the cosine value of <b>r</b> in radian format</td>
      <td>cos(3.1415)</td>
      <td>-1</td>
    </tr>
    <tr>
      <td>deg2rad(<b>d</b>)</td>
      <td>Returns the radian value of <b>d</b> in degree format</td>
      <td>deg2rad(-90)</td>
      <td>-1.570796</td>
    </tr>
    <tr>
      <td>dist(<b>x</b>, <b>y</b>)</td>
      <td>Returns the Euclidean distance from the origin to the (<b>x</b>, <b>y</b>)
        coordinate</td>
      <td>dist(3.5,10)</td>
      <td>10.59481</td>
    </tr>
		<tr>
			<td>floor(x)</td>
			<td>Returns the rounded down value of <b>x</b>.</td>
			<td>
				floor(3.1415)<br>
				floor(-3.1415)
			</td>
			<td>
				3<br>
				-4
			</td>
		</tr>
    <tr>
      <td>max(<b>a</b>, <b>b</b>)</td>
      <td>Returns the greater value between <b>a</b> and <b>b</b>
      </td>
      <td>max(-1.23, -3)</td>
      <td>-1.23</td>
    </tr>
    <tr>
      <td>min(<b>a</b>, <b>b</b>)</td>
      <td>Returns the lesser value between <b>a</b> and <b>b</b>
      </td>
      <td>max(-1.23, -3)</td>
      <td>-3</td>
    </tr>
    <tr>
      <td>near(<b>a</b>, <b>b</b> [,<b>e</b>])</td>
      <td>Returns 1 if the difference between the real number values &#x200B;&#x200B;<b> a</b> and <b>b</b> is
        less than or equal to <b>e</b> and returns 0 if the difference is larger
        than <b>e</b>
      </td>
      <td>
        <p>near(0.005, 0.0058)</p>
        <p>near(0.005, 0.006)</p>
        <p>near(0.005, 0.006, 0.1)</p>
      </td>
      <td>
        <p>1</p>
        <p>0</p>
        <p>1</p>
      </td>
    </tr>
    <tr>
      <td>rad2deg(<b>r</b>)</td>
      <td>Returns the degree value of <b>r</b> in radian format</td>
      <td>rad2deg(1.570796)</td>
      <td>90</td>
    </tr>
		<tr>
			<td>round(x)</td>
			<td>Returns the rounded off value of <b>x</b>.</td>
			<td>
				round(3.1415)<br>
				round(3.7415)<br>
				round(-3.1415)<br>
				round(-3.7415)
			</td>
				<td>
				3<br>
				4<br>
				-3<br>
				-4
				</td>
		</tr>
    <tr>
      <td>sin(<b>r</b>)</td>
      <td>Returns the sine value of <b>r</b> in radian format</td>
      <td>sin(1.5*3.1415)</td>
      <td>-1</td>
    </tr>
    <tr>
      <td>sqr(<b>a</b>)</td>
      <td>Returns the square root of <b>a</b>
      </td>
      <td>
        <p>sqr(16)</p>
        <p>sqr(0)</p>
      </td>
      <td>
        <p>4</p>
        <p>0</p>
      </td>
    </tr>
    <tr>
      <td>tan(<b>r</b>)</td>
      <td>Returns the tangent value of <b>r</b> in radian format</td>
      <td>tan(3.141592/4)</td>
      <td>0.9999</td>
    </tr>
		<tr>
			<td>trunc(x)</td>
			<td>Returns the the truncated integer part of <b>x</b>.</td>
			<td>
				trunc(3.1415)<br>
				trunc(-3.1415)
			</td>
			<td>
				3<br>
				-3
			</td>
		</tr>
		<tr>
			<td>val_as(format, v)</td>
			<td>
      Returns the binary data of the v value reinterpreted by the format.<br>
			For supported format, refer to below [Table 1].
			</td>
			<td>
				val_as("u1", -127)<br>
				val_as("u2", -2)<br>
				val_as("s4", -2147483648)<br>
				val_as("S4", -2147483648)
			</td>
			<td>
				129<br>
				0xfffe<br>
				0x80000000<br>
				0x00000080
			</td>
		</tr>
  </tbody>
</table>

[Table 1] The supported formats of `val_as()` function

<table style="text-align:left">
	<thead>
		<tr>
			<th>endian</th>
			<th>format</th>
			<th>meaning</th>
		</tr>
	</thead>
	<tbody>
		<tr><td rowspan="7">little<br>endian</td>
		     <td>u1</td><td>unsigned 1 byte</td></tr>
		<tr><td>u2</td><td>unsigned 2 byte</td></tr>
		<tr><td>s1</td><td>signed 1 byte</td></tr>
		<tr><td>s2</td><td>signed 2 byte</td></tr>
		<tr><td>s4</td><td>signed 4 byte</td></tr>
		<tr><td>f4</td><td>float 4 byte</td></tr>
		<tr><td>f8</td><td>double 8 byte</td></tr>
		<tr><td rowspan="7">big<br>endian</td>
		     <td>U1</td><td>unsigned 1 byte</td></tr>
		<tr><td>U2</td><td>unsigned 2 byte</td></tr>
		<tr><td>S1</td><td>signed 1 byte</td></tr>
		<tr><td>S2</td><td>signed 2 byte</td></tr>
		<tr><td>S4</td><td>signed 4 byte</td></tr>
		<tr><td>F4</td><td>float 4 byte</td></tr>
		<tr><td>F8</td><td>double 8 byte</td></tr>
	</tbody>
</table>




[__SOURCE](2-basic-syntax/9-function/2-func-string.md)
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
      <td style="text-align:left">strpos(<b>s</b>, <b>p</b>)</td>
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






[__SOURCE](2-basic-syntax/9-function/3-func-datetime.md)
# 2.9.3 Date and Time Functions

<table>
  <thead>
    <tr>
      <th style="text-align:right">Function</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Example of usage</th>
      <th style="text-align:left">Result</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:right">date( )</td>
      <td style="text-align:left">
        <p>Returns the current date in string type</p>
        <p>(YYYY-MM-DD format)</p>
      </td>
      <td style="text-align:left">date( )</td>
      <td style="text-align:left">&quot;2019-04-17&quot;</td>
    </tr>
    <tr>
      <td style="text-align:right">time( )</td>
      <td style="text-align:left">
        <p>Returns the current time in string type</p>
        <p>(HH:MM:SS format)</p>
      </td>
      <td style="text-align:left">time( )</td>
      <td style="text-align:left">&quot;08:48:14&quot;</td>
    </tr>
    <tr>
      <td style="text-align:right">timer( )</td>
      <td style="text-align:left">Returns the time elapsed in seconds (sec) from when the power was turned
        on</td>
      <td style="text-align:left">timer( )</td>
      <td style="text-align:left">2796.37</td>
    </tr>
  </tbody>
</table>


[__SOURCE](2-basic-syntax/9-function/4-func-creator.md)
# 2.9.4 Constructor Functions

These functions receive an input of a parameter and then create and return an object.

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
      <td style="text-align:left">
        <p>Array(n)</p>
        <p>Array(a, b, c)</p>
      </td>
      <td style="text-align:left">
        <p>Creates and returns an array of &#x201C;n&#x201D; elements</p>
        <p>The initial value of the element is 0.</p>
        <p>A multidimensional array is created if two or more elements are designated.</p>
        <p>Refer to &quot;<a href="../../4-array-object/1-array/3-array-creator">4.1.3 Array Constructor Function - Array()</a>&quot;.</p>
      </td>
      <td style="text-align:left">
        <p>Array(900)</p>
        <p>Array(3,4)</p>
      </td>
      <td style="text-align:left">
        <p>Array [900]</p>
        <p>Array [3] [4]</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Pose(element)</td>
      <td style="text-align:left">
        <p>Creates and returns a pose object</p>
        <p>Refer to &quot;<a href="../../5-moving-robot/1-pose.md">5.1 Pose</a>&quot;.</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Pose object</td>
    </tr>
    <tr>
      <td style="text-align:left">Shift(element)</td>
      <td style="text-align:left">
        <p>Creates and returns a shift object</p>
        <p>Refer to &quot;<a href="../../5-moving-robot/2-shift.md">5.2 Shift</a>&quot;.</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Shift object</td>
    </tr>
  </tbody>
</table>




[__SOURCE](2-basic-syntax/9-function/5-func-etc.md)
# 2.9.5 Other Functions

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
      <td style="text-align:left">cpo(crd, mode)</td>
      <td style="text-align:left">
        <p>Returns the current pose of the robot to the "crd" coordinate
          system</p>
        <p>For values that can be used as "crd" elements, see the table
          under "<a href="../../5-moving-robot/1-pose.md">5.1 Pose</a>".</p>
        <p>If the mode is "cmd," it is the command value, and if the mode is "cur," it is the current value.</p>
        <p>The "crd" and "mode" parameters may be omitted,
          and their default values are "base" and "cur,"
          respectively.</p>
      </td>
      <td style="text-align:left">cpo("joint", "cmd")</td>
      <td style="text-align:left">Pose* that stores the command value of the robot to the axis coordinate
        system</td>
    </tr>
    <tr>
      <td style="text-align:left">gather_state()</td>
      <td style="text-align:left">Returns the current state of data gathering by executing <a href="../../10-etc/1-proc/1-gather.md">gather</a> statement</td>
      <td style="text-align:left">gather_state()</td>
      <td style="text-align:left">
        0 : not in gathering.<br>
        1 : in gathering.<br>
        2 : saving the gathering result as a file.
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>mkucs(n,po)</p>
        <p>mkucs(n,po1,po2,po3)</p>
        <p>mkucs(n,"OXY",po1,po2,po3)</p>
      </td>
      <td style="text-align:left">
        <p>Creates and registers the nth user coordinate system object</p>
        <p>Refer to "<a href="../../5-moving-robot/5-ucs.md">5.5 User Coordinate System (UCS)</a>".</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>0: OK</p>
        <p>&lt;0: Error code</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">result()</td>
      <td style="text-align:left">For some procedures, it may be necessary to check the results. If the result() function is called right after the procedure is executed, the execution result can be returned.</td>
      <td style="text-align:left">result()</td>
      <td style="text-align:left"></td>
    </tr>
   <tr>
      <td style="text-align:left">mkshift(3,ref_po,mea_po,2.0) <br>
      mkshift(5,ref_po,mea_sft)
      </td>
      <td style="text-align:left">The optimized shift value is calculated and returned from the measured pose or shift data corresponding to multiple reference poses. <br>
      If the 4th parameter corresponding to tolerance is specified to be greater than 0 and the calculated shift value is greater than this value, it stops with an error. <br>
      # Note <br>
      ref_po (reference pose) and mea_po (measured pose) are the array types of pose variables, and mea_sft (measured shift) is the type of array of shift variables. <br>
      If there is no 4th parameter corresponding to tolerance, no error is detected. <br>
      We currently support up to 100 positions.
      </td>
      <td style="text-align:left">sft1=mkshift(4,ref_po,mea_po,3.0)</td>
      <td style="text-align:left">Shift</td>
    </tr> 
    <tr>
      <td style="text-align:left">calshift(po1,po2) <br>
      calshift(po1,po2,"TV")
      </td>
      <td style="text-align:left">Returns the difference between two poses as a shift value. <br>
      If the "TV" parameter is present, the vertical orientation of the tool is returned as a shift value.
      </td>
      <td style="text-align:left">sft1=calshift(po1,po2)</td>
      <td style="text-align:left">Shift</td>
    </tr> 
    <tr>
      <td style="text-align:left">po.valid()
      </td>
      <td style="text-align:left">
        Returns information about the pose object whether it is within the robot's motion range. <br>
        # Example <br>
        if po1.valid()==0 <br>
            stop # Robot stop<br>
        endif <br>        
      </td>
      <td style="text-align:left">var ret=po1.valid()
      </td>
      <td style="text-align:left">0:Outside the operating range <br>
      1:Within operating range
      </td>
    </tr>
    <tr>
      <td style="text-align:left">po.str_array()
      </td>
      <td style="text-align:left">
        Returns information about the pose object as a string in array format. <br>
        # Example <br>
        var msg=cpo().str_array() <br>
        print msg # [1850.000,2010.500,0.000,0.000,-90.000,0.000,"base"]
      </td>
      <td style="text-align:left">msg=po1.str_array()
      </td>
      <td style="text-align:left">String</td>
    </tr>
    <tr>
      <td style="text-align:left">sft.str_array()
      </td>
      <td style="text-align:left">
        Returns information about the shift object as a string in array format. <br>
        # Example <br>
        var sft1=Shift(0.000,0.000,30.000,0.000,0.000,0.000,"base") <br>
        var msg=sft1.str_array() <br>
        print msg # [0.000,0.000,30.000,0.000,0.000,0.000,"base"]
      </td>
      <td style="text-align:left">msg=sft1.str_array()
      </td>
      <td style="text-align:left">String</td>
    </tr>
    <tr>
      <td style="text-align:left">upo(crd)
      </td>
      <td style="text-align:left">
        <p>When executing the move ~ until statement, the current pose when the until condition is satisfied is returned in the crd coordinate system.</p>
        <p>For values that can be used as "crd" elements, see the table
          under "<a href="../../5-moving-robot/1-pose.md">5.1 Pose</a>".</p>
         <p>The "crd" parameter may be omitted,
          and the default value is "base" respectively.</p>
      </td>
      <td style="text-align:left">upo(&quot;joint&quot;)
      </td>
      <td style="text-align:left">Pose*</td>
    </tr>

  </tbody>
</table>

\* Pose is a data type that represents the posture of the robot or the position of the tool tip. Details will be described later in "[5.1 Pose](../../5-moving-robot/1-pose.md)".


[__SOURCE](2-basic-syntax/10-import.md)
# 2.10 import

### Description

Some features are not supported as hrspace's built-in features, but are also supported in the form of plug-in modules.

Some modules are pre-installed as default options, while others require you to install them.  
The module must be loaded into the controller with the `import` statement before it can be used in the robot language.

### Syntax

import &lt;module name&gt; [as &lt;alias&gt;]

### Parameter

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">module name</td>
      <td style="text-align:left">
        module's name
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">alias</td>
      <td style="text-align:left">
			Name to be used within the robot language program.<br>
			If specified, it can be used instead of the module name.
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

For example, in order to perform Ethernet TCP or UDP communication in the robot language, you must `import` the default option module called `enet`.

After executing the `import`, a module object named `enet` is created in the global scope. As in the example below `enet.ENet()`, you can access to a member variable or call a member function of a module object, and especially by calling a `creator` from among the member functions, you can create new object.

### Example

In the example below,  
(1) `enet` module object has been `import`ed.  
(2) The `enet.ENet()` creator function was called to create a new Ethernet socket object and assigned it into a local variable named `cli`.  
(3) Assigned a string to member variable `ip_addr` of the object `cli`.

```python
import enet # (1)
var cli=enet.ENet() # (2)
cli.ip_addr="192.168.1.172" # (3)
```

It does the same thing when you code it as below.

```python
import enet as enet_module # (1)
var cli=enet_module.ENet() # (2)
cli.ip_addr="192.168.1.172" # (3)
```

* This section only covered the rough syntax of the `import` statement. You will often see examples of the use of `import` in the later sections describing module features.
[__SOURCE](3-flowcontrol-subprogram/README.md)
# 3. Flow-Control Statements and Sub-Program

The statements in the job program are executed line by line in top-to-bottom order. However, depending on certain conditions, the statements can be skipped without being executed, or certain statements can be executed repeatedly. Let us look at the control statements that can control the flow of the program in this manner. 


[__SOURCE](3-flowcontrol-subprogram/1-address.md)
# 3.1 Address

Moving to another position in the program without executing the next line in order is called a "branch."
The address is the destination of the branch.

There are three ways to define addresses:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Format</th>
      <th style="text-align:left">Example</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">line-number</td>
      <td style="text-align:left">
        An integer between 1~9999. It can be attached to the left of a statement, not a step.
      </td>
      <td style="text-align:left">99</td>
    </tr>
    <tr>
      <td style="text-align:left">label</td>
      <td style="text-align:left">
        A label is not a syntax you attach to a statement, it is a statement in itself.<br>
        It is in the form of \* followed by [identifier](2-identifier.md). However, the identifier must not be longer than 128 characters.
      </td>
      <td style="text-align:left">*timeout</td>
    </tr>
    <tr>
      <td style="text-align:left">step number</td>
      <td style="text-align:left">
        Step number is automatically attached on steps being incremented by one.<br>
        It is in the form of S followed by a number of step. You can specify S1~S999.
      </td>
      <td style="text-align:left">S15</td>
    </tr>
  </tbody>
</table>


In the example below, `10` in the second statement is the line-number, `*err_handle` is the label, and `S12` is the step number.

```python
     move P,po3,spd=80%,accu=1,tool=3 until do33
  10 z_pos = (base_height+offset)*1.05
     # robot has to wait sensor2 input
     *err_handle
S12  move P,spd=80%,accu=1,tool=3
```




[__SOURCE](3-flowcontrol-subprogram/2-stop-wait/README.md)
# 3.2 Stop or Wait Statement

This statement can stop the execution of a program or make it wait for a certain period of time or until the conditions are satisfied.


[__SOURCE](3-flowcontrol-subprogram/2-stop-wait/1-stop.md)
# 3.2.1 stop

### Description

This will stop the program. When the program is restarted, execution will continue from the next line.

### Syntax

stop

### Example 

```python
if di9
  stop
endif
```




[__SOURCE](3-flowcontrol-subprogram/2-stop-wait/2-end.md)
# 3.2.2 end

### Description

This will stop the program. Execution will restart from the beginning of the main program when in continuous playback mode or in restart mode.

### Syntax

end

### Example

```python
move p,spd=70%,accu=1,tool=0
move p,spd=70%,accu=1,tool=0
end
```




[__SOURCE](3-flowcontrol-subprogram/2-stop-wait/3-delay.md)
# 3.2.3 delay

### Description

Makes it possible to progress to the next command statement after waiting for a designated time.

### Syntax

delay &lt;time&gt;

### Parameter

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Time</td>
      <td style="text-align:left">Time to wait</td>
      <td style="text-align:left">
        <p>Arithmetic expression
          <br />
        </p>
        <p>0.1~60.0 sec
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

### Example

```python
delay 3.5
```




[__SOURCE](3-flowcontrol-subprogram/2-stop-wait/4-wait.md)
# 3.2.4 wait

### Description

Makes it possible to move to the next command statement after waiting until a designated condition becomes true.

### Syntax

wait &lt;condition&gt;\[,&lt;timeout&gt;,&lt;timeout address&gt;\]

### Parameter

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Condition</td>
      <td style="text-align:left">Conditions in which waiting is required</td>
      <td style="text-align:left">Conditional expr</td>
    </tr>
    <tr>
      <td style="text-align:left">Timeout</td>
      <td style="text-align:left">Maximum time limit during which waiting will occur when the condition
        is false (timeout)</td>
      <td style="text-align:left">
        <p>Arithmetic expression</p>
        <p>0.1~60.0 sec</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">timeout address</td>
      <td style="text-align:left">Address to which branching will be made when the timeout is exceeded.</td>
      <td
      style="text-align:left">address</td>
    </tr>
  </tbody>
</table>

### Example

```python
wait sensor_ok
wait (sensor_ok and pos_ok),10,*timeout
```


[__SOURCE](3-flowcontrol-subprogram/3-branch/README.md)
# 3.3 Branch Statement

Makes it possible to go to a different address, without conditions.


[__SOURCE](3-flowcontrol-subprogram/3-branch/1-goto.md)
# 3.3.1 goto

### Description

Makes it possible to go to a designated address.

### Syntax

goto &lt;address&gt;

### Parameter

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">address</td>
      <td style="text-align:left">
        Address to branch<br/>
        An arithmetic expression is possible in the case of a line number.
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### Example

```python
goto 99
goto addr
goto *err_hdl
```




[__SOURCE](3-flowcontrol-subprogram/3-branch/2-gosub.md)
# 3.3.2 gosub~retsub

### Description

When the gosub statement is encountered, it branches to the specified address.
When the retsub statement is encountered, it returns to the next position after the gosub statement.
Gosub can be nested into several level, and there is no limit on the number of nesting.

### Syntax
```python
gosub <address>
...
end
  
<address>
...  
retsub
```

### Parameter

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">address</td>
      <td style="text-align:left">
        <p>Address to branch</p>
        <p>An arithmetic expression is possible in the case of a line number.</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### Example

```python
var x=5
var y=6
var res
var sum=0
gosub *calc_dist1
gosub *calc_dist2
var total=sum
if near(total,18.8102)
  print "OK"
else
  print "NG"
endif
end
     
*calc_dist1
res=x*x+y*y
res=sqr(res)
gosub *calc_sum
retsub
     
*calc_dist2
res=x+y
gosub *calc_sum
retsub
     
*calc_sum
sum=sum+res
retsub
end
```

[__SOURCE](3-flowcontrol-subprogram/4-conditional/README.md)
# 3.4 Conditional Statements

These statements allow a certain operation to be or not to be executed depending on certain conditions.


[__SOURCE](3-flowcontrol-subprogram/4-conditional/1-simple-if.md)
# 3.4.1 Single-Line if

### Description

The form of a single-line if statement is as follows: If &lt;Boolean expression&gt; is true, branching to &lt;address&gt; will occur. If false, moving to the next statement will occur.

### Syntax

```python
if <bool expression> then <address>
```

### Example

Below is an example of the single-line if statement. If the condition that pressure is greater than the limit is true, branching to the label address "\*err will occur," making it possible to print a warning that the pressure is too high. If the condition is false, the next statement will be executed one after the other without branching, so "In normal operation " will be printed, ending the program.

```python
var pressure=95, limit=90
if pressure > limit then *err
print "in normal operation."
end
*err
print "warning: pressure is too high."
```


[__SOURCE](3-flowcontrol-subprogram/4-conditional/2-if-endif.md)
# 3.4.2 if-endif

### Description

If the single-line if statement is true, only the operation of branching to a specific address will occur. If executing other operations or multiple statements is necessary, the if-endif block should be used.

The form is as follows: If &lt;Boolean expression&gt; is true, the multiple number of &lt;statement&gt; between if and endif will be executed in order. If &lt;Boolean expression&gt; is false, skipping to the position after endif will occur without the &lt;statements&gt; being executed.

### Syntax

```python
if <bool expression>
	<statement>
	...
endif
```

### Example

In the following example, if the pressure is greater than the limit, the following assignment and print statements will be executed. Otherwise, branching to the end will occur without the statements being executed.

```python
var pressure=95, limit=90, exceed
if pressure > limit
	exceed = pressure - limit
	print "warning: pressure is too high."
endif
end
```

In the example program, the statements between if and endif are indented by two spaces. These statements are indented to make it easier to recognize that they are codes for the blocks nested between if and endif.


[__SOURCE](3-flowcontrol-subprogram/4-conditional/3-if-else-endif.md)
# 3.4.3 if-else-endif Statement

### Description

If the expression is false and if there are statements to be executed, the following form is used:

If the expression is true, statement A will be executed. If false, statement B will be executed.

### Syntax

```python
if <bool expression>
	<statement A>
	...
else
	<statement B>
	...
endif
```

### Example

```python
var pressure=95, limit=90, exceed
if pressure > limit
	exceed = pressure - limit
	print "warning: pressure is too high."
else
	print "in normal operation."
endif
end
```




[__SOURCE](3-flowcontrol-subprogram/4-conditional/4-if-elseif-else-endif.md)
# 3.4.4. if-elseif-else-endif

### Description

In the case of multiple conditions, the elseif statement can be used in the following form.

### Syntax

```python
if <bool expression>
	<statement A>
	...
elseif <bool expression>
	<statement B>
	...
elseif <bool expression>
	<statement C>
	...
else
	<statement N>
	...
endif
```

### Example

```python
var pressure=95, limit_h=90, limit_m=80
if pressure > limit_h
	print "warning : pressure is too high."
elseif pressure > limit_m
	print "notification: pressure is high."
else
	print "in normal operation."
endif
end
```




[__SOURCE](3-flowcontrol-subprogram/4-conditional/5-switch-case-break-end_switch.md)
# 3.4.5 switch-case-break-end\_switch

### Description

A **switch** statement evaluates a numeric expression and compares it with the resulting value of the numeric expression designated by a **case** statement. It is executed from the **case** statement of equal value until a **break** statement is encountered.

In the following example, if the resulting value of Expression X is equal to the resulting value of Expression B1 or B2, \(1\) through \(3\) will be executed, and it will move to the point of the **end\_switch** statement \(note that there is no **break** below the command statement B\). Meanwhile, if the resulting value of Expression X is equal to that of Expression C, \(2\) through \(3\) will be executed.

If the resulting value of Expression X is not equal to that of any **case** statement, it will be moved to the **default**, and \(4\) through \(5\) will be executed. Then, the **default** section may be omitted.

### Syntax

```python
switch <expression X>
case <expression A>
	<statement A>
	...
	break
case <expression B1>
case <expression B2>
	<statement B>	... (1)
case <expression C>
	<statement C>	... (2)
	...
	break		... (3)
default
	<statement N>	... (4)
	...
	break		... (5)
end_switch
```

Any expressions such as Boolean, numeric, string  constant, parameter, and numeric, are permissible.

### Example

```python
     var state="timeout"
     var res=0
     
     switch state
     case "ok"
       res=11
       break
     case "timeout"
     case "timeover"
       res=33
       break
     case "invalid"
       res=55
       break
     case "fault"
       res=77
       break
     default
       res=99
       break
     end_switch
     
  99 end
```


[__SOURCE](3-flowcontrol-subprogram/5-nested-flow-control.md)
# 3.5. Nested Flow-Control Statements

### Description

In the control statement block, another control statement block can be placed, as shown in the following example. In the following form, two nesting  levels are shown, but multiple nesting levels can be made as much as necessary.

### Syntax

```python
if <bool expression>
	if <bool expression>
		<statement A>
		...
	else
		<statement B>
		...
	endif
endif
```

### Example

```python
var pressure=95, limit=90, inject_on=true
if inject_on
	if pressure > limit
		print "warning: pressure is high."
	else
		print "in normal operation."
	endif
endif
end
```




[__SOURCE](3-flowcontrol-subprogram/6-loop/README.md)
# 3.6 Loop Statements

Loop statements can be used when the same operation needs to be repeated multiple times.


[__SOURCE](3-flowcontrol-subprogram/6-loop/1-for-next.md)
# 3.6.1 for-next

### Description

The format of the `for`~`next` statement, which repeats the same operation, is as follows.

First, the initial value will be assigned to the index variable. When the `next` statement is encountered while the statements under the for statement are executed, the index variable will add increment/decrement values and perform repetition from the point of the for statement. When the index variable passes the end value, the repetition will end.

If a step is not specified, 1 will be applied.

### Syntax

```python
for <index variable>=<initial value> to <end value> [step <increment/decrement value>]
	<statement>
	...
next
```

### Example

The following shows an example of a routine that accumulates 1 to 10 in the sum using the for-next statement. When the repetition is over, 11 and 55 will be printed on the screen.

```python
var idx
var sum=0
for idx=1 to 10
	sum=sum+idx
next
print idx, sum
end
```

[__SOURCE](3-flowcontrol-subprogram/6-loop/2-break-continue.md)
# 3.6.2 break, continue

### Description

The `break` and `continue` are used between `for`~`next` statements explained in this previous section.

- When run into `break` in the `for`~`next` block, the loop stops its repetition and branch to the `next` statement.
- When run into `continue` in the `for`~`next` block, it doesn't proceed to the next statement, but does an increment/decrement of the index variable, and branch to the `for` statement.

### Syntax

```python
for <index variable>=<initial value> to <end value> [step <increment/decrement value>]
	<statement>
	...
	break
	<statement>
	...
next
```

```python
for <index variable>=<initial value> to <end value> [step <increment/decrement value>]
	<statement>
	...
	continue
	<statement>
	...
next
```

### Example

This is an example of outputting all the names in the array using the `for`~`next` statement, except for names with more than 5 characters, but stopping when an empty string is encountered.

```python
var i
var names=["Anna", "James", "George", "Brenda", "Tom", "", "Kate"]
var n_name = len(names)
for i=0 to n_name-1
   var name=names[i]
	if name==""
	   break
	endif
   if len(name)>5
	   continue
	endif
	print name
next
end
```

Result

```python
Anna
James
Tom
```

[__SOURCE](3-flowcontrol-subprogram/7-call-jump/README.md)
# 3.7 Call, Jump Statement and Subprograms

If an entire large-scale robot operation is created as one job program, the program becomes large and complex, making it difficult to add functions or find and solve problems.

For the program"s maintainability, it is preferable to divide the unit operations that make up the entire program into subprograms. For example, when routines, such as a routine performs communication with a sensor, a routine that calculates the target position of the tool tip with the received data, and a routine that generates an appropriate message when an error occurs, are turned into individual subprograms and allow the main program to call them, it will be easier to grasp the overall structure of the program. It will also be useful to reuse divided subprograms in other projects.






[__SOURCE](3-flowcontrol-subprogram/7-call-jump/1-call.md)
# 3.7.1 call

### Description

There is no significant difference in format between the main program and the subprogram in HRScript. The first job executed by the start button or by a signal is the main program, and all other jobs called by the **call** statement are subprograms. 

### Syntax

```python
call <job number, file name, or user function name> [,parameter 1,parameter 2,...]
```

Specify the job number of the job file name \(excluding the extension\) after the **call** statement. Then, while program A is being executed, if call B is encountered, A's execution will be stopped, and the first statement of program B, a subprogram, will continue to be executed. If the **end** or **return** statement is encountered while B is being executed, program A's execution will continue upon returning to the position of the next statement of program A's **call** statement that was previously called.

### Example

The following shows an example and the result of a subprogram called by a **call** statement. It seems meaningless to divide the program into two because the subprogram must handle only one print statement. However, a more practical example will be shown later.

* Refer to [3.7.3 def](./3-def.md) for an example of calling user function.

```python
# 0001_main.job
print "main job start"
call 102_err
print "main job end"
end
```

```python
# 0102_err.job
print "sub-program"
end
```

<br>

RESULT
```python
main job start
sub-program
main job end
```

[__SOURCE](3-flowcontrol-subprogram/7-call-jump/2-param-return.md)
# 3.7.2 Parameters and param, return

In a job program, formal parameters are used as channels through which input and output are passed. The **param** statement will define formal parameters at the beginning of the job program.

In the following example, job no. 105 is named as "dist2d" as it is a subjob that acquires the Euclidean distance from the origin to the coordinate value \(x, y\) and returns it to len.

```python
# 0001_main.job
var x,y
x=5
y=12.8
call 105_dist2d,x,y
var res=result()
print res
end
```

```python
# 0105_dist2d.job
# Calc. Euclide distance 2D
param dx,dy
var tmp

tmp=x*x+y*y
var len=sqr(tmp) # distance from origin
return len
```

<br>

RESULT
```python
13.742
```

In job no. 1, the dist2d subprogram is called with the **call** statement, and "x, y," which are local variables, are passed. In the dist2d subprogram, "dx", and "dy" defined with the **param** statement are called "formal parameters", and "x, y" passed to the **call** statement are called "actual parameters."

The dist2d program transports resulting values to external destinations through **return** statements. Returned values can be obtained by calling a result\(\) function in the called program.

(A **return** statement and an **end** statement have the same action as they end a called program and return to the main program. However, a **return** statement is different from **end** statement as the former can designate a resulting value as an element).

[__SOURCE](3-flowcontrol-subprogram/7-call-jump/3-def.md)
# 3.7.3 def (defining user function)

since V60.05-06

### Description

You can define user functions in the job with **def** statement and call it with **call** statement. Similar to **param** statement, **def** statement can specify a list of formal parameters. The actual parameter values of the **call** statement are passed to the formal parameters.
The execution of a function defined by **def** statement returns to the next statement after the **call** statement when executing **return** statement or **end** statement

User functions are called by name rather than number, so its readability is better than sub-program. And you can group multiple related functions into one subprogram to make your project structure better.


### Syntax

```python
def <user function name> [,parameter1[=default value],parameter2[=default value],...]
```

Specify the user function name after **def**. Function names must follow the rules defined in the section [2.2 Identifier](../../2-basic-syntax/2-identifier.md). In addition, it should be globally unique name. Be careful not to duplicate the new name with other function names or other variable names.
After that, specify the formal parameters. You can also specify a default value for each parameter. If you omit a actual parameter in the call statement, the formal parameter is initialized to the default value. If you start specifying a default value for a particular formal parameter, you must specify all paramters until last parameter.


```python
# examples of formal parameters default value
def set_work,mass,cx=0,cy=0,cz=0 # legal example
def set_work,mass,cx=0,cy,cz     # illegal example
```

### Example

Below are examples of user function calls with **call** statements and the results. We've presented the Euclidean distance example in the previous section to describe the subprogram. Now let's define user functions for Euclidean distance and Manhattan distance respectively and call them.


```python
# 0001_main.job
var x,y
x=5
y=12.8

call euclid_dist,x,y
var res=result()
print "euclid=",res # 13.7419

call manhattan_dist,x,y
var res=result()
print "manhattan=",res # 17.8
end
```

```python
# 0008_dist.job

# Calc. Euclide distance 2D
def euclid_dist,x,y
var tmp
tmp=x*x+y*y
var len=sqr(tmp) # distance from origin
return len

# Calc. Manhattan distance 2D
def manhattan_dist,x,y
var len=x+y
return len
```

<br>

RESULT
```python
euclid= 13.7419
manhattan= 17.8
end
```



[__SOURCE](3-flowcontrol-subprogram/7-call-jump/4-jump.md)
# 3.7.3 jump

### Description

This format is completely identical to that of call statements, and its action is also similar to that of **call** statements.

The only difference is that, while a **call** statement returns to the main program using an end program, a **jump** statement does not.

### Syntax

```python
jump <job number or file name> [,parameter 1,parameter 2,???]
```



### Example

If the jump statement of this example program is replaced with a **call** statement, the result of the replaced program will be as follows. When the **end** of the sub-program \(0102\_err\) is encountered, the action cycle will end. If the next action cycle is executed, the main program \(0001\) will be executed from the start.


```python
# 0001_main.job
print "main job start"
jump 102_err
print "main job end"
end
```

```python
# 0102_err.job
print "sub-program"
end
```


<br>

RESULT
```python
main job start
sub-program
```

[__SOURCE](3-flowcontrol-subprogram/8-local-global-var/README.md)
# 3.8 Local Variables and Global Variables

## 


[__SOURCE](3-flowcontrol-subprogram/8-local-global-var/1-local-var.md)
# 3.8.1 Local Variables

### Description

Examples have been described only using the examples of local variables defined with the var statement. Local variables are created by a var statement in one job program and are automatically destroyed when the program ends after the encounter with the end statement. Moreover, their values cannot be read or written by other programs. 

### Example

"main\_v" is a local variable accessible only within 0001.job, and "sub\_v" is a local variable accessible only within 0107.job.   Attempting to access it from another program will cause an error. 

The local variable "x" is defined in both 0001.job and 0107.job. The local variable "x" respectively defined in both programs has the same name but are different. So the value 5 for the variable "x" is set in subprogram 0107, 3 will be printed instead of 5 after the return to main program 0001.



<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var main_v=10
          <br />
        </p>
        <p>var x=3
          <br />
        </p>
        <p>call 107
          <br />
        </p>
        <p>print main_v # ok
          <br />
        </p>
        <p>print sub_v # error
          <br />
        </p>
        <p>print x # 3 is printed
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0107.job</td>
      <td style="text-align:left">
        <p>var sub_v=20
          <br />
        </p>
        <p>var x
          <br />
        </p>
        <p>print sub_v # ok
          <br />
        </p>
        <p>print main_v # error
          <br />
        </p>
        <p>x=5
          <br />
        </p>
        <p>end</p>
      </td>
    </tr>
  </tbody>
</table>


[__SOURCE](3-flowcontrol-subprogram/8-local-global-var/2-global-var.md)
# 3.8.2 Global Variables

### Description

On the other hand, global variables defined as global can always be accessed from all job programs. If a global variable is once defined, it will not be cleared even when the program cycle is reset by an end statement or an R0 \[Enter\] operation of the main program.

### Example

If a global x is executed first, a variable x will be created, and the value will be initialized to the default value of 0. Then, it will increase to 1 in the next row. If the global x is executed again in the next program cycle, it will not be defined again, and the value of 1 will be retained because the x has been defined. On the other hand, global y=10 will carry out defining and assignment so that the value of variable y will be reset to 10 when it is executed in the next program cycle.



<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>global x
          <br />
        </p>
        <p> in the case x=2
          <br />
        </p>        
        <p>x=x+1 # 3
          <br />
        </p>
        <p>call 107
          <br />
        </p>
        <p>print x, y # 4, 10
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0107.job</td>
      <td style="text-align:left">
        <p>global y=10
          <br />
        </p>
        <p>print x, y # 3, 10
          <br />
        </p>
        <p>x=x+1 # 4
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

Therefore, if a global variable is to be utilized as a counter for the number of program cycles, no value should be assigned along with a definition.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>Wrong
          <br />
        </p>
        <p>Teaching
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>global count=0
          <br />
        </p>
        <p>count=count+1
          <br />
        </p>
        <p>&#x2026;
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Correct
          <br />
        </p>
        <p>Teaching
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>global count
          <br />
        </p>
        <p>count=count+1
          <br />
        </p>
        <p>&#x2026;
          <br />
        </p>
        <p>end</p>
      </td>
    </tr>
  </tbody>
</table>


[__SOURCE](3-flowcontrol-subprogram/8-local-global-var/3-precedence.md)
# 3.8.3 Precedence

When there are local variables and global variables with an identical name, the local variable will be accessed preferentially. For example, while 0005.job is executed, as shown below, the global variable x and the local variable x will exist concurrently. At this time, if you read the x value, the local variable will also be read. After 0005.job returns to 0001.job, if you read the x value, the global variable will be read because only the global variable is present.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>global x=100
          <br />
        </p>
        <p>call 5
          <br />
        </p>
        <p>print x # 100
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0005.job</td>
      <td style="text-align:left">
        <p>var x=&quot;hello&quot;
          <br />
        </p>
        <p>print x # hello
          <br />
        </p>
        <p>end</p>
      </td>
    </tr>
  </tbody>
</table>


[__SOURCE](4-array-object/README.md)
# 4. Arrays and Objects


[__SOURCE](4-array-object/1-array/README.md)
# 4.1 Arrays






[__SOURCE](4-array-object/1-array/1-1d-array.md)
# 4.1.1 Arrays

An array is a variable type that collects and stores several values under a single name and allows access through an index number.

Arrays are defined as **var** or **global**, like any other variable.

{% hint style="warning" %}
[The names of top-level arrays in global variables are exceptionally case-insensitive, so please be aware.](../../2-basic-syntax/2-identifier.md)
{% endhint %}


Array definitions and access formats are as follows.

|  |  |
| :--- | :--- |
| Definition | var array name = \[ Value, Value, ...\] |
| Access | Array name \[Index\] |

The values that make up an array are called `elements.` Distances, an array shown in the following example, has a total of five elements. The index starts from 0. Element 0 and element 1 of `distances` are 10 and 10.5, respectively.



The \[ \] operator is used as follows to read or write the value of an array"s specific element value. The following shows an example of an object that is defined and accessed.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var distances = [ 10, 10.5, 12.7, 11.92, 9.5 ]</p>
        <p>distances[1]=20.5</p>
        <p>print distances[0], distances[1]</p>
        <p>end</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Result</td>
      <td style="text-align:left">
        <p>10</p>
        <p>20.5</p>
      </td>
    </tr>
  </tbody>
</table>



The number of elements in an array can be acquired by using the len\(\) function. Previously, the len\(\) function was introduced as a function to acquire the length of a string. If an array is put as a parameter of len\( \), it will return the number of elements in the array.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Function name</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Example of usage</th>
      <th style="text-align:left">Result</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">len(<b>a</b>)</td>
      <td style="text-align:left">Returns the length of the string if <b>a</b> is a string. Returns the number
        of elements in the array if <b>a</b> is an array</td>
      <td style="text-align:left">
        <p>len(&quot;HELLO&quot;)</p>
        <p>len([20, 30, 80])</p>
      </td>
      <td style="text-align:left">
        <p>5</p>
        <p>3</p>
      </td>
    </tr>
  </tbody>
</table>



The **for-next** statement is mainly used to perform some processing on all elements of an array.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var i</p>
        <p>var distances = [ 10, 10.5, 12.7, 11.92, 9.5]</p>
        <p>for i=0 to len(distances)-1</p>
        <p>distances[i] = distances[i]+10</p>
        <p>print distances[i]</p>
        <p>next</p>
        <p>end</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Result</td>
      <td style="text-align:left">
        <p>20</p>
        <p>20.5</p>
        <p>22.7</p>
        <p>21.92</p>
        <p>19.5</p>
      </td>
    </tr>
  </tbody>
</table>



It does not matter if the values stored in the array are of different types.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var i</p>
        <p>var arr = [ 10, &quot;abc&quot;, true]</p>
        <p>for i=0 to 2</p>
        <p>print arr[i]</p>
        <p>next</p>
        <p>end</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Result</td>
      <td style="text-align:left">
        <p>10</p>
        <p>abc</p>
        <p>true</p>
      </td>
    </tr>
  </tbody>
</table>








[__SOURCE](4-array-object/1-array/2-md-array.md)
# 4.1.2 Multidimensional Arrays

An array can also be nested as an element of an array. When accessing the elements of a multidimensional array, you can use the \[ \] operator consecutively. In the following example, "arr\_y" is a two-dimensional array. \(1\)

arr\_y\[1\] is an array of elements of index 1, namely \["abc", "jqk", "xyz"\], and it is assigned to the new variable "arr\_x." \(2\)

So, arr\_x\[1\] is "jqk", and arr\_y\[1\]\[2\] is "xyz" because it points to \[2\] of arr\_y\[1\].



<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var arr_y = [ [10,20], [&quot;abc&quot;,&quot;jqk&quot;, &quot;xyz&quot;]
          ] # (1)
          <br />
        </p>
        <p>var arr_x=arr_y[1] # (2)
          <br />
        </p>
        <p>print arr_x[1]
          <br />
        </p>
        <p>print arr_y[1][2]
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Result</td>
      <td style="text-align:left">
        <p>jqk
          <br />
        </p>
        <p>xyz
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>


[__SOURCE](4-array-object/1-array/3-array-creator.md)
# 4.1.3 Array Constructor Function - Array()

It is difficult to create an array with hundreds of elements with the notation \[ \] alone. Any number of arrays may be created by calling the constructor function. Each element will be initialized to 0.

```python
var name = Array(900)	# creates an array of 900 elements
```

If two or more elements are designated, a multidimensional array can be created. In the following example of a 3-dimensional array, \[4\] is the lowest dimension.

```python
var name = Array(3,2,4)	# [3][2][4] numbers of 3-dimensional arrays are created
# [ [[0,0,0,0], [0,0,0,0]], [[0,0,0,0], [0,0,0,0]], [[0,0,0,0], [0,0,0,0]] ]
```




[__SOURCE](4-array-object/1-array/4-array-append.md)
# 4.1.4 Append Procedure for Adding an Element to an Array

Supported from V60.32-00

The append procedure can be used to add an element to an array

```python
var arr = [1, 2]
append_arr arr, 3   # Adding 3 as an element of arr
print arr       # [1, 2, 3]
```

Any value, including another array, can be appended as an element because an array can contain elements of different types.

```python
var arr = [1, 2]
append_arr arr, [3, 4]  # Appending [3, 4] as an element of arr
print arr           # [1, 2, [3, 4]]
```

[__SOURCE](4-array-object/1-array/5-array-extend.md)
# 4.1.5 Extend Procedure for Adding All Elements of One Array to Another

Supported from V60.32-00

The extend procedure can be used to add all elements of an array to another.

```python
var arr = [1, 2]
var brr = [3, 4]
extend_arr arr, brr
print arr   # [1, 2, 3, 4]
```

It can be used like below.

```python
var arr = [1, 2]
extend_arr arr, [3, 4, 5]
print arr   # [1, 2, 3, 4, 5]
```

[__SOURCE](4-array-object/2-object.md)
# 4.2 Object

As previously seen, it was found that an array could store multiple element values and are accessed by index. 

Objects are like arrays in that they store multiple element values. The difference is that an object is accessed by a key, not with an index. Moreover, the key is a string, not a number. 

Objects are defined as var or global, like any other variables. The definition of an object and format of its access are as follows.

|  |  |
| :--- | :--- |
| Definition | var object name = { key : value, key : value, ...} |
| Access | Object name key |



The following shows an example of defining and accessing an object.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var gap = { x:200, y:152.6 }</p>
        <p>gap.x = gap.x + 10</p>
        <p>print gap.x, gap.y</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Result</td>
      <td style="text-align:left">210 152.6</td>
    </tr>
  </tbody>
</table>



The object"s key must be in the format of an identifier, but the element"s value can be of any type and can also be of different types. 

An object can contain other objects or arrays as its elements. Likewise, an array can also contain other arrays or objects as its elements. In the following example, "work," which is an object, contains "size," which is an object, and "heights," which is an array.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var work = { part_no:3, name: &quot;gear&quot;, tested : false</p>
        <p>, size : { x : 150, y : 80 }</p>
        <p>, heights : [ 72.89, 74.91, 81.03, 87.60, 87.11 ] }</p>
        <p>print work.tested, work.size.y, work.heights[3]</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Result</td>
      <td style="text-align:left">false, 80, 87.600000</td>
    </tr>
  </tbody>
</table>




[__SOURCE](4-array-object/3-array-object-assignment.md)
# 4.3 Copied assignment of arrays and objects

If the right side of an assignment statement has object variables, the entire values of the variables will be copied to the variables of the left side. When an array or an object includes sub-arrays and sub-objects in a complex manner as element values, such inclusion structures will be copied, which is called a deep copy.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var my_obj = { x:5, y:0, z:0 }
          <br />
        </p>
        <p>my_obj.y=[ [10, 20], [&quot;abc&quot;, true] ]
          <br />
        </p>
        <p>my_obj.z={ a:7, b:8 }
          <br />
        </p>
        <p>var your_obj=my_obj # deep copy
          <br />
        </p>
        <p>print your_obj.y[0]
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Result</td>
      <td style="text-align:left">[10, 20]</td>
    </tr>
  </tbody>
</table>

![](../_assets/image.png)




[__SOURCE](4-array-object/4-call-by-reference-call-by-value.md)
# 4.4 Call-by-reference and call-by-value

In the description of call statements and jump statements given in Section 3.4, the concepts of formal parameters and actual parameters were explained. When an actual parameter has been transported to a sub-program, if the sub-program ends after changing the value of the parameter, will it be reflected to the main program?

For example, let"s assume that a sub-program 0005\_pow3.job raises a value to the third power as follows:



<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var x=2
          <br />
        </p>
        <p>call 0005_pow3,x
          <br />
        </p>
        <p>print x
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0005_pow3.job</td>
      <td style="text-align:left">
        <p>param p
          <br />
        </p>
        <p>var t=p
          <br />
        </p>
        <p>p=t*t*t # (1)
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Result</td>
      <td style="text-align:left">2</td>
    </tr>
  </tbody>
</table>

Although we expected that 8 is output because 2x2x2 is 8, the result is 2. It is because, when a numeric-type actual parameter is transported to a sub-program, the value is copied as a parameter. In other words, in \(1\), because the value raised to the third power was assigned to the copied version, it did not affect the value of the original parameter, x.

Therefore, the teaching program should be corrected so that the resulting value is transported by a return statement.



<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var x=2
          <br />
        </p>
        <p>call 0005_pow3,x
          <br />
        </p>
        <p>x=result()
          <br />
        </p>
        <p>print x
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0005_pow3.job</td>
      <td style="text-align:left">
        <p>param p
          <br />
        </p>
        <p>var t=p
          <br />
        </p>
        <p>p=t*t*t
          <br />
        </p>
        <p>return p
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Result</td>
      <td style="text-align:left">8</td>
    </tr>
  </tbody>
</table>

On the other hand, in the case of arrays or objects, the reference of actual parameters, not the copied versions, will be transported. A reference refers to the position of a parameter.

In the following example, where the sub-program 0006\_pow3.job raises each element of an array to the third power, the values of the elements of the actual parameter array are changed.



<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var x=[3, 2, 4]
          <br />
        </p>
        <p>call 0006_pow3,x
          <br />
        </p>
        <p>print x
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0006_pow3.job</td>
      <td style="text-align:left">
        <p>param p
          <br />
        </p>
        <p>var t
          <br />
        </p>
        <p>for i=0 to len(arr)-1
          <br />
        </p>
        <p>t=p[i]
          <br />
        </p>
        <p>p[i] = t*t*t
          <br />
        </p>
        <p>next
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Result</td>
      <td style="text-align:left">[27, 8, 64]</td>
    </tr>
  </tbody>
</table>

When a sub-program is called, if the copied version of the value of an actual parameter is transported, it is referred to as call-by-value; and if a reference is transported, it is referred to as call-by-reference. Whether it will be call-by-value or call-by-reference is determined by the type of values as follows:

|  |  |
| :--- | :--- |
| call-by-value | Boolean, numeric, and string types |
| call-by-reference | Array and object types |

![](../_assets/image_3.png)




[__SOURCE](5-moving-robot/README.md)
# 5. Moving a Robotwith Robot Language

After understanding the pose that expresses the target position of the robot, let us learn about the commands to move the robot.


[__SOURCE](5-moving-robot/1-pose.md)
# 5.1 Pose

Pose is an object type embedded in the ${cont_model} Controller and represents each axis of the robot or the Cartesian coordinates and direction of the tool tip. 

Poses are created by calling the constructor function `Pose()`. All function parameters are position parameters. The first string element is recognized as the `format`, and the second string element as the `config`. The remaining elements are all numeric type.

### format
Multiple sub-elements including the coordinate system are listed, separated by semicolons (;). Each sub-element is optional and can appear in any order.

<table>
  <tr>
    <th>Sub-element name</th>
    <th>Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>crd</td>
    <td>string</td>
    <td>coordinate system.<br>If omitted, joint coordinate system is used.<br>
See table below.</td>
  </tr>
  <tr>
    <td>sync(p1,p2)</td>
    <td>p1, p2 : real</td>
    <td>sensor sync (1 or 2 position values)</td>
  </tr>
  <tr>
    <td>mi(mech#[, ...])</td>
    <td>Each mech number : integer 0~7</td>
    <td>Mechanism configuration.<br>(mi stands for mech.info.)<br>If omitted, all mechanisms are included.</td>
  </tr>
</table>

Examples of format;
```python
"base,mi(0,2)" # Base coord., mech. 0 and 2 included
"" # Coord. omitted (joint), no sensor sync, mechinfo omitted (all mech.)
"sync(20.5,-12.0),robot" # Sensor sync (pos.1=20.5, pos.2=-12.0), robot coord.
```

{% hint style="info" %}
The cfg element specifies the robot configuration. For more information, refer to "[2.3.2.2 Base and Robot Recording Coordinates](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-${cont_model}-tp630/2-operation/3-step/2-step-pose-modify/2-base-robot-crd-sys)" in the ${cont_model} Robot Controller Operation Manual.
{% endhint %}



```python
var <pose variable name> = Pose(j1, j2, j3, ...)		# axis coordinate
var <pose variable name> = Pose(x, y, z, rx, ry, rz, j7, j8,..., crd, cfg)		# base coord.
```

Refer to the following examples of creating the poses for 6 axes + 1 additional axis and for Cartesian + 1 additional axis.

```python
var po1 = Pose(10, 90, 0, 0, -30, 0, -1240.8)				# axis coordinate
var po2 = Pose(1850, 0, 2010.5, 0, -90, 0, -1240.8, "base", "fl;r2")	# base coord.
var po3 = Pose(-1140.8, "mi(2)")	# joint coord., mech. 2
```

Alternatively, the pose constructor function may be called using a single array or string parameter. With this, files or data may be converted into poses, acquired through remote communication, and used.

```python
var <pose variable name> = Pose(array)
var <pose variable name> = Pose(string)
```

Refer to the following example.

```python
var arr = [10, 90, 0, 0, -30, 0, -1240.8]
var str = "[1850, 0, 2010.5, 0, -90, 0, -1240.8, \"base\", \"fl;r2\"]"
var po3 = Pose(arr)
var po4 = Pose(str)
```

Elements of the pose object can be accessed with the following keys.



<!--![](../_assets/image_5.png)-->

<table>
  <tr>
    <th>Key</th>
    <th>Type</th>
    <th>Value range</th>
    <th>Description</th>
    <th>Unit, Remarks</th>
  </tr>
    <tr>
    <td>nj</td>
    <td>Integer</td>
    <td>1~32</td>
    <td>Axis count</td>
    <td> </td>
  </tr>
   </tr>
    <tr>
    <td>j1~j32</td>
    <td>Real</td>
    <td>8-byte real mumber</td>
    <td>Axis value</td>
    <td>mm, deg</td>
  </tr>
   </tr>
    <tr>
    <td>x, y, z</td>
    <td>Real</td>
    <td>8-byte real mumber</td>
    <td>Tool position in Cartesian coordinate</td>
    <td>mm</td>
  </tr>
   </tr>
    <tr>
    <td>rx, ry, rz</td>
    <td>Real</td>
    <td>8-byte real mumber</td>
    <td>Euler angle of tool orientation</td>
    <td>deg</td>
  </tr>
  <tr>
    <td rowspan="4">crd</td>
    <td rowspan="4">String</td>
    <td>joint</td>
    <td>Joint coordinate (default)</td>
    <td rowspan="4"></td>
  </tr>
  <tr>
    <td>base</td>
    <td>Base coordinate</td>
  </tr>
  <tr>
    <td>robot</td>
    <td>Robot coordinate</td>
  </tr>
  <tr>
    <td>u1 ~ u10</td>
    <td>User coordinate</td>
  </tr>
  <tr>
    <td rowspan="8">cfg</td>
    <td rowspan="8">String</td>
    <td>s</td>
    <td>|S|>=180</td>
    <td rowspan="7">Possible to perform<br>combination by <br>dividing with ";"<br><br>The default is all flags turned off.</td>
  </tr>
  <tr>
    <td>r1</td>
    <td>|R1|>=180</td>
  </tr>
  <tr>
    <td>r2</td>
    <td>|R2|>=180</td>
  </tr>
  <tr>
    <td>b</td>
    <td>|B|>=180</td>
  </tr>
  <tr>
    <td>re</td>
    <td>rear</td>
  </tr>
  <tr>
    <td>dn</td>
    <td>down</td>
  </tr>
  <tr>
    <td>nf</td>
    <td>non-flip</td>
  </tr>
  <tr>
    <td>auto</td>
    <td>auto (automatic desision)</td>
    <td></td>
  </tr>
  <tr>
    <td>mechinfo</td>
    <td>Integer</td>
    <td>-1 ~ 255</td>
    <td>bitfield<br>(bit0:M0, bit1:M1, .... bit7:M7)<br>-1 is all mech.</td>
    <td>Only the bits corresponding to the included mechanisms are set to 1.</td>
  </tr>
  <tr>
    <td>nsync</td>
    <td>Integer</td>
    <td>0~2</td>
    <td>The number of sensor-sync</td>
    <td></td>
  </tr>
  <tr>
    <td>sync</td>
    <td>String (p1, p2; integer)</td>
    <td>sync(p1,p2)</td>
    <td>Sensor-sync values</td>
    <td>sync(220.5,195.3)</td>
  </tr>
</table>


1. For V60.06-06 or older versions, fl is non-fl.

The pose element values can be accessed as shown in the following example.

```python
po1.j2 = po1.j2 + 5
print po2.z, po2.cfg
```




[__SOURCE](5-moving-robot/2-shift.md)
# 5.2 Shift

Shift is an object type embedded in the ${cont_model} Controller and represents the pose's change value. 

Shifts are created by calling the constructor function Shift\( \). All function parameters are position parameters. Meanwhile, crd and cfg are string types, and the rest are number types.



```python
var <shift variable name> = Shift(j1, j2, j3, ...)				# axis coordinate
var <shift variable name> = Shift(x, y, z, rx, ry, rz, j7, j8,..., crd)		# base coordinate
```

Refer to the following examples of creating the shifts for 6 axes + 1 additional axis and for Cartesian + 1 additional axis.

```python
var sft1 = Shift(30, 0, 0, 0, -5.8, 0, -120)				# axis coordinate
var sft2 = Shift(0, 0, 55.2, 0, -5, 0, -120, "base")			# base coordinate
```

Alternatively, the constructor function shift may be called using a single array or string parameter. With this, files or data may be converted into shifts, acquired through remote communication, and used.

```python
var <shift variable name> = Shift(array)
var <shift variable name> = Shift(string)
```

Refer to the following example.

```python
var arr = [30, 0, 0, 0, -5.8, 0, -120]
var str = "[0, 0, 55.2, 0, -5, 0, -120, \"base\"]"
var sft3 = Shift(arr)
var sft4 = Shift(str)
```

Elements of the shift object can be accessed with the following keys.

![](../_assets/image_7.png)


[__SOURCE](5-moving-robot/3-pose-expression.md)
# 5.3 Pose Expression

The expression in which the result value becomes a pose is called a "pose expression." 

All the following forms are recognized as poses.

```python
Pose
Pose+Shift
Pose-Shift
Pose+Shift+Shift+...
```



Refer to the following example of assigning the result of a pose expression to another pose variable.

```python
var po1 = Pose(10, 90, 0, 0, -30, 0)
var po2 = Pose(1850, 0, 2010.5, 0, -90, 0, "base", "fl;r2")
var po3 = cpo("robot")
var sft1 = Shift(30, 0, 0, 0, -5.8, 0)
var po4 = po1-sft1
var po5 = po2+sft1+Shift(0, 0, 55.2, 0, -5, 0, "base")
```


[__SOURCE](5-moving-robot/4-move.md)
# 5.4 move

The move statement is a procedure for moving the robot. The format is as follows.

### Description

The robot"s tool tip moves to the pose position.

### Syntax

move &lt;interpolation&gt;, \[tg=&lt;pose/shift&gt;\], spd=&lt;speed&gt;, accu=&lt;accuracy&gt;

, tool=&lt;tool number&gt; \[x=&lt;assignment statement&gt;,\] \[until &lt;conditional expression&gt;\]

### Parameter

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Interpolation</td>
      <td style="text-align:left">
        <p>P: Axis interpolation;</p>
        <p>L: Linear interpolation;</p>
        <p>C: Circular interpolation,</p>
        <p>SP: Stationary axis interpolation,</p>
        <p>SL: Stationary tool linear interpolation,</p>
        <p>SC: Stationary tool circular interpolation</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Pose/Shift</td>
      <td style="text-align:left">
        <p>Target posture (pose) to move to</p>
        <p>It will be omitted if there is a hidden pose.</p>
        <p>If a shift expression is specified with a + or - sign, (hidden pose +
          shift expression) will be applied as the target posture.</p>
      </td>
      <td style="text-align:left">Pose expression or a signed shift expression</td>
    </tr>
    <tr>
      <td style="text-align:left">Speed</td>
      <td style="text-align:left">
        <p>Moving speed of the tool tip</p>
        <p>A unit (mm/sec, cm/min, sec, %) should be added.</p>
      </td>
      <td style="text-align:left">Arithmetic expression</td>
    </tr>
    <tr>
      <td style="text-align:left">Accuracy</td>
      <td style="text-align:left">
        <p>Arithmetic expression</p>
        <p>The lower the value, the more accurate. If it is 0, the operation will
          occur discontinuously.</p>
      </td>
      <td style="text-align:left">0~7</td>
    </tr>
    <tr>
      <td style="text-align:left">Tool number</td>
      <td style="text-align:left">The number of the tool to be used when the robot is operating</td>
      <td
      style="text-align:left">0~31</td>
    </tr>
      <tr>
      <td style="text-align:left">Assignment statement</td>
      <td style="text-align:left">
        <p>When move starts, the assignment statements to be executed are carried out sequentially from left to right.</p>
      </td>
      <td style="text-align:left">True if not 0 False if 0
      <p>"&lt;assignment statement1;assignment statement2;...&gt;"<\p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Conditional expression</td>
      <td style="text-align:left">
        <p>As soon as the conditional expression is true, the robot operation will
          end, and the designated pose is considered to have been reached.</p>
        <p>The result of the conditional expression can be acquired with the result()
          function.</p>
      </td>
      <td style="text-align:left">True if not 0 False if 0</td>
    </tr>
  </tbody>
</table>

### Example

```python
move L,tg=po[0]+sft[1],spd=800mm/sec,accu=0,tool=1
move P,tg=+Shift(0,0,0,0,-10,0),spd=80%,accu=1,tool=3,x="do1=1;do2=2",until di2  (hidden pose)
if result() then *sensor_on
```

If the \[Record\] button of the teach pendant is pressed, a move statement in hidden pose type will be recorded as the current robot position. The hidden pose value can be checked or edited by placing the cursor on the move statement and pressing the \[Property\] button. 

When the \[Command\] button is pressed and the \[Motion\] group is opened, select the move menu. As a result, a pose-type move statement is recorded.






[__SOURCE](5-moving-robot/5-mkucs.md)
# 5.5 mkucs - make user coordinate system

### Description

A command that creates a user coordinate system with three poses or one pose.   

- When you create with three poses, it is created with the origin pose, an axis pose, plane pose  according to the specified step order.
-  If the step order is not specified, it is created with the origin pose, X-axis pose, and XY plane pose.
- When you create with one pose, it is created with the origin pose and the position/direction is based on the pose value.
- If the calculation is not possible, the job execution is interrupted with an error.


### Syntax

```python
<result variable> = mkucs(<user coord. system number>,<step order>,<origin pose>,<axis pose>,<plane pose>)
or
<result variable> = mkucs(<user coord. system number>,<origin pose>)
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">result variable</td>
      <td style="text-align:left">
        result of background execution<br>
        <ul>
        <li>0: Successfully completed.</li>
        <li>-1: Failed to create user coord. system.</li>
        </ul>
      </td>
      <td style="text-align:left">Variable</td>
    </tr>
    <tr>
      <td style="text-align:left">user coord. system number</td>
      <td style="text-align:left">
        umber of the user coordinate system to create
      </td>
      <td style="text-align:left">[1~20]</td>
    </tr>
    <tr>
      <td style="text-align:left">step order</td>
      <td style="text-align:left">
        The order of the three poses below, if not specified, will be "OXY" <br>
        (Example) <br>
        "OXY" : origin pose, X axis pose, XY plane pose <br>
        "OYZ" : origin pose, Y axis pose, YZ plane pose <br>
      </td>
      <td style="text-align:left">string variable</td>
    </tr>
    <tr>
      <td style="text-align:left">origin pose</td>
      <td style="text-align:left">
        pose at the origin
      </td>
      <td style="text-align:left">pose variale</td>
    </tr>
    <tr>
      <td style="text-align:left">axis pose</td>
      <td style="text-align:left">
        pose located on the X, Y, Z-axis
      </td>
      <td style="text-align:left">pose variale</td>
    </tr>
    <tr>
      <td style="text-align:left">plane pose</td>
      <td style="text-align:left">
        Pose located on the XY, YZ, ZX-plane
      </td>
      <td style="text-align:left">pose variale</td>
    </tr>
  </tbody>
</table>

### Return value


<table>
  <thead>
    <tr>
      <th style="text-align:left">Value</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Etc.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>
        OK
      </td>
      <td></td>
    </tr>  
  </tbody>
</table>


### Errors

- E14613 : Occurs when the actual parameter does not match the formal parameter. Check the actual parameters.
- E14614 : Occurs when the user coordinate number is not a number. Please specify the user coordinate number again.
- E14615 : Occurs when the user coordinate number is not a number between 1 and 20. Please change the user coordinate number.
- E1011 : Occurs when the distance between the taught poses is too close. Occurs when the distance between each point is less than 1mm. Please correct the distance value between poses.
- E1012 : Occurs when three called poses are in a straight line.


### Example

```python
   var p_origin=Pose(0,0,0,0,0,0,"base")
   var p_xaxis=Pose(100,0,0,0,0,0,"base")
   var p_xyplane_=Pose(100,100,0,0,0,0,"base")
   var uc1 = mkucs(1,p_origin,p_xaxis,p_xyplane)
   var uc2 = mkucs(2,p_origin)
   var uc3 = mkucs(1,"OXY",p_origin,p_xaxis,p_xyplane)
   end
```

![](../../_assets/mkucs.png)


[__SOURCE](5-moving-robot/6-selucrd.md)
# 5.6 selucrd - select user coordinate system

The selucrd statement is a procedure for changing the user coordinate system number specified as the user coordinate system in the condition setting.

### Description

Function corresponding to specifying the User coordinate system in the condition setting.

### Syntax

```python
selucrd <coord. system number>
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">coord. system number</td>
      <td style="text-align:left">
        coord. system number to select<br>
        <ul>
        <li>0: Unspecifying user coordinate system</li>
        <li>1~20: Specifying a User Coordinate system</li>
        </ul>
      </td>
      <td style="text-align:left">expression</td>
    </tr>
  </tbody>
</table>

### Example

```python
   selucrd 1
   end
```
[__SOURCE](5-moving-robot/7-contpath.md)
# 5.7 contpath

### Description

Select the mode of CONTPATH.

See the link below for the description of CONTPATH.
[Operation Manual: 8.15 R360 Set CONTPATH manually](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-${cont_model}-tp630/8-r-code/15-r360)

<br><br>


### Syntax

```python
contpath <mode number>
```

### Parameter

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">mode number</td>
      <td style="text-align:left">
        0: Discontinuous<br>
        1: Continuous. However, input signal is discontinuous (default)<br>
        2: Continuous. Input signal is also continuous
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### Example

```python
contpath 0
contpath 1
contpath 2
```


{% hint style="info" %}

- If the `contpath` statement is not explicitly executed, `contpath 1` is applied by default. Even if specified explicitly, it is initialized to `contpath 1` at the start of the cycle.

- The changed status can be checked by the `CP0` / `CP1` / `CP2` flags on the title bar.

{% endhint %}

[__SOURCE](5-moving-robot/8-coldet.md)
# 5.8 coldet 

Robot language "coldet" is used for setting collision detection(of each axis) level in case of the function activated on. 

Users should set the function activation on/off and collision level in the TP menu. \[3: robot parameter &gt; 14: impact detection &gt; 2: set the collision detection(of each axis) \] 

The menu can be shown in that robot is set for detecting collision.  

If the function is activated on, default detecting level is 1. 

Also in manual mode, the default level is same. 

--- 

### Description
* Set the collision detection level 


### Syntax 
```python
coldet LV=<level> 
```

### Parameter 
* The value of level can be set from 0 to 16 (0: off)

### Example 

```python
S1   move P,spd=60%,accu=0,tool=0
S2   move P,spd=60%,accu=0,tool=0
     coldet LV=2
S3   move P,spd=60%,accu=0,tool=0
     coldet LV=3
S4   move P,spd=60%,accu=0,tool=0
S5   move P,spd=60%,accu=0,tool=0
     coldet LV=0
S6   move P,spd=60%,accu=0,tool=0
S7   move P,spd=60%,accu=0,tool=0
     end 
```
* The value of detecting level in step1 and step2 is 1. 
* The value of detecting level in step3 is 2, and that of level in step 4 and step5 is 3.
* In case of step6 and step7, the function of collision detection is deactivated. 
--- 

[__SOURCE](5-moving-robot/9-colsense.md)
# 5.9 colsense 

Robot language "colsense" is used for setting detection sensitivity in case of the function activated on. 

Users should set the function activation on/off and detection sensitivity in the TP menu. \[3: robot parameter &gt; 14: impact detection &gt; 1: Model-based collision detection \] 

--- 

### Description
* General collision detection sensitivity can be set
* Each axis collision detection sensitivity can be set 

### Syntax 
```python
colsense general,sensitivity=<general sensitivity>  
colsense axis,id=<joint number>,criteria=<each axis sensitivity> 
```

### Parameter 
* General threshold value can be set from 0 to 200, and larger value is more sensitive.(0:0ff,1~200)
* The parameter "id" is set as joint number.(1~6)  
* Axis threshold value can be set from 0 to 100, and lower value is more sensitive.(0:0ff,1~100)"

### Example 

```python
S1   move P,spd=60%,accu=0,tool=0
S2   move P,spd=60%,accu=0,tool=0
     colsense general,sensitivity=150
S3   move P,spd=60%,accu=0,tool=0
     colsense general,sensitivity=200
S4   move P,spd=60%,accu=0,tool=0
S5   move P,spd=60%,accu=0,tool=0
     colsense axis,id=1,criteria=0
     colsense axis,id=2,criteria=0
S6   move P,spd=60%,accu=0,tool=0
S7   move P,spd=60%,accu=0,tool=0
     end 
```
* The detection sensitivity value in step1 and step2 is used from setting based on the menu \[3: robot parameter &gt; 14: impact detection &gt; 1: Model-based collision detection \] 
* The General sensitivity in step3 is 150, and the value is changed as 200 in step4 and step5 
* Sensing collision on joint1 and joint2 is deactivated, and other joints collision are detected by general sensitivity as 200.  

--- 
{% hint style="info" %}

The final sensitivity value per axis is proportional to the sensitivity value of each axis, and inversely proportional to the general sensitivity value. 
{% endhint %}



[__SOURCE](5-moving-robot/10-softxyz.md)
# 5.10 softxyz 


The softxyz function is a sensorless force-control feature that allows the robot  
to move flexibly in Cartesian space in response to external forces under user-defined conditions.

To ensure proper operation, **tool data and additional payload information must be configured correctly**.

{% hint style="warning" %}

Since the softxyz function is **sensorless** and does not use a force sensor,  
there are **inherent limitations** in achieving fully smooth and natural motion.

However, by tuning the `softxyz_lim` values appropriately for the application environment,  
you can achieve the smoothest possible motion within the functional limitations.

Because `softxyz_lim (pos / xnr / vel / thr)` directly determines how the robot responds to external force,  
**fine-tuning is required** depending on the environment, assembly process, and tool stiffness.

{% endhint %}

### Description
* A function that allows the robot to be displaced in a Cartesian coordinate system by external force without using a force sensor.

---

### Syntax
```python
softxyz on, crd=<reference_coordinate>
softxyz set, dpr=<stiffness>
softxyz off
```

### Parameters
- **on** : Start the softxyz function  
- **off** : Stop the softxyz function  
- **set** : Modify softxyz settings  

- **crd** : Reference coordinate system for external-force displacement  
  - Available options: `base`, `robot`, `tool`, `user_x`

- **dpr** : Stiffness value  
  - Range: **0.0 ~ 2.0**  
  - Higher values = **stiffer**, less displacement under external force  
  - Default: **1.0**

```python
softxyz on,  crd="base"     # Based on the base coordinate system
softxyz on,  crd="robot"    # Based on the robot coordinate system
softxyz on,  crd="tool"     # Based on the tool coordinate system
softxyz on,  crd="user_1"   # User-defined coordinate system #1

softxyz set, dpr=1.0        # Set stiffness (0.0~2.0, higher = stiffer)
softxyz off                 # Disable the softxyz function
```


### Example 
> Example 1) Assembly along the Z-direction while allowing displacement in X, Y, and Ry
> * Coordinate : robot coordinate (crd="robot") <br>
> * Position (xnr) limit : the range of X and Y direction [-50,+50](mm), the range of Ry direction [-3,+3] (deg) <br>
> * Velocity (vel) limit : the maximum speed of X and Y direction 5(mm/sec), the maximum speed of Ry 3(deg/sec)  <br>
> * Torque (thr) limit : the threshold of X direction 3N, that of Y direction 3N and that of Ry direction 1Nm 

```python
S1   move P,spd=100mm/sec,accu=0,tool=0
     delay 2.0   # Required before enabling softxyz
     softxyz_lim xnr, x=50, y=50, ry=3
     softxyz_lim vel, x=5, y=5, ry=3
     softxyz_lim thr, x=20, y=20, ry=3
     softxyz on, crd="robot"

S2   move P,spd=250mm/sec,accu=0,tool=0
     softxyz off
     end
```

> Example 2) Injection materials handling 
> * Coordinate : robot coordinate (crd="robot") <br>
> * Position (pos) limit : the range of +Y direction [0,3]  
(mm) , the range of -Y direction [-200,0] (mm) <br>
> * Velocity (vel) limit : the maximum speed of Y direction 150(mm/sec)<br>


```python
S1   move P,spd=100mm/sec,accu=0,tool=0
     delay 2.0   # Required before enabling softxyz
     softxyz_lim pos, _y=300, y_=200
     softxyz_lim vel, y=150
     softxyz on, crd="robot"

S2   wait ...
     softxyz off
     end
```

--- 
> **Information**
>
> - Before using `softxyz on`, you **must** configure the `softxyz_lim` parameters  
>   (`pos`, `xnr`, `vel`, `thr`) to set the maximum displacement, speed,  
>   and Cartesian threshold values.
>
> - To improve sensitivity to external force, it is recommended to  
>   **keep the robot stationary for 1-2 seconds using the `delay` command**  
>   before executing `softxyz on`.
>
> - If vibration occurs during softxyz operation, the following adjustments are recommended:
>   1) *Increase the `thr` value*  
>   2) *Increase the `dpr` value*  
>   3) *Decrease the `vel` value*
[__SOURCE](5-moving-robot/11-softxyz_lim.md)
# 5.11 softxyz_lim

Before using instruction "softxyz on", user should set softxyz_lim parameters such as position limit(pos), workspace limit(xnr), velocity limit(vel) and force threshold limit(thr). <br>


--- 

### Description 
* softxyz_lim parameter setting   


### Syntax 
```pythonghlt
softxyz_lim pos,_x=<+X>,x_=<-X>,_y=<+Y>,y_=<-Y>,_z=<+Z>,z_=<-Z> 
softxyz_lim vel,x=<X>,y=<Y>,z=<Z>,rx=<Rx>,ry=<Ry>,rz=<Rz>  
softxyz_lim xnr,x=<X>,y=<Y>,z=<Z>,rx=<Rx>,ry=<Ry>,rz=<Rz> 
softxyz_lim thr,x=<X>,y=<Y>,z=<Z>,rx=<Rx>,ry=<Ry>,rz=<Rz> 
```

### Parameter 
* softxyz_lim pos : Position limit based on cartesian space [mm] <br>
* softxyz_lim vel : Maximum translation and rotation velocity limit based on cartesian space [mm/sec] or [deg/sec] 
<br>
* softxyz_lim xnr : Workspace (position/rotation) limit based on cartesian space [mm] or [deg] <br>
* softxyz_lim thr : force threshold limit based on cartesian space [N] or [Nm] <br>


### Example
> * setting position limit : +X direction is 200[mm], -Y direction is 100[mm], +Z direction is 300[mm]
```python
softxyz_lim pos, _x=200, y_=100, _z=300
```
> * setting velocity limit : maximum speed of Z direction is 40[mm/sec] 
```python
softxyz_lim vel, z=40
```
> * setting workspace limit : maximum position of X direction is [-200,200][mm]
```python
softxyz_lim xnr, x=200
```
> * setting torque limit : torque threshold is set to 10[N]
```python
softxyz_lim thr, y=10
```



[__SOURCE](5-moving-robot/12-softjoint.md)
# 5.12 softjoint

softjoint instruction is sensorless force control, that allows the robot to move compliantly in joint space with respect to external forces in the environment set by the user. <br>

User should check the validity of robot tool and additional axis information for increasing function accuracy. <br>



--- 

### Description 
* Without using sensor, move compliantly in joint space with respect to external forces in the environment set by the user. 


### Syntax 
```python
softjoint on
softjoint off  
```

### Parameter
* on : function start
* off : function end 



--- 
{% hint style="info" %}

* Before using "softjoint on", user should set softjoint_lim parameters such as joint number(j), softness(sft), joint angle limit(ang) and torque threshold(thr).

* For upgrading sensorless force control performance, user should set "delay" command as "delay 1.0" befor "softjoint on".  

{% endhint %}

[__SOURCE](5-moving-robot/13-softjoint_lim.md)
# 5.13 softjoint_lim

Before using instruction "softjoint on", user should set softjoint_lim  parameters such as joint number(j), compliance(sft), joint angle limit(ang) and torque threshold(thr). <br>

--- 

### Syntax 
```python
softjoint_lim, j=<joint number>, sft=<softness>, ang=<joint angle limit>, thr=<torque threshold> 
```

### Parameter
* j : joint number [1~6]
* sft : larger value is more soft to move [0:off,0~100]
* ang : joint angle limit [deg]
* thr : torque threshold [Nm]


### Example 
> Example1) setting parameters on joint number 3(J3) 
> * Activation on J3, softness(50), joint angle limit [-30~30] (deg) and torque threshold 10(Nm)   
```python
softjoint_lim, j=3, sft=50, ang=30, thr=10
```

> Example2) setting parameters on joint number 2 and 3(J2, J3)
> * Setting softness : J2-sft(30), J3-sft(80)  
> * Setting joint angle limit : J2[-50,+50] (deg), J3[min joint angle limit, max joint angle limit] (deg) <br>
> * Setting torque threshold : J2-thr(3)(Nm), J3-thr(5)(Nm) 


```python
S1   move P,spd=100mm/sec,accu=0,tool=0
     delay 2.0 
     softjoint_lim j=2,sft=30,ang=50,thr=3
     softjoint_lim j=3,sft=80,thr=5
     softjoint on
S2   move P,spd=250mm/sec,accu=0,tool=0
     softjoint off 
     end 
```


--- 
{% hint style="info" %}

* For using the function of softjoint, parameters on "j" and "sft" on softjoint_lim should be set. Also, if you do not set "ang" parameter, robot moves in workspace on defined softlimit. And, default parameter value on torque threshold "thr" is 0 [Nm]. 

{% endhint %}

[__SOURCE](5-moving-robot/14-external_control.md)
# 5.14 External control


### Description  
* The position command generation for the robot's movement is performed by an external device, and this generated external command is transmitted to the ${cont_model} controller as string data via ethernet or serial communication. The ${cont_model} controller receives this command and controls the robot. 

### Syntax 
```python
     global onl_trj
     var msg # Pose or Pose type string

     onl_trj=online.Traject()
     onl_trj.time_from_start=-1.0
     onl_trj.look_ahead_time=1.0
     onl_trj.interval=0.1
     onl_trj.init
     onl_trj.buf_in msg
 
```

### Parameter 
* time_from_start : elapsed time from start position (-1: disable)  
* look_head_time : time delay for robot moving (unit : [s])  
* interval : time interval between generated commands (unit : [s])  
* init : online trajectory init, clear command buffer  
* buf_in  : add pose or pose type string to the command buffer



### Example
> The robot moves by receiving commands generated externally via enet communication. 

```python
     import enet
     global enet0
     enet0=enet.ENet("tcp")
     enet0.ip_addr="192.168.1.213"
     enet0.lport=7000
     enet0.rport=7000
     var ret=enet0.open()
     ret=enet0.listen()
     ret=enet0.accept()

     global onl_trj
     onl_trj=online.Traject()
     onl_trj.time_from_start=-1.0
     onl_trj.look_ahead_time=1.0 # Delay time for robot movement start
     onl_trj.interval=0.1 # Sampling time of generated commands
     onl_trj.init # Buffer init

     var msg
10   enet0.recv
     str_pose=result()
      if msg == "stop"
       onl_trj.init # buffer clear (quick stop)
     else
       onl_trj.buf_in msg 
     endif    
     goto 10
     end 
```


--- 
{% hint style="info" %}

* Currently received pose or pose type strings can only be in axis-angle coordinates.
* Pose strings can only be in array-formatted axis-angle coordinates (e.g. [0.000,90.000,0.000,0.000,-90.000,0.000]).    

{% endhint %}

[__SOURCE](5-moving-robot/15-convcrd.md)
# 5.15 convcrd


### Description 
* convcrd command is a function instruction that converts the coordinate system of the pose variable.


### Syntax 
>* poseA: The pose variable to be converted.
>* poseB: Converted pose variable.

```python
poseB = poseA.convcrd("base")      # base coordinate
poseB = poseA.convcrd("robot")     # robot coordinate
poseB = poseA.convcrd("tool")      # tool coordinate
poseB = poseA.convcrd("u1")        # user coordinate 1
```

### Example 
```python
     var pose_A, pose_B
     
     # joint coordinate
     pose_A=Pose(0.00,60.00,0.00,0.00,-30.00,0.00)
     # base coordinate
     pose_B=pose_A.convcrd("base")
```



[__SOURCE](5-moving-robot/16-pose_trans.md)
# 5.16 pose_trans 


### Description 
* pose_trans command is a function instruction that multiplies two pose variables to obtain the resulting pose value. 

### Syntax 

```python
poseC = pose_trans(poseA,poseB)
```

### Example 
```python
     var pose_A, pose_B, pose_C
     var pose_inv_B
     var pose_shift
     
     pose_shift=Shift(10.0, 10.0, 10.0, 0.000, 0.000, 0.000, "base")

     # pose_A : (0,60,0,0,-30,0) 
     pose_A=Pose(0.00,60.00,0.00,0.00,-30.00,0.00)
     pose_A=pose_A.convcrd("base")
 
     pose_B=pose_A+pose_shift
     
     # pose_inv_B is inverse matrix oof pose_B
     pose_inv_B=pose_B
     pose_inv_B=pose_B.convcrd("base")
     pose_inv_B=pose_inv(pose_B)

     # pose_C is same to pose_A
     pose_C=pose_trans(pose_A,pose_B)
     pose_C=pose_trans(pose_C,pose_inv_B)
          
S1   move P,tg=pose_C,spd=10%,accu=0,tool=0
     
     end
```


[__SOURCE](5-moving-robot/17-pose_inv.md)
# 5.17 pose_inv 


### Description
* pose_inv instruction is a function that converts to a pose variable corresponding to the inverse matrix of the pose variable.  


### Syntax 

```python
poseB = pose_inv(poseA)
```

### Example  
```python
     var pose_A, pose_B, pose_C
     var pose_inv_B
     var pose_shift
     
     pose_shift=Shift(10.0, 10.0, 10.0, 0.000, 0.000, 0.000, "base")

     # pose_A : (0,60,0,0,-30,0) 
     pose_A=Pose(0.00,60.00,0.00,0.00,-30.00,0.00)
     pose_A=pose_A.convcrd("base")
 
     pose_B=pose_A+pose_shift
     
     # pose_inv_B is inverse matrix oof pose_B
     pose_inv_B=pose_B
     pose_inv_B=pose_B.convcrd("base")
     pose_inv_B=pose_inv(pose_B)

     # pose_C is same to pose_A
     pose_C=pose_trans(pose_A,pose_B)
     pose_C=pose_trans(pose_C,pose_inv_B)

S1   move P,tg=pose_C,spd=10%,accu=0,tool=0
     
     end
```



[__SOURCE](5-moving-robot/18-axisctrl.md)
# 5.18 axisctrl

### Description
* The `axisctrl` command specifies whether additional axes should move to their target positions when the `move` command is executed to move each axis.
* For a detailed description of the `axisctrl` statement, refer to the link below.  
[${cont_model} Controller Function Manual - Multitasking](https://hrbook-hrc.web.app/#/view/doc-multi-task/en/README)

### Syntax
```python
axisctrl <on/off>,a=<additional axis number>
axisctrl <on/off>,a=[additional axis number, additional axis number, ...]  # Multiple specification possible (up to 4)
```
[__SOURCE](5-moving-robot/19-smov.md)
# 5.19 smov

### Description
The `smov` statement is a procedure used for positioner synchronization.  
For a detailed description of the `smov` statement, refer to the link below.  
[${cont_model} Controller Function Manual - Positioner Synchronization](https://hrbook-hrc.web.app/#/view/doc-positioner-sync/en/README)

<br><br>

### Syntax
```python
smov S<station number>,<interpolation mode>,tg=<target position>,spd=<speed>,accu=<Accuracy>,tool=<tool number>
smov S<station number>,<interpolation mode>,tg=<target position>,spd=<speed>,accu=<Accuracy>,tool=<tool number> until <input signal>
```
[__SOURCE](5-moving-robot/20-shift.md)
# 5.20 shift

### Description
The `shift` statement translates an already taught point in the XYZ coordinate system while maintaining the tool orientation (tool angles).

### Syntax
```python
shift crd=<reference coordinate>,x=<X shift value>,y=<Y shift value>,z=<Z shift value>
```

### Parameters
* crd : Reference coordinate system
["base": base, "robot": robot, "tool": tool, "joint": joint, "u": user]
* x, y, z : X, Y, Z shift values [0-3000, mm]

### Example
```python
     var po1=Pose(0.691,99.293,24.758,-6.528,-48.574,15.774,0.000)
S1   move P,tg=po1,spd=10%,accu=0,tool=0
     shift crd="base",x=200,z=100
S2   move P,tg=po1,spd=10%,accu=0,tool=0
     shift crd="u1",x=-150,y=70,z=10
S3   move P,tg=po1,spd=10%,accu=0,tool=0
     end
```
[__SOURCE](5-moving-robot/21-shift_lim.md)
# 5.21 shift_lim

The `shift_lim` statement is a function that improves safety when using the shift feature by setting the maximum allowable shift amount for the robot.  
If a shift value exceeding the configured limit is entered, an error is generated.

### Syntax
```python
shift_lim x=<X shift limit>, y=<Y shift limit>, z=<Z shift limit>
```

### Parameters
* x, y, z: X, Y, Z shift limit values[0~3000,mm]<br><br>

### Error Guide
* E1196: The shift amount exceeds the configured shift limit. Reduce the shift amount or readjust the shift limit value.

### Example
```python
     var po1 = Pose(0.691, 99.293, 24.758, -6.528, -48.574, 15.774, 0.000)
S1   move P, tg=po1, spd=10%, accu=0, tool=0
     shift_lim x=120, x=200, z=100
     shift crd="base", x=-150, y=70, z=10  # Shift limit exceeded error occurs
S2   move P, tg=po1, spd=10%, accu=0, tool=0
     end
```
[__SOURCE](6-external-comm/README.md)
# 6. Communicating with External Devices


[__SOURCE](6-external-comm/1-fb-io/README.md)
# 6.1 FB Object: Digital I/O

Digital input/output \(I/O\) can be performed through 10 FB objects that can be accessed from HRScript. "FB" refers to fieldbus block, and each FB object is set to be mapped to the I/O hardware installed in the robot controller and contains input and output variables as elements.


[__SOURCE](6-external-comm/1-fb-io/1-io-val.md)
# 6.1.1 Input/Output Variables

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.tg-kftd{background-color:#efefef;}
</style>

<table>
<thead>
  <tr>
    <td colspan="3"></td>
    <td>Type</td>
    <td>Value range</td>
  </tr>
</thead>
<tbody> 
  <tr>
    <td rowspan="10">fb0 ~ fb9</td>
    <td rowspan="5">Digital output</td>
    <td>do[0~959] <br>
    dob[0~119].x[0~7] <br>
    dow[0~118].x[0~15] <br>
    dol[0~116].x[0~31] </td>
    <td>bit</td>
    <td>0, 1</td>
  </tr>
  <tr>
    <td>dob[0~119]</td>
    <td>signed 1byte integer</td>
    <td>-128 ~ +127</td>
  </tr>
  <tr>
    <td>dow[0~118]</td>
    <td>signed 2byte integer</td>
    <td>-32768 ~ +32767</td>
  </tr>
  <tr>
    <td>dol[0~116]</td>
    <td>signed 4byte integer</td>
    <td>-2147483648 ~ +2147483647</td>
  </tr>
  <tr>
    <td>dof[0~116]</td>
    <td>signed 4byte real number</td>
    <td>3.4E+/-38 (7 significant figures)</td>
  </tr>
  <tr>
    <td rowspan="5">Digital input</td>
    <td>di[0~959] <br>
    dob[0~119].x[0~7] <br>
    dow[0~118].x[0~15] <br>
    dol[0~116].x[0~31] </td>
    <td>bit</td>
    <td>0, 1</td>
  </tr>
  <tr>
    <td>dib[0~119]</td>
    <td>signed 1byte integer</td>
    <td>-128 ~ +127</td>
  </tr>
  <tr>
    <td>diw[0~118]</td>
    <td>signed 2byte integer</td>
    <td>-32768 ~ +32767</td>
  </tr>
  <tr>
    <td>dil[0~116]</td>
    <td>signed 4byte integer</td>
    <td>-2147483648 ~ +2147483647</td>
  </tr>
  <tr>
    <td>dif[0~116]</td>
    <td>signed 4byte real number</td>
    <td>3.4E+/-38 (7 significant figures)</td>
  </tr>
</tbody>
</table>

<br><br>

In do, dob, dow, dol, and dof, the suffixes b, w, l, and f mean "byte," "word," "long," and "float," respectively, and all are signed values. These are not separate memory spaces and represent the same 960-byte space just with different data types. For example, do\[1~16\], dob\[1~2\], and dow\[1\] are all the same output signals.

![](../../_assets/image_2.png)

If a value is assigned to an output variable that starts with "do," I/O signal output will be performed. The I/O signal currently being inputted can be acquired by reading the input variable value that starts with "di." The do variable can be read and written, but the di variable can only be read.



The FB object name can be omitted as follows.

| **object name** | **do notation** | fb.do notation |
| :--- | :--- | :--- |
| fb0 | do0 ~ do959 | fb0.do0 ~ fb0.do959 |
| fb1 | do960 ~ do1919 | fb1.do0 ~ fb1.do959 |
| fb2 | do1920 ~ do2879 | fb2.do0 ~ fb2.do959 |
| fb3 | do2880 ~ do3839 | fb3.do0 ~ fb3.do959 |
| fb4 | do3840 ~ do4799 | fb4.do0 ~ fb4.do959 |
| fb5 | do4800 ~ do5759 | fb5.do0 ~ fb5.do959 |
| fb6 | do5760 ~ do6719 | fb6.do0 ~ fb6.do959 |
| fb7 | do6720 ~ do7679 | fb7.do0 ~ fb7.do959 |
| fb8 | do7680 ~ do8639 | fb8.do0 ~ fb8.do959 |
| fb9 | do8640 ~ do9599 | fb9.do0 ~ fb9.do959 |




[__SOURCE](6-external-comm/1-fb-io/2-io-example.md)
# 6.1.2 Examples

Refer to the following examples of usage.

```python
do2=1		# Turns on the bit output value of number 0 of fb0
fb2.dob3=0b00001111  	# Designates the 3rd byte output value of fb2 as a binary bit string
fb[4].dob1=0x0F  	# Turns on the lower 4 bits of the 1st byte output value of fb4, and turns off the upper 4 bits
var work_no=fb9.dib3    # Assigns the 3rd byte input value of fb9 to the work_no variable
if fb5.di43 then *err  	# Branches to the *err label when fb5.di42 is turned on
for idx=21 to 29
  fb3.do[idx]=1  	# Turns on all output signals do21 ~ do29 of fb3 
next
fb2.do3=fb2.do7=fb2.do11=1   # Turns on 3rd, 7th, and 11th output signals of fb2 at once
```


[__SOURCE](6-external-comm/1-fb-io/3-fn-io.md)
# 6.1.3 fn object

You can define fn objects by specifying specific areas of fb objects.
If the ${cont_model} controller is a fieldbus master, and there are multiple fieldbus slave devices, you can set the areas of each slave device to each fn object to handle these slaves intuitively.

![](../../_assets/io/io_fn.png)

See the link below for instructions on how to set up the fn region.

[Operation manual: fn block allocation](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-${cont_model}-tp630/7-system/3-control-parameter/2-io-signal-setting/12-fn-block)
  
&nbsp;

The syntax of fn is the same format as fb.
The fn index is 0 to 63, and the bit index is 0 to 959, just like the fb.
That is, the maximum configurable index is fn0.do0 to fn63.do959.

An error occurs when accessing an unconfigured non-existent fn object or when accessing a do/di that exceeds the set range of fn.

See the use cases below;



```python
fn2.dob3=0b00001111  	# Set the fn2's output byte 3 as a binary bits
fn[4].dob1=0x0F  	# Turns on the fn4's output byte 1's lower 4 bits, and turns off the upper 4 bits.
var work_no=fn63.dib3    # Assign fn63's input byte 3 to the work_no variable
if fn5.di43 then *err  	# Branch to *err label when fn5.di42 is on.
for idx=21 to 29
  fn3.do[idx]=1  	# Turn on all of fn3's output signal do21 ~ do29.
next
fn2.do3=fn2.do7=fn2.do11=1   # Turn on the fn2's output signals 3, 7, and 11 at once.
```

[__SOURCE](6-external-comm/1-fb-io/4-pulse.md)
# 6.1.4 pulse

`pulse` statement is the procedure for signal output of pulse type.

### Description

After tlag time has elapsed, it is output as many times as cnt in the form of On(High) for ton time and Off(Low) for toff time.


### Syntax

```python
pulse <Signal>,tlag=<Lag time>,ton=<On time>,toff=<Off time>,cnt=<output count>
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">Signal</td>
      <td style="text-align:left">
        Output signal name to be output in pulse form<br>
        (Only supports fb.do signals.)
      </td>
      <td style="text-align:left">output signal</td>
    </tr>
    <tr>
      <td style="text-align:left">Lag time</td>
      <td style="text-align:left">
        Time to wait until the pulse signal starts after performing the procedure<br>
        (0.0 ~ 100.0[sec])
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
    <tr>
      <td style="text-align:left">On time</td>
      <td style="text-align:left">
        Time to output signal in On(High) state<br>
        (0.0 ~ 100.0[sec])
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
    <tr>
      <td style="text-align:left">Off time</td>
      <td style="text-align:left">
        Time to output signal in Off (Low) state<br>
        (0.0 ~ 100.0[sec])
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
    <tr>
      <td style="text-align:left">Number of outputs</td>
      <td style="text-align:left">
        Number of times to repeat pulse cycle
        (0 ~ 1000)
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
  </tbody>
</table>

### Sample

```python
   pulse do10,tlag=0.0,ton=1.5,toff=0.5,cnt=5
   end
```
[__SOURCE](6-external-comm/2-http_cli/README.md)
# 6.2 http_cli Module: HTTP Client

Using the general-purpose Ethernet port of the ${cont_model} controller, it is possible to access remote web services and consume HTTP services.
To use this feature, import the `http_cli` module and create an `HttpCli` object as shown below.

```python
import http_cli
var cli = http_cli.HttpCli()
```

After creating an `HttpCli` object, service requests can be made by calling the `get`, `put`, `post`, and `delete` member procedures.<br>
The `HttpCli` object provides an attribute named `body`.<br>
- When a GET request is made and a response is successfully received, the data returned by the remote server is stored in the `body` attribute.<br>The type of the `body` value may be a string, a number, an array, or an object.
- When making a PUT request, the data to be transmitted must be assigned to the `body` attribute in advance.
- When making a POST request, the data to be transmitted must also be assigned to the `body` attribute in advance, and the data returned by the remote server in the response is stored in the `body` attribute.
- The DELETE service does not use the `body` attribute.
The provided HTTP client communication operates in synchronous mode.


[__SOURCE](6-external-comm/2-http_cli/1-http_cli-creator.md)
# 6.2.1 Constructor 

### Description

Creates an HttpCli object and returns a reference to it.

### Syntax


HttpCli\(\)

### Return Value

A reference to the newly created object.

### Usage Example

```python
var cli = http_cli.HttpCli()
```




[__SOURCE](6-external-comm/2-http_cli/2-http_cli-member-var.md)
# 6.2.2 Member Variables

<table>
  <thead>
    <tr>
      <th style="text-align:left">Variable</th>
      <th style="text-align:left">Data Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">body</td>
      <td style="text-align:left">Any</td>
      <td style="text-align:left">
        <p>The data to be transmitted must be assigned in advance for PUT and POST requests.<br><br>If a value other than an object is assigned to `body`, the last path segment of the URL is treated as the key during execution.<br><br>The response data from GET and POST requests is stored in `body`.<br><br>In HRScript, direct access to the member variables of `body` is not supported. To modify or use the data, assign it to another variable first.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">query</td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">
        Used for GET services that require query parameters.<br>The data to be sent with a GET request must be assigned in advance.
      </td>
    </tr>
    <tr>
      <td style="text-align:left">status</td>
      <td style="text-align:left">int</td>
      <td style="text-align:left">
        <p>
            Returns the HTTP response code and error code. (See Section [6.2.4, HTTP Communication Codes](./4-http_cli-code.md))
          <br/>
        </p>
      </td>
    </tr>
  </tbody>
</table>

<br/>

Both `body` and `query` use the object data type.

The object type is supported in the `{ key: value }` format.

```python
cli.body = { name: "WORK #32", color: "green", state: "OK" }
cli.query = { axis: 3 }
```


[__SOURCE](6-external-comm/2-http_cli/3-http_cli-member-proc/README.md)
# 6.2.3 Member Procedures


[__SOURCE](6-external-comm/2-http_cli/3-http_cli-member-proc/1-http_cli-get.md)
# get

### Description

Requests an HTTP GET service.

The server retrieves the information associated with the requested URL and returns it in the response.

The response data is stored in the `body` attribute.

### Syntax

&lt;HttpCli object&gt;.get &lt;URL string, timeout, timeout fallback address&gt;


### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Item</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Note</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>URL string</td>
      <td>
        The request URL.
      </td>
      <td></td>
    </tr>
    <tr>
      <td>Timeout</td>
      <td>
        (Optional) Timeout duration. If the timeout expires, execution proceeds to the next statement or to the fallback address.<br>If not specified, the request waits indefinitely.<br>The timeout must be set between 5 ms and 15 ms (inclusive). Otherwise, a playback timeout error occurs.<br>If the value is outside this range, `-9 (InvalidTimeout)` is stored in `status`. 
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>timeout fallback address</td>
      <td>
        (Optional) The address to branch to when a timeout occurs.<br>If not specified, execution proceeds to the next address.
      </td>
      <td>Address</td>
    </tr>
  </tbody>
</table>


### Usage Example

```python
#case 1
var domain="http://192.168.1.200:8888"
cli.get domain+"/setting/max_torque"

#case 2
var url = domain+"/joints/max_speed"
cli.query = {axis: 3}
cli.get url, 10, *timeout
# cli.get(url, 10, *timeout) also possible
```




[__SOURCE](6-external-comm/2-http_cli/3-http_cli-member-proc/2-http_cli-put.md)
# put

### Description

Requests an HTTP PUT service.

Updates the specified resource.

The data to be transmitted must be assigned to the `body` attribute in advance.

### Syntax

&lt;HttpCli object&gt;.put &lt;URL string, timeout, timeout fallback address&gt;


### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Item</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Note</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>URL string</td>
      <td>
        The request URL.
      </td>
      <td></td>
    </tr>
    <tr>
      <td>Timeout</td>
      <td>
        (Optional) Timeout duration. If the timeout expires, execution proceeds to the next statement or to the fallback address.<br>If not specified, the request waits indefinitely.<br>The timeout must be set between 5 ms and 15 ms (inclusive). Otherwise, a playback timeout error occurs.<br>If the value is outside this range, `-9 (InvalidTimeout)` is stored in `status`.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>timeout fallback address</td>
      <td>
        (Optional) The address to branch to when a timeout occurs.<br>If not specified, execution proceeds to the next address.
      </td>
      <td>Address</td>
    </tr>
  </tbody>
</table>

### Usage Example

```python
#case 1
var domain="http://192.168.1.200:8888"
cli.body=500
cli.put domain+"/setting/max_torque"

#case 2
var url = domain + "/setting"
cli.body = {max_torque: 500}
cli.put(url, 10, S1)
```




[__SOURCE](6-external-comm/2-http_cli/3-http_cli-member-proc/3-http_cli-post.md)
# post

### Description

Requests an HTTP POST service.

Creates the specified resource.

The data to be transmitted must be assigned to the `body` attribute in advance.

The response data returned by the remote server is stored in the `body` attribute.

### Syntax

&lt;HttpCli object&gt;.post &lt;URL string, timeout, timeout fallback address&gt;

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Item</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>URL string</td>
      <td>
      The request URL.
      </td>
      <td></td>
    </tr>
    <tr>
      <td>Timeout</td>
      <td>
        (Optional) Timeout duration. If the timeout expires, execution proceeds to the next statement or to the fallback address.<br>If not specified, the request waits indefinitely.<br>The timeout must be set between 5 ms and 15 ms (inclusive). Otherwise, a playback timeout error occurs.<br>If the value is outside this range, `-9 (InvalidTimeout)` is stored in `status`.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>timeout fallback address</td>
      <td>
        (Optional) The address to branch to when a timeout occurs.<br>If not specified, execution proceeds to the next address.
      </td>
      <td>Address</td>
    </tr>
  </tbody>
</table>

### Usage Example 

```python
#case 1
var domain="http://192.168.1.200:8888"
cli.body={ name: "WORK #32", color: "green", state: "OK" }
cli.post domain+"/display/update"

#case 2
var url = domain+"/display/update"
cli.post url, 10, *TimeOut
```


[__SOURCE](6-external-comm/2-http_cli/3-http_cli-member-proc/4-http_cli-delete.md)
# delete

### Description

Requests an HTTP DELETE service.

Deletes the specified resource.

The `body` attribute is not used for this request.

### Syntax

&lt;HttpCli object&gt;.delete &lt;URL string, timeout, timeout fallback address&gt;


### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Item</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>URL string</td>
      <td>
        The request URL.
      </td>
      <td></td>
    </tr>
    <tr>
      <td>Timeout</td>
      <td>
        (Optional) Timeout duration. If the timeout expires, execution proceeds to the next statement or to the fallback address.<br>If not specified, the request waits indefinitely.<br>The timeout must be set between 5 ms and 15 ms (inclusive). Otherwise, a playback timeout error occurs.<br>If the value is outside this range, `-9 (InvalidTimeout)` is stored in `status`.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>Timeout fallback address</td>
      <td>
        (Optional) The address to branch to when a timeout occurs.<br>If not specified, execution proceeds to the next address. 
      </td>
      <td>Address</td>
    </tr>
  </tbody>
</table>

### Usage Example

```python
var domain="http://192.168.1.200:8888"
cli.delete domain+"/items"
```


[__SOURCE](6-external-comm/2-http_cli/4-http_cli-code.md)
# 6.2.4 HTTP Communication Codes

* Major HTTP Response Codes 
<table>
  <thead>
    <tr>
      <th style="text-align:left">Response Category</th>
      <th style="text-align:left">Response Code</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2">Informational</td>
      <td>
        100
      </td>
      <td>
      continue
      </td>
    </tr>
    <tr>
      <td>
        101
      </td>
      <td>
      Switching protocols
      </td>
    </tr>
    <tr>
    <tr>
      <td rowspan="5">Success</td>
      <td>
        200
      </td>
      <td>
      OK
      </td>
    </tr>
    <tr>
      <td>
        201
      </td>
      <td>
      Created
      </td>
    </tr>
    <tr>
      <td>
        202
      </td>
      <td>
      Accepted
      </td>
    </tr>
    <tr>
      <td>
        203
      </td>
      <td>
      Non-authoritative information
      </td>
    </tr>
    <tr>
      <td>
        204
      </td>
      <td>
      No content
      </td>
    </tr>
    <tr>
    <tr>
      <td rowspan="3">Redirection</td>
      <td>
        301
      </td>
      <td>
      Moved permanently
      </td>
    </tr>
    <tr>
      <td>
        302
      </td>
      <td>
      Not temporarily
      </td>
    </tr>
    <tr>
      <td>
        303
      </td>
      <td>
      Not modified
      </td>
    </tr>
    <tr>
      <td rowspan="11">Client error</td>
      <td>
        400
      </td>
      <td>
      Bad Request
      </td>
    </tr>
    <tr>
      <td>
        401
      </td>
      <td>
      Unauthorized 
      </td>
    </tr>
    <tr>
      <td>
        402
      </td>
      <td>
      Payment required
      </td>
    </tr>
    <tr>
      <td>
        403
      </td>
      <td>
      Forbidden 
      </td>
    </tr>
    <tr>
      <td>
        404
      </td>
      <td>
      Not found 
      </td>
    </tr>
    <tr>
      <td>
        405
      </td>
      <td>
      Method not allowed
      </td>
    </tr>
    <tr>
      <td>
        407
      </td>
      <td>
      Proxy authentication required 
      </td>
    </tr>
    <tr>
      <td>
        408
      </td>
      <td>
      Request timeout
      </td>
    </tr>
    <tr>
      <td>
        410
      </td>
      <td>
      Gone  
      </td>
    </tr>
    <tr>
      <td>
        412
      </td>
      <td>
      Precondition failed
      </td>
    </tr>
    <tr>
      <td>
        414
      </td>
      <td>
      Request-URI too long
      </td>
    </tr>
    <tr>
      <td rowspan="5">Server error</td>
      <td>
        500
      </td>
      <td>
       Internal server error 
      </td>
    </tr>
    <tr>
      <td>
        501
      </td>
      <td>
      Not implemented
      </td>
    </tr>
    <tr>
      <td>
        503
      </td>
      <td>
      Service unnailable
      </td>
    </tr>
    <tr>
      <td>
        504
      </td>
      <td>
      Gateway timeout
      </td>
    </tr>
    <tr>
      <td>
        505
      </td>
      <td>
      HTTP version not supported
      </td>
    </tr>
  </tbody>
</table>


* Error Code (Exception)

<table>
  <thead>
    <tr>
    <th style="text-align:left">Error Name</th>
      <th style="text-align:left">Error Code</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>RequestException</td>      
      <td>
        -1
      </td>
      <td>
      There was an ambiguous exception that occurred while handling your request.
      </td>
    </tr>
    <tr>
      <td> ConnectionErr</td>
      <td>
        -2
      </td>
      <td>
      In the event of a network problem (e.g. DNS failure, refused connection, etc)
      </td>
    </tr>
    <tr>
    <td> HTTPError
      <td>
        -3
      </td>
      <td>
      It will occur if the HTTP request returned an unsuccessful status code.
      </td>
    </tr>
    <tr>
    <td>URLRequired</td>
      <td>
        -4
      </td>
      <td>
      A valid URL is required to make a request.
      </td>
    </tr>
    <tr>
    <td>TooManyRedirects</td>
      <td>-5</td>
      <td>
      If a request exceeds the configured number of maximum redirections, a TooManyRedirects exception is raised.
      </td>
    </tr>
    <tr>
    <td>Timeout</td>
      <td>
        -6
      </td>
      <td>
      If a request times out, a Timeout exception is raised.
      </td>
    </tr>
    <td>SessionInvalid</td>
      <td>
        -7
      </td>
      <td>
        This error indicates that the session is invalid because a runtime error occurred while processing a session request.     Session is invalid. This error apears when the runtime error is happend during session requests.
      </td>
    </tr>
    <td>UnhandledException</td>
      <td>
        -8
      </td>
      <td>
        An unexpected error occurred during the HTTP request or response processing (e.g., session creation, request execution, or response parsing) and did not match any explicitly handled exceptions. The request outcome is therefore reported as UnhandledException.
      </td>
    </tr>
    <td>InvalidTimeout</td>
      <td>
        -9
      </td>
      <td>
        When the timeout value exceeds the range of 5 ms to 15 ms.
      </td>
    </tr>
  </tbody>
</table>

[__SOURCE](6-external-comm/2-http_cli/5-http_cli-example.md)
# HTTP Client Usage Examples

```python
     import http_cli
     var cli=http_cli.HttpCli()
     var url, body, query, status_code
     var domain="http://192.168.1.200:8888"

     # get
     cli.get domain+"/device/direction"
     body = cli.body

     #check the communication status
     if cli.status>=400 or cli.status<0
        goto 99 		#http communication error
     endif

     # put
     url = domain+"/device/direction"
     body.ry=90
     cli.body=body
     cli.put(url, 3000, *Timeout)

     # post
     cli.body={ name: "WORK #32", color: "green", state: "OK" }
     cli.post domain+"/display/update", 5000, *Timeout

     # delete
     cli.delete(domain+"/items")

     end
     
  99 print "error status"
     
     *Timeout
     print "timeout"
```


[__SOURCE](6-external-comm/3-tp-console-bar/README.md)
# 6.3 Input/Output with Teach Pendant console bar



[__SOURCE](6-external-comm/3-tp-console-bar/1-print.md)
# 6.3.1 print

### Description

`print` statement prints a string to the guide-bar of the Teach Pendant. In addition to string constants, any type of expression (including constants and variables) result converted into a string and printed out. If you specify multiple expressions, each expression is printed separated by a single space character.

### Syntax

```python
print <expression>[,<expression>,<expression>...]
```


### Parameter

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">expression</td>
      <td style="text-align:left">
        <p>Expresion to print out.<br>
        All types of boolean, number, string, array, object are supported.
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### Example

```python
input work_no
input work_no,10
input work_no,10,*timeout
```

[__SOURCE](6-external-comm/3-tp-console-bar/2-input.md)
# 6.3.2 input

### Description

Use the **input** statement to enter a string as a keystroke of the Teach Pendant and store it in a variable. If not entered by the timeout, proceed to the following statement or branch to the timeout address.

### Syntax

```python
input <variable>;[,<timeout>,<timeout address>]
```


### Parameter

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">variable</td>
      <td style="text-align:left">
        <p>Variable to receive input. Numbers are also entered as string types. If
          numerical values are required, convert to int( ) or double( ) functions.
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">timeout</td>
      <td style="text-align:left">Maximum time limit</td>
      <td style="text-align:left">0.1~60.0 sec
        <br />
      </td>
    </tr>
    <tr>
      <td style="text-align:left">timeout address</td>
      <td style="text-align:left">Address to branch when timeout is exceeded</td>
      <td style="text-align:left">address</td>
    </tr>
  </tbody>
</table>

### Example

```python
input work_no
input work_no,10
input work_no,10,*timeout
```

![](../../_assets/image_6.png)




[__SOURCE](6-external-comm/4-modbus/README.md)
# 6.4 Modbus module : Modbus master

Modbus master operations can be performed in HRScript. For detailed information on modbus communication functions, please refer to the separate manual. [${cont_model} Controller Function Manual - Modbus](https://hrbook-hrc.web.app/#/view/doc-modbus/en/README)  

[__SOURCE](6-external-comm/5-sci/README.md)
# 6.5 Sci module : Serial communication

Serial communication can be performed through the COM port of the ${cont_model} controller.

To use this function, you must create a Sci object as a global variable as shown below.

Also, be sure to check the settings specifications in [System > 2. Control Parameters > 3. Serial Port] before use.

```python
global sci2
sci2=com.Sci(2)
```

After creating a Sci object, simply call the send, recv, open, and close member procedures.

When calling send, you must input the string to be sent in advance.

When calling recv, it is assigned to the specified string variable upon successful reception. 

When calling open, the port is opened.

When calling open, the port is closed.





[__SOURCE](6-external-comm/5-sci/1-sci-creator.md)
# 6.5.1 Constructor

### Description

Creates a global variable for the Sci object.

### Syntax

com.Sci(port number)

### Return Value

Reference to created object

### Example

```python
global sci2
sci2=com.Sci(2)
```




[__SOURCE](6-external-comm/5-sci/2-sci-member-proc/README.md)
# 6.5.2 Member procedure
[__SOURCE](6-external-comm/5-sci/2-sci-member-proc/1-sci-send.md)
# send

### Description

Send a string by calling Sci's send.

### Syntax

&lt;Sci object&gt;.send "string" <br>
&lt;Sci object&gt;.send string variable


### Example

```python
sci2.send "test"
or
var msg="test"
sci2.send msg
```




[__SOURCE](6-external-comm/5-sci/2-sci-member-proc/2-sci-recv.md)
# recv

### Description

Call Sci's recv to receive a string.


### Syntax

&lt;Sci object&gt;.recv string variable \[,{timeout}\] \[,{goto address}\]


### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Item</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Etc</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>string variable</td>
      <td>
        A string variable that will hold the entered string when successfully received.<br>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>timeout</td>
      <td>
        When no data is received for a specified time, it branches to the goto address, and if there is no goto address, an error occurs.<br>
        If not specified, it waits indefinitely.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>goto address</td>
      <td>
        Address to branch to when timeout occurs.<br>
        If not specified, it stops with an error.
      </td>
      <td>address</td>
    </tr>
  </tbody>
</table>


### Example

```python
   var msg
   sci2.recv msg,5000,*timeout
   print msg
   ...
   ...
   *timeout
   print "timeout error"
   stop
```




[__SOURCE](6-external-comm/5-sci/2-sci-member-proc/3-sci-open.md)
# open

### Description

Execute Sci's open() function to open the serial port.

The serial port is opened with the preset contents through the controller settings, and there is no need to separately open the port unless the port was previously closed.(default: open)


### Syntax

&lt;Sci object&gt;.open()

### Return Value
- 0: Success
- <0: Fail


### Example

```python
var ret
ret=sci2.open()
if ret<0
  print "open error"
  stop
endif
```




[__SOURCE](6-external-comm/5-sci/2-sci-member-proc/4-sci-close.md)
# close

### Description

Execute Sci's close to close the serial port.


### Syntax

&lt;Sci object&gt;.close()

### Return Value
- 0: Success
- -1: Fail

### Example

```python
var ret
ret=sci2.close()
if ret<0
  print "open error"
  stop
endif
```




[__SOURCE](6-external-comm/5-sci/2-sci-member-proc/5-sci-clr-rbuf.md)
# clr_rbuf

### Description

Initialize Sci's received buffer.


### Syntax

&lt;Sci object&gt;.clr_rbuf()

### Return Value
- 0: Receive buffer initialization success
- -1: Fail

### Example

```python
var ret
ret=sci2.clr_rbuf()
if ret<0
  print "receive buffer clear error"
  stop
endif
```




[__SOURCE](6-external-comm/5-sci/3-sci-example.md)
# 6.5.3 Serial communication example

``` python
Hyundai Robot Job File; { version: 1.6, mech_type: "", total_axis: -1, aux_axis: -1 }
     
     # Create a Sci object using the constructor and assign it to a global variable 
     global sci2
     sci2=sci.Sci(2)   #port no. (com2)
     
     # clear receive buffer
     var ret
     ret=sci2.clr_rbuf()

     # send
     sci2.send "test"

     # receive (option: when 3000ms over, goto *timeout)
     var msg
     sci2.recv msg,3000,*timeout
     print msg

     end

     *timeout
     print "error"
     stop

```



[__SOURCE](7-enet-module/README.md)
# 7 enet module : Ethernet TCP/UDP communication

Using the ${cont_model} controller's user ethernet port, You can send and receive strings or binary data over Ethernet TCP or UDP communication with an external devices.

The enet module can create two objects, ENet and BBuf. ENet provides an Ethernet socket interface, and BBuf is used to communicate binary data.

Let's follow the client example and the server example to understand how to use it. A reference guide for each object's member variables and functions follows it.

[__SOURCE](7-enet-module/1-exam-client/README.md)
# 7.1 peer-to-peer, client example

The UDP peer-to-peer (1:1 communication), or TCP client example program is explained for string and binary transmission.

[__SOURCE](7-enet-module/1-exam-client/1-enet-client-str.md)
# 7.1.1 peer-to-peer, client Example - Transceiving string data

Follow these steps:

1. After importing the `enet` module, create an `ENet` object with the constructor.
2. Set the IP address and port number with the member variables.
   - `Caution: Ports 50000-50005 on the controller are pre-allocated lports and cannot be used.`
3. Open the ethernet socket with the `open` member procedure, and check the status with the `state()` member variable.
\(For TCP communication, the `connect` procedure must also be called after opening.\)
1. Transceiving with `send` and `recv` member procedure.
2. Close the communication connection with the `close` member procedure.

<br>

### UDP peer-to-peer
```python
     # 1. After importing the enet module, create an ENet object with the constructor
     import enet
     var cli=enet.ENet() # for TCP communication, ENet("tcp")

     # 2. Set the IP address and port number
     cli.ip_addr="192.168.1.172" # remote (opponent) IP address
     cli.lport=51001 # local (self) port
     cli.rport=51002 # remote (opponent) port
     # (port no. 49152-65535(except 50000-50005) contains dynamic or private ports)

     # 3. Open ethernet socket
     cli.open
     
     print cli.state() # If 1, it's OK.

     # --------------------------------
     # 4-1. string trasmitting
     cli.send "hello, peer.\n"

     # 4-2. string receiving
     #     (if not received for 5 seconds, jump to *TimeOut label)
     var msg
     cli.recv 5000, *TimeOut
     var msg=result() # received string
     print msg
     delay 1.0
     # --------------------------------

     # 5. Close ethernet socket
     cli.close
     print cli.state() # If 0, it's OK.
     delay 1.5
     end

     *TimeOut
     print "time out!"
     cli.close
     end
```
<br>

### TCP client
(Only `lport` and `connect` parts are different from peer-to-peer.)
```python
     # 1. After importing the enet module, create an ENet object with the constructor
     import enet
     var cli=enet.ENet() # for TCP communication, ENet("tcp")

     # 2. Set the IP address and port number
     cli.ip_addr="192.168.1.172" # remote (opponent) IP address
     cli.lport=0 # local (self) port; random
     cli.rport=51002 # remote (opponent) port
     # (port no. 49152-65535 contains dynamic or private ports)

     # 3. Open ethernet socket
     cli.open
     cli.connect # connect to the server.
     print cli.state() # If 1, it's OK.

     # --------------------------------
     # 4-1. string trasmitting
     cli.send "hello, peer.\n"

     # 4-2. string receiving
     #     (if not received for 5 seconds, jump to *TimeOut label)
     var msg
     cli.recv 5000, *TimeOut
     var msg=result() # received string
     print msg
     delay 1.0
     # --------------------------------

     # 5. Close ethernet socket
     cli.close
     print cli.state() # If 0, it's OK.
     delay 1.5
     end

     *TimeOut
     print "time out!"
     cli.close
     end
```

[__SOURCE](7-enet-module/1-exam-client/2-enet-client-bin.md)
# 7.1.2 peer-to-peer, client Example - Transceiving binary data

Binary transceiving are performed using `BBuf` (binary buffer) object.  
(Only the transceiving parts are different, and the rest are the same as the transceiving string data.)

Sending

1. Create `enet.BBuf` object.
2. Append the desired binary data to the `BBuf` object with the `BBuf.append()` function.
3. Send the BBuf object as a function of `ENET.send_bbuf()`


Receiving

1. Create `enet.BBuf` object.
2. Receive binary data into BBuf objects with the `ENET.recv_bbuf()` function.
3. Read the desired binary data from the `BBuf` object with the `BBuf.read_nums()` function.


<br>

### UDP peer-to-peer
```python
     # 1. After importing the enet module, create an ENet object with the constructor
     import enet
     var cli=enet.ENet() # For TCP communications, ENet("tcp")

     # 2. Set the IP address and port number
     cli.ip_addr="192.168.1.172" # remote (opponent) IP address
     cli.lport=51001 # local (self) port
     cli.rport=51002 # remote (opponent) port
     # (port no. 49152-65535(except 50000-50005) contains dynamic or private ports)

     # 3. Open ethernet socket
     cli.open
     
     print cli.state() # If 1, it's OK.

     # Sending --------------------------------
     # 4-1. Create BBuf object
     var bbuf=enet.BBuf()

     # (sample binary data)
     var arr=[ -3, 0, 1 ]
     
     # 4-2. Append binary data to BBuf object
     bbuf.clear()
     bbuf.append("s4", arr) # append little endian signed-4byte data

     # 4-3. Send BBuf object
     var ret
     ret=cli.send_bbuf(bbuf)

     # Receiving --------------------------------
     # 4-1. Create BBuf object
     var bbuf2=enet.BBuf()
     
     # 4-2. Receive binary data into BBuf object
     #     (If no response for 3 seconds, jump to *TimeOut label)
     cli.recv_bbuf bbuf2,3000,*TimeOut

     # 4-3. Read binary data from BBuf object.
     var nums=bbuf2.read_nums("U2", 0, 3) # read 3 big-endian unsigned-2byte data
     print nums
     # --------------------------------

     # 5. Close ethernet socket
     cli.close
     print cli.state() # If 0, it's OK.
     delay 1.5
     end

     *TimeOut
     print "time out!"
     cli.close
     end
```


### TCP client
(Only `lport` and `connect` parts are different from peer-to-peer.)
```python
     # 1. After importing the enet module, create an ENet object with the constructor
     import enet
     var cli=enet.ENet() # For TCP communications, ENet("tcp")

     # 2. Set the IP address and port number
     cli.ip_addr="192.168.1.172" # remote (opponent) IP address
     cli.lport=0 # local (self) port; random
     cli.rport=51002 # remote (opponent) port
     # (port no. 49152-65535 contains dynamic or private ports)

     # 3. Open ethernet socket
     cli.open
     cli.connect # connect to the server.
     print cli.state() # If 1, it's OK.

     # Sending --------------------------------
     # 4-1. Create BBuf object
     var bbuf=enet.BBuf()

     # (sample binary data)
     var arr=[ -3, 0, 1 ]
     
     # 4-2. Append binary data to BBuf object
     bbuf.clear()
     bbuf.append("s4", arr) # append little endian signed-4byte data

     # 4-3. Send BBuf object
     var ret
     ret=cli.send_bbuf(bbuf)

     # Receiving --------------------------------
     # 4-1. Create BBuf object
     var bbuf2=enet.BBuf()
     
     # 4-2. Receive binary data into BBuf object
     #     (If no response for 3 seconds, jump to *TimeOut label)
     cli.recv_bbuf bbuf2,3000,*TimeOut

     # 4-3. Read binary data from BBuf object.
     var nums=bbuf2.read_nums("U2", 0, 3) # read 3 big-endian unsigned-2byte data
     print nums
     # --------------------------------

     # 5. Close ethernet socket
     cli.close
     print cli.state() # If 0, it's OK.
     delay 1.5
     end

     *TimeOut
     print "time out!"
     cli.close
     end
```

* String arguments such as "s4" and "U2" determine the binary data format such as endian type, signed/unsigned, and the number of bytes. For more information, see [7.4.2 Supported format](../4-bbuf/2-format.md).
[__SOURCE](7-enet-module/2-exam-server/README.md)
# 7.2 TCP server example

The TCP server example program is explained for the case of tranceiving string data and binary data.

While the TCP client connects to the server with the `connect()` function, the TCP server calls the `listen()` function and waits for the client's connection with the `accept()` function.  

* Allow only one client connection at the same time.
* You do not need to specify a remote port.

The rest of the action is the same as the client.
[__SOURCE](7-enet-module/2-exam-server/1-enet-server-str.md)
# 7.2.1 ethernet TCP server - Transceiving string data

Follow these steps:

1. After importing the `enet` module, create an `ENet` object with the constructor.
2. Set the IP address and port number with the member variables. (remote port setting is not needed.)
   - `Caution: Ports 50000-50005 on the controller are pre-allocated lports and cannot be used.`
3. Open the ethernet socket with the `open` member procedure, and calls `listen()`, `accept()` function. Check the status with the `state()` member variable.
4. Transceiving with `send` and `recv` member procedure.
5. Close the communication connection with the `close` member procedure.


```python
     # 1. After importing the enet module, create an ENet object with the constructor
     import enet
     var svr=enet.ENet("tcp")
     
     # 2. Set the IP address and port number
     svr.ip_addr="192.168.1.172" # remote (opponent) IP address
     svr.lport=51001 # local (self) port
     # (port no. 49152-65535(except 50000-50005) contains dynamic or private ports)
     
     # 3. Open ethernet socket
     svr.open
     var ret
     ret=svr.listen()
     ret=svr.accept() # wait for connect from client
     print svr.state() # If 1, it's OK.
     
     # --------------------------------
     # 4-1. string trasmitting
     svr.send "Welcome, I am a TCP server.\n"
     
     # 4-2. string receiving
     #     (if not received for 5 seconds, jump to *TimeOut label)
     svr.recv 5000,*TimeOut
     var msg=result() # received string
     print msg
     delay 1.0
     # --------------------------------
     
     # 5. Close ethernet socket
     svr.close
     print svr.state() # If 0, it's OK.
     delay 1.5
     end

     *TimeOut
     print "time out!"
     svr.close
     end
```

[__SOURCE](7-enet-module/2-exam-server/2-enet-server-bin.md)
# 7.2.2 ethernet TCP server Example - Transceiving binary data

Binary transceiving are performed using BBuf (binary buffer) object.  
(Only the transceiving parts are different, and the rest are the same as the transceiving string data.)

Sending

1. Create `enet.BBuf` object.
2. Append the desired binary data to the `BBuf` object with the `BBuf.append()` function.
3. Send the BBuf object as a function of `ENET.send_bbuf()`


Receiving

1. Create `enet.BBuf` object.
2. Receive binary data into BBuf objects with the `ENET.recv_bbuf()` function.
3. Read the desired binary data from the `BBuf` object with the `BBuf.read_nums()` function.


```python
     # 1. After importing the enet module, create an ENet object with the constructor
     import enet
     var svr=enet.ENet("tcp")
     
     # 2. Set the IP address and port number
     svr.ip_addr="192.168.1.172" # remote (opponent) IP address
     svr.lport=51001 # local (self) port
     # (port no. 49152-65535(except 50000-50005) contains dynamic or private ports)
     
     # 3. Open ethernet socket
     svr.open
     var ret
     ret=svr.listen()
     ret=svr.accept() # wait for connect from client
     print svr.state() # If 1, it's OK.

     # Sending --------------------------------
     # 4-1. Create BBuf object
     var bbuf=enet.BBuf()

     # (sample binary data)
     var arr=[ -3, 0, 1 ]
     
     # 4-2. Append binary data to BBuf object
     bbuf.clear()
     bbuf.append("s4", arr) # append little endian signed-4byte data

     # 4-3. Send BBuf object
     ret=svr.send_bbuf(bbuf)

     # Receiving --------------------------------
     # 4-1. Create BBuf object
     var bbuf2=enet.BBuf()
     
     # 4-2. Receive binary data into BBuf object
     #     (If no response for 3 seconds, jump to *TimeOut label)
     svr.recv_bbuf bbuf2,3000,*TimeOut

     # 4-3. Read binary data from BBuf object.
     var nums=bbuf2.read_nums("U2", 0, 3) # read 3 big-endian unsigned-2byte data
     print nums
     # --------------------------------

     # 5. Close ethernet socket
     svr.close
     print svr.state() # If 0, it's OK.
     delay 1.5
     end

     *TimeOut
     print "time out!"
     svr.close
     end
```

* String arguments such as "s4" and "U2" determine the binary data format such as endian type, signed/unsigned, and the number of bytes. For more information, see [7.4.2 supported format](../4-bbuf/2-format.md).

[__SOURCE](7-enet-module/3-enet/README.md)
# 7.3 ENet object

The `ENet` object provides a socket interface for Ethernet communication.  
See the examples in the previous section for instructions on how to use them.

[__SOURCE](7-enet-module/3-enet/1-enet-creator.md)
# 7.3.1 ENet creator

### Description

Create an Ethernet object. Returns the reference of the created object.

### Syntax

`ENet({protocol})`

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Misc.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>protocol</td>
      <td>
        "tcp" : TCP comm.<br>
        "udp" : UDP comm.<br>
        If omitted, recognized as "udp".</td>
    </tr>
  </tbody>
</table>

### Return value

Reference of the created object.

### Example

```python
enet0 = ENet()
var tcp = ENet("tcp")
```

[__SOURCE](7-enet-module/3-enet/2-enet-member-var.md)
# 7.3.2 ENet member variable

<table>
  <thead>
    <tr>
      <th style="text-align:left">Variable name</th>
      <th style="text-align:left">Data type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">ip_addr</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        readable/writable<br>
        Set or get the IP address of the communication opponent(remote).<br>
        Applied only when calling the open statement.
      </td>
    </tr>
    <tr>
      <td style="text-align:left">rport</td>
      <td style="text-align:left">number</td>
      <td style="text-align:left">
        readable/writable<br>
        Set or get the port number of the communication opponent(remote).<br>
        Applied only when calling the open statement.
      </td>
    </tr>
    <tr>
      <td style="text-align:left">lport</td>
      <td style="text-align:left">number</td>
      <td style="text-align:left">
        readable/writable<br>
        Only used in UDP peer-to-peer and TCP server, ignored in TCP client.<br>
        Set or get the controller's own (local) port number.<br>
        The default value is 0 (if not specified), in which case this port number is automatically generated.<br>
        Applied only when calling the open statement.<br>
        Ports 50000-50005 on the controller are pre-allocated lports and cannot be used.
      </td>
    </tr>
  </tbody>
</table>


[__SOURCE](7-enet-module/3-enet/3-enet-member-func/README.md)
# 7.3.3 ENet member function

* When getting the return value from a member function, be sure to enclose the argument in parentheses.
  
  ```python
  var nitem=obj.func(param1,param2) # (O) ; parentheses is necessary
  var nitem=obj.func param1,param2 # (X) ; syntax error
  ```

* Parentheses can be omitted, not getting the return value.

  ```python
  obj.func(param1,param2) # (O)
  obj.func param1,param2 # (O) ; parentheses omitted
  ```
[__SOURCE](7-enet-module/3-enet/3-enet-member-func/enet-accept.md)
# accept

### Description

As a server in Ethernet TCP communication, it waits for a connection request from the client side. Creates a connection when a request occurs.
Not used in UDP peer-to-peer communication.


### Syntax

`{ENet object}.accept [{waiting time}] [, {address on timeout}]`


### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Misc.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>waiting time</td>
      <td>
        timeout. If elapsed, proceed to the next command or jump to the address on timeout.<br>
        If not specified, wait ininfinitely.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>address on timeout</td>
      <td>
        address to which jump on timeout.<br>
        If not specified, proceed to next command.
      </td>
      <td>address</td>
    </tr>
  </tbody>
</table>


### Return value

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Misc.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>
        OK (completed)
      </td>
      <td></td>
    </tr>  
    <tr>
      <td>0</td>
      <td>
        waiting
      </td>
      <td></td>
    </tr>
    <tr>
      <td>-1</td>
      <td>timeout</td>
      <td></td>
    </tr>
    <tr>
      <td>-2</td>
      <td>error</td>
      <td></td>
    </tr>    
  </tbody>
</table>


### Example

```python
enet_to_sensor.listen
var ret=enet_to_sensor.accept(5000)
```

```python
enet_to_sensor.listen
enet_to_sensor.accept 5000,*TimeOut
```


[__SOURCE](7-enet-module/3-enet/3-enet-member-func/enet-close.md)
# close

### Description

Closes the connection for Ethernet TCP or UDP communication.

### Syntax

`{ENet object}.close`

### Example

```python
enet_to_sensor.close
```

[__SOURCE](7-enet-module/3-enet/3-enet-member-func/enet-connect.md)
# connect

### Description


As a client in Ethernet TCP communication, it tries to connect to the server.
Not used in UDP peer-to-peer communication.

### Syntax

`{ENet object}.connect [{waiting time}] [, {address on timeout}]`


### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Misc.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>waiting time</td>
      <td>
        timeout. If elapsed, proceed to the next command or jump to the address on timeout.<br>
        If not specified, wait ininfinitely.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>address on timeout</td>
      <td>
        address to which jump on timeout.<br>
        If not specified, proceed to next command.
      </td>
      <td>address</td>
    </tr>
  </tbody>
</table>


### Return value

<table>
  <thead>
    <tr>
      <th style="text-align:left">Value</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Misc.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>
        OK (completed)
      </td>
      <td></td>
    </tr>  
    <tr>
      <td>0</td>
      <td>
        waiting
      </td>
      <td></td>
    </tr>
    <tr>
      <td>-1</td>
      <td>timeout</td>
      <td></td>
    </tr>
    <tr>
      <td>-2</td>
      <td>error</td>
      <td></td>
    </tr>  
  </tbody>
</table>


### Example

```python
var ret=enet_to_sensor.connect(5000)
```

```python
enet_to_sensor.connect 5000,*TimeOut
```
[__SOURCE](7-enet-module/3-enet/3-enet-member-func/enet-listen.md)
# listen

### Description

As a server in Ethernet TCP communication, it prepares for a connection request from the client side. 
Not used in UDP peer-to-peer communication.


### Syntax

`{ENet object}.listen [{backlog}]`


### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Misc.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>backlog</td>
      <td>
        The permitted connection of the pending connection which is not acceptted.<br>
        If not specified, wait ininfinitely.
      </td>
      <td></td>
    </tr>
  </tbody>
</table>


### Return value

<table>
  <thead>
    <tr>
      <th style="text-align:left">Value</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Misc.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>
        OK
      </td>
      <td></td>
    </tr>
    <tr>
      <td>-1</td>
      <td>error</td>
      <td></td>
    </tr>	 
  </tbody>
</table>


### Example

```python
enet_to_sensor.listen
enet_to_sensor.accept 5000,*TimeOut
```

[__SOURCE](7-enet-module/3-enet/3-enet-member-func/enet-open.md)
# open

### Description

Opens a connection for Ethernet TCP or UDP communication.

### Syntax

`{ENet object}.open`

### Example

```python
enet_to_sensor.open
```

[__SOURCE](7-enet-module/3-enet/3-enet-member-func/enet-recv.md)
# recv

### Description

Receives string data from the Ethernet object. The received string can be get from return value or `result()` function.


### Syntax

`{ENet object}.recv [{waiting time}][,{address on timeout}]`


### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Misc.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>waiting time</td>
      <td>
        timeout. If elapsed, proceed to the next command or jump to the address on timeout.<br>
        If not specified, wait ininfinitely.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>address on timeout</td>
      <td>
        address to which jump on timeout.<br>
        If not specified, proceed to next command.
      </td>
      <td>address</td>
    </tr>
  </tbody>
</table>


### Return value

The received string.


### Example

```python
var msg
msg=enet_to_sensor.recv
msg=enet_to_sensor.recv(5000)
msg=enet_to_sensor.recv(5000,*TimeOut)
end

*TimeOut
print "Time out! No response from sensor"
end
```

[__SOURCE](7-enet-module/3-enet/3-enet-member-func/enet-recv_bbuf.md)
# recv_bbuf

### Description

Receives binary data from the Ethernet object and stores it in the [BBuf](../../4-bbuf/README.md) object.


### Syntax

`{ENet object}.recv_bbuf {BBuf onject}[,{waiting time}][,{address on timeout}]`


### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Misc.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>BBuf object</td>
      <td>
        BBuf object to store the received binary data
      </td>
      <td></td>
    </tr>
    <tr>
      <td>waiting time</td>
      <td>
        timeout. If elapsed, proceed to the next command or jump to the address on timeout.<br>
        If not specified, wait ininfinitely.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>address on timeout</td>
      <td>
        address to which jump on timeout.<br>
        If not specified, proceed to next command.
      </td>
      <td>address</td>
    </tr>
  </tbody>
</table>


### Return value

The number of received data.


### Example

```python
var bbuf=enet_to_sensor.BBuf()
enet_to_sensor.recv bbuf
enet_to_sensor.recv bbuf, 5000
var nitem=enet_to_sensor.recv(bbuf,5000,*TimeOut)
end

*TimeOut
print "Time out! No response from sensor"
end
```


[__SOURCE](7-enet-module/3-enet/3-enet-member-func/enet-send.md)
# send

### Description

Send string data to ethernet object.


### Syntax

`{ENet object}.send {msg}`



### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Misc.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">msg</td>
      <td style="text-align:left">
        string to send
      </td>
      <td style="text-align:left">string</td>
    </tr>
  </tbody>
</table>


### Return value

The number of bytes sent.


### Example

```python
enet_to_sensor.send "rob:"+10+", command:"+cmd+"\n"
```




[__SOURCE](7-enet-module/3-enet/3-enet-member-func/enet-send_bbuf.md)
# send_bbuf

### Description

Send [BBuf](../../4-bbuf/README.md) object to ethernet object.


### Syntax

`{ENet object}.send_bbuf {BBuf object}`


### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Misc.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">BBuf object</td>
      <td style="text-align:left">
        binary buffer object to send.
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>


### Return value

The number of bytes sent.


### Example

```python
var bbuf=enet.BBuf()
var arr=[ -3, 0, 1 ]
bbuf.append("s4", arr)
var nitem=cli.send_bbuf(bbuf)
```

[__SOURCE](7-enet-module/3-enet/3-enet-member-func/enet-set_send_trail_null.md)
# set_send_trail_null


### Description

When sending a string with the `ENet.send()` function, it sets whether to send it with a terminating-null character attached. (default is false)


### Syntax

`{ENet object}.set_send_trail_null(true|false)`


### Return value

None.


### Example

```python
enet_to_sensor.set_send_trail_null(true)
enet_to_sensor.send "ACK"
enet_to_sensor.set_send_trail_null(false)
```

[__SOURCE](7-enet-module/3-enet/3-enet-member-func/enet-state.md)
# state

### Description

Returns the state of the ethernet object.


### Syntax

`{ENet object}.state`


### Return value

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Misc.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>
        Connected. <br>
        (In case of UDP, even just an `open` is considered connected.<br>
         In the case of TCP, it is considered connected only when `listen`, `connect`, and `accept` are performed after `open`.
      </td>
      <td></td>
    </tr>
    <tr>
      <td>0</td>
      <td>Disconnected.</td>
      <td></td>
    </tr>
    <tr>
      <td>-1</td>
      <td>Failed in creating ethernet socket.</td>
      <td></td>
    </tr>
    <tr>
      <td>-2</td>
      <td>Failed in binding ethernet socket.</td>
      <td></td>
    </tr>
    <tr>
      <td>-3</td>
      <td>Failed to connect.</td>
      <td></td>
    </tr>
    <tr>
      <td>-4</td>
      <td>Failed to listen.</td>
      <td></td>
    </tr>
    <tr>
      <td>-5</td>
      <td>Failed to accept.</td>
      <td></td>
    </tr>
  </tbody>
</table>


### Example

```python
var ret = enet_to_sensor.state()
```


[__SOURCE](7-enet-module/4-bbuf/README.md)
# 7.4 BBuf object

A BBuf (Binary Buffer) object encapsulates binary data to be sent and received over Ethernet communication.
For usage, see the binary communication examples.

[7.1.2 peer-to-peer, client example - binary transmission](7-enet-module/1-exam-client/2-enet-client-bin.md)

[7.2.2 ethernet TCP server - binary transmission](7-enet-module/2-exam-server/2-enet-server-bin.md)

[__SOURCE](7-enet-module/4-bbuf/1-bbuf-creator.md)
# 7.4.1 BBuf creator

### Description

Create binary buffer object. Returns the reference of the created object.

### Syntax

`BBuf()`


### Return value

Reference of the created object.

### Example

```python
var bbuf = BBuf()
```

[__SOURCE](7-enet-module/4-bbuf/2-format.md)
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
[__SOURCE](7-enet-module/4-bbuf/3-bbuf-member-func/README.md)
# 7.4.2 BBuf member function


[__SOURCE](7-enet-module/4-bbuf/3-bbuf-member-func/bbuf-append.md)
# append

### Description

Appends data in the specified format to a binary buffer.


### Syntax

`{BBuf object}.append {format},{data}`


### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Misc.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">format</td>
      <td style="text-align:left">binary format<sup>*</sup><br>
      e.g. "U4", "s2"
      </td>
      <td style="text-align:left">string</td>
    </tr>
	 <tr>
      <td style="text-align:left">data</td>
      <td style="text-align:left">
        data to append in binary buffer
      </td>
      <td style="text-align:left">primitive data,<br>or 1-D array of primitive data</td>
    </tr>
  </tbody>
</table>

<br>


* See [7.4.2 Supported format](../2-format.md).
* If data of a different type from the specified format, automatic type casting is performed implicitly. For example, if the format is "s2" (2-byte integer) and the data is a float value of 3.7, the integer value 3(0x0003) is appended to the buffer.
Conversely, if format is "f4" (4-byte real number) and data is an integer value of -3, the real value -3.0(0xC0400000) is stored in the buffer.
* If the format is unsigned and the data is a negative number, an error occurs, so be careful.

<br>


### Return value

The number of data appended.


### Example

```python
var bbuf=enet.BBuf()
bbuf.append("F8", 9.80665)
bbuf.append("U4", [2, 3, 5, 7, 11, 13])
```

[__SOURCE](7-enet-module/4-bbuf/3-bbuf-member-func/bbuf-clear.md)
# clear

### Description

Delete all data stored in the binary buffer.


### Syntax

`{BBuf object}.clear()`


### Parameters

None


### Example

```python
var bbuf=enet.BBuf()
bbuf.append("s4", 20)
bbuf.append("s4", -10)
bbuf.clear()
```

[__SOURCE](7-enet-module/4-bbuf/3-bbuf-member-func/bbuf-nbyte.md)
# nbyte

### Syntax

`{BBuf object}.nbyte`


### Return value

The number of bytes of binary data


### Example

```python
var bbuf=enet.BBuf()
bbuf.append("s4", 20)
bbuf.append("s4", -10)
print bbuf.nbyte() # "8"
```

[__SOURCE](7-enet-module/4-bbuf/3-bbuf-member-func/bbuf-read_num.md)
# read_num

### Description

Reads a numeric value from a specified position in the binary buffer, and returns it.


### Syntax

`{BBuf object}.read_num {format},{offset}`


### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Misc.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">format</td>
      <td style="text-align:left">binary data format<sup>*</sup><br>
      e.g. "U4", "s2"<br>
      </td>
      <td style="text-align:left">string</td>
    </tr>
	 <tr>
      <td style="text-align:left">offset</td>
      <td style="text-align:left">
        position at which to read the data (0-based byte offset)
      </td>
      <td style="text-align:left">integer</td>
    </tr>
  </tbody>
</table>

<br>

\* Refer to [7.4.2 Supported format](../2-format.md).
<br>
<br>

### Return value

* Numeric value read
* If an error occurs when reading the data type, it returns 0.


### Example

```python
var bbuf=enet.BBuf()
bbuf.append("F8", 9.80665)
bbuf.append("U4", [2, 3, 5, 7, 11, 13])
print bbuf.read_num("F8", 0) # "9.80665"
print bbuf.read_num("U4", 12) # "3"
print bbuf.read_num("U4", 16) # "5"
```

[__SOURCE](7-enet-module/4-bbuf/3-bbuf-member-func/bbuf-read_nums.md)
# read_nums

### Description

Reads a specified number of numeric values from a specified position in the binary buffer and returns them in array format.


### Syntax

`{BBuf object}.read_num  {format},{offset},{n.item}`


### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Misc.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">format</td>
      <td style="text-align:left">
			binary data format<sup>*</sup><br>
      e.g. "U4", "s2"
      </td>
      <td style="text-align:left">string</td>
    </tr>
	  <tr>
      <td style="text-align:left">offset</td>
      <td style="text-align:left">
        position at which to read the data (0-based byte offset)
      </td>
      <td style="text-align:left">integer</td>
    </tr>
    <tr>
      <td style="text-align:left">n.item</td>
      <td style="text-align:left">
        the number of data to read
      </td>
      <td style="text-align:left">integer</td>
    </tr>
  </tbody>
</table>

<br>


\* Refer to [7.4.2 Supported format](../2-format.md).
<br>
<br>


### Return value

* Array of numeric values read.
* If the number of data in the buffer is less than the specified number, only reads as many as there are.
* Returns an empty array if an error occurs when reading the data type.


### Example

```python
var bbuf=enet.BBuf()
bbuf.append("F8", 9.80665)
bbuf.append("U4", [2, 3, 5, 7, 11, 13])
print bbuf.read_nums("U4", 12, 3) # "[3, 5, 7]"
print bbuf.read_num("U4", 12, 6) # "[3, 5, 7, 11, 13]"
```

[__SOURCE](8-alias.md)
# 8. Alias

Alias is a name that can be used as an alternative to the notation of a variable or a property of an object.

Alias is an alternative name can be used to notate a variable or object. You can replace property notations that are too long to be repeated with concise names, or replace IO variables at specific indexes with more readable names.

An alias is defined with the **alias** statement, and the syntax is almost identical to that of **var** or **global**.

The scope of an alias is the same as global. That is, after the alias statement is executed, it can be used in any subsequent job, and is not destroyed even if the program cycle is reset by the end statement of the main program or the R0 \[ENTER\] operation.

```python
global myval=3, yourname="Jane"
val i=0,msg="hello"
val profile = { name: "Paul", age: 43, role: [ "CTO", "engineer" ] }

alias grip=fb3.do4, work_no=fb1.diw2 # (1)
alias role=profile.role # (2)
alias tool0=project.robot.tools.t_0 # (3)

# usage
grip=1
print work_no
print role[1]
tool0.mass=12
```

In (1) of the above example, the output variable **fb3.do4** was defined as an alias named **grip**, and the input variable **fb1.diw2** was defined as an alias **work_no**.  
In (2), the role array which is an property of **profile**, is defined as alias **role**.  
In (3), the built-in object **project.robot.tools.t_0** is defined as alias **tool0**, which points to tool-data \#0.

For an alias refer to an array, its element can be specified with [ ] operator, like **role[1]**.  
For an alias refer to an object, its property can be specified with . operator, like **tool0.mass**.

A constant cannot be defined as an alias. Define it using **global** or **var**.  
Expression cannot be defined as alias, either. Be careful as it may cause malfunction.


```python
#alias pie=3.141592 # (X)
#alias unit="mm/s" # (X)
global pie=3.141592 # (O)
global unit="mm/s" # (O)

#alias pie_2 = pie*pie # (X)
```

[__SOURCE](9-file/README.md)
# 9. File


[__SOURCE](9-file/1-file-system/README.md)
# 9.1 File System

In the MAIN module's file system of the ${cont_model} controller, instructions for creating, copying, and deleting directories and files are described.
[__SOURCE](9-file/1-file-system/1-mkdir.md)
# 9.1.1 mkdir

mkdir is the procedure making directory.

### Description

Creates a directory for the specified path in the MAIN module.

- You cannot create a directory on Teach Pendant or USB memory.
- If a directory with an intermediate path does not exist, it creates the intermediate path.

### Syntax

```python
mkdir <path>
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">path</td>
      <td style="text-align:left">
        The directory path to create.<br>
        Do not put / at the beginning.
      </td>
      <td style="text-align:left">string expression</td>
    </tr>
  </tbody>
</table>

### Sample

```python
mkdir "work/data1"
```

![](../../_assets/mkdir.png)

[__SOURCE](9-file/1-file-system/2-copyfile.md)
# 9.1.2 copyfile

A copyfile is a procedure that requests to copy a directory or file.

### Description

Copies a directory or file of specified source path to the specified destination pathname.

- Can only be performed within the MAIN module, not Teach Pendant or USB memory.
- If a directory of the intermediate path of the destination pathname does not exist, it creates the intermediate path.
- If the destination directory already exists, delete it and copy the source directory.
- Overwrite the destination file if it already exists.
- All subdirectories in the directory are also copied.
- The pathname also supports wildcard ('*', '?').

- Because large files or entire directories may be copied, it is asynchronously performed in the background to avoid loss of tact time due to waiting during copying. In other words, when the copyfile statement is performed, starting the copy in the background task, immediately proceed with the next statement. For example, you can request a copy and execute the move statements. The successful completion of the copy can be determined by reading the values of the result-variable. (That is, no errors or warnings are generated when the copy fails.)

- You cannot request another copy or deletion until one copy or deletion is complete.


### Syntax

```python
copyfile <result-variable>,<source pathname>,<destination pathname>
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">result-variable</td>
      <td style="text-align:left">
        result of background execution<br>
        <ul>
        <li>1: Successfully completed.</li>
        <li>0: Copy in progress.</li>
        <li>-1: Source pathname is invalid.</li>
        <li>-2: Destination pathname is invalid.</li>
        <li>-3: Failed to copy.</li>
        <li>-6: All failed when copying wildcard.</li>
        <li>-7: Some failed when copying wildcard.</li>
        <li>-11: Failed to create temporary path.</li>
        <li>-12: Failed to copy to temporary path.</li>
        <li>-13: Failed to clear existing destination path.</li>
        <li>-14: Destination path creation failed.</li>
        <li>-15: Move from temporary path to destination path failed.</li>
        </ul>
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">source pathname</td>
      <td style="text-align:left">
        directory's path to copy,<br>
        or file's pathname to copy
      </td>
      <td style="text-align:left">string expression</td>
    </tr>
    <tr>
      <td style="text-align:left">string expression</td>
      <td style="text-align:left">
        - End with '/': Path to be copied.<br>
        - Not end with '/': Pathname that will be created by copying.
      </td>
      <td style="text-align:left">string expression</td>
    </tr>
  </tbody>
</table>

### Sample

```python
   var res
   copyfile res,"project/vars","work/vars_1" # vars_1/ folder is created.
   wait res==1,8,*timeout
   copyfile res,"project/vars","work/vars_1/" # vars_1/vars/ folder is created.
   wait res==1,8,*timeout
   copyfile res,"work/clear.job","project/jobs/0005_clear.job"
   wait res==1,4,*timeout
   copyfile res,"work/*_sub.job","project/jobs/" # wildcard
   wait res==1,4,*timeout
   call 5
   end
   *timeout
   print "copyfile failed"
   end
```

![](../../_assets/copyfile.png)


[__SOURCE](9-file/1-file-system/3-delfile.md)
# 9.1.3 delfile

A delfile is a procedure that requests to delete a directory or file.

### Description

Deletes a directory or file in the specified path.

- Can only be performed within the MAIN module, not Teach Pendant or USB memory.
- All subdirectories in the directory are also deleted.
- If the specified pathname does not exist, it ends with success.
- The pathname also supports wildcard ('*', '?').

- Because large files or entire directories may be deleted, it is asynchronously performed in the background to avoid loss of tact time due to waiting during deletion. The successful completion of the deletion can be determined by reading the values of the result-variable. (That is, no errors or warnings are generated when the deletion fails.)

- You cannot request another copy or deletion until one copy or deletion is complete.


### Syntax

```python
delfile <result-variable>,<pathname>
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">result-variable</td>
      <td style="text-align:left">
        result of background execution<br>
        <ul>
        <li>1: Successfully completed.</li>
        <li>0: Deletion in progress.</li>
        <li>-41: Failed to delete directory.</li>
        <li>-42: Failed to delete file.</li>
        </ul>
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">pathname</td>
      <td style="text-align:left">
        directory's path to delete,<br>
        or file's pathname to delete
      </td>
      <td style="text-align:left">string expression</td>
    </tr>
  </tbody>
</table>

### Sample

```python
   var res
   delfile res,"work/vars_1"
   wait res==1,8,*timeout
   delfile res,"work2/10??.job" # wildcard
   wait res==1,8,*timeout
   copyfile res,"project/jobs/0005_sub.job"
   wait res==1,4,*timeout
   end
   *timeout
   print "delfile failed"
   end
```

[__SOURCE](9-file/2-load-save/README.md)
# 9.2 Load/Save

Explains the statements that load/save files into/from the memory of the ${cont_model} controller's MAIN module.
[__SOURCE](9-file/2-load-save/1-load_job.md)
# 9.2.1 load_job

Statement that reads changes of the MAIN module's project/jobs/ folder to update the memory.


### Description

Load the jobs in the project/jobs/ folder of the MAIN module into new memory.

If you copy or overwrite .job files into the jobs/ folder with FTP or copyfile commands, you must perform this statement to reflect the memory to be able to select or call the job.

- CAUTION: Jobs in memory that do not exist in the jobs/ folder will be deleted.
- If the file has different modified time, it is loaded.
- Files that do not exist in memory are loaded.

- Since large capacity .jobs can be loaded, it is performed asynchronously in the background to avoid loss of tact time due to load. The successful completion of the load can be determined by reading the value of the resulting-variable.
- You cannot request another loading until current loading is finished.


### Syntax

```python
load_job <result-variable>,"*"
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">result-variable</td>
      <td style="text-align:left">
        result of background execution<br>
        <ul>
        <li>1: Successfully completed.</li>
        <li>0: Load in progress.</li>
        </ul>
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">job filename</td>
      <td style="text-align:left">
        You can only use the "*" argument, which means all files.
      </td>
      <td style="text-align:left">string expression</td>
    </tr>
  </tbody>
</table>

### Sample

```python
     var res
     copyfile res,"project/vars","work/vars_1"
     wait res==1,8,*timeout
     copyfile res,"work/sub5.job","project/jobs/0005_sub.job"
     wait res==1,4,*timeout
     load_job res,"*"
     wait res==1,4,*timeout
     call 5
     end
     *timeout
     print "copyfile failed"
     end
```

[__SOURCE](9-file/2-load-save/2-load_csv.md)
# 9.2.2 load_csv

Supported from V60.28-00.

Statement that reads to memory the changes to the .csv file (root global array) in the `project/vars/` folder of the MAIN module.

### Description

The global root arrays of HRScript is stored in the `vars/` folder as files in CSV standard format. ('Root' means that it is not a property of another array or object.)

For information on variable files, please refer to the operation manual link below.

[global variable/variable file](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-${cont_model}-tp630/6-monitoring/3-job/3-global-variable/3-var-files)

You can easily edit .csv files with a text editor on your PC.
The edited file copied to the `vars/` folder is not immediately reflected in memory, but only by using the `[load all]` function in the TeachPendant's global variable window or executing the `load_csv` statement.

- Because large .csv's can be loaded, they are performed asynchronously in the background to avoid loss of tact time due to loading. The successful loading can be determined by reading the value of the result-variable.
- You cannot request another loading until current loading is finished.


### Syntax

```python
load_csv <result-variable>,"*"
load_csv <result-variable>,"<variable name>"
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">result-variable</td>
      <td style="text-align:left">
        result of background execution<br>
        <ul>
        <li>1: Completed.</li>
        <li>0: Load in progress.</li>
        </ul>
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">.csv file title</td>
      <td style="text-align:left">
        <ul>
        <li>"*": loads all files.</li>
        <li>"&lt;variable name&gt;": Loads &lt;variable name&gt;.csv file.</li>
        </ul>
      </td>
      <td style="text-align:left">string expression</td>
    </tr>
  </tbody>
</table>

{% hint style="warning" %}
If you load all .csv with "*", the root arrays in memory that does not have .csv in the `vars/` folder are deleted.
{% endhint %}

### Sample

```python
     var res
     copyfile res,"work/arrs/locs1.csv","project/vars/locs.csv"
     wait res==1,4,*timeout
     load_csv res,"locs"
     wait res==1,4,*timeout
     call 5
     end
     *timeout
     print "failed to load new locations."
     end
```

[__SOURCE](9-file/2-load-save/3-save_csv.md)
# 9.2.3 save_csv

Supported from V60.28-00.

Statement that stores the global root array variable in memory as a .csv file in the `project/vars/` folder of the MAIN module.

### Description

The global root array of HRScript is stored in the `vars/` folder as a file in CSV standard format. ('Root' means that it is not a property of another array or object.)

For information on variable files, please refer to the operation manual link below.

[global variable/variable file](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-${cont_model}-tp630/6-monitoring/3-job/3-global-variable/3-var-files)

The global root arrays are not immediately stored to the .csv file whenever the value changes.
It is saved as a file when you press `Ctrl+[F7: save]` or power off, and you can save it as a file immediately by executing the `save_csv` command.

- Because large .csv's can be saved, they are performed asynchronously in the background to avoid loss of tact time due to saving. The successful saving can be determined by reading the value of the result-variable.
- You cannot request another saving until current saving is finished.


### Syntax

```python
save_csv <result-variable>,"*"
save_csv <result-variable>,"<variable name>"
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">result-variable</td>
      <td style="text-align:left">
        result of background execution<br>
        <ul>
        <li>1: Completed.</li>
        <li>0: Save in progress.</li>
        </ul>
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">.csv file title</td>
      <td style="text-align:left">
        <ul>
        <li>"*": saves all variable.</li>
        <li>"&lt;variable name&gt;": Saves &lt;variable name&gt;.csv file.</li>
        </ul>
      </td>
      <td style="text-align:left">string expression</td>
    </tr>
  </tbody>
</table>

{% hint style="warning" %}
If you save all .csv by specifying "*", it does not delete the .csv files in the `vars/` folder because the root variable of the corresponding name does not exist.
{% endhint %}

### Sample

```python
     var res
     save_csv res,"locs"
     wait res==1,4,*timeout
     copyfile res,"project/vars/locs.csv","work/arrs/locs2.csv"
     wait res==1,4,*timeout
     call 5
     end
     *timeout
     print "failed to save new locations."
     end
```

[__SOURCE](10-etc/README.md)
# 10. Etc.


[__SOURCE](10-etc/1-proc/README.md)
# 10.1 Etc. procedures


[__SOURCE](10-etc/1-proc/1-gather.md)
# 10.1.1 gather

`gather` is the procedure that specifies the start and end of the gathering when you use the data gathering function.

### Description

Specifies the start and end of gathering with `gather`. The gathering result file is saved as follows;
- Storage path: MAIN/project
- File name: 0001.GDT to 0030.GDT

Up to 30 gathering result files are stored, and if the number is exceeded, the previous collection result file is overwritten.

`gather_state()` function returns the current state of the data collection operation.
  - 0 : not in gathering.
  - 1 : in gathering. (gather 1 ~ gather 0)
  - 2 : saving the gathering results as a file. (gather 0~)

### Syntax

```python
gather <start/end>
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">start/end</td>
      <td style="text-align:left">
        <ul>
        <li>1: data gathering start</li>
        <li>0: data gathering end</li>
        </ul>
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
  </tbody>
</table>

### Sample

```python
S1   move L,spd=100%,accu=0,tool=0
     gather 1
S2   move L,spd=100%,accu=0,tool=0
     delay 1.5
S3   move L,spd=100%,accu=0,tool=0
     gather 0
     end
```
[__SOURCE](10-etc/1-proc/2-tonl.md)
# 10.1.2 tonl

`tonl` statement is the procedure for performing position correction for steps between start and end.

### Description

If you know the coordinate transformation relationship, this procedure is applied when you enter the transformation relationship without calculating a separate coordinate transformation relationship.

```python
R=[x,y,z,rx,ry,rz]
```

![](../../_assets/tonl2.png)

For the rotation matrix, it is applied in the order of Rot_z.Rot_y.Rot_x.

### Syntax

```python
tonl <start/end>,<shift>
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">start/end</td>
      <td style="text-align:left">
        online transformation start/end<br>
        <ul>
        <li>on: start</li>
        <li>off: end</li>
        </ul>
      </td>
      <td style="text-align:left">on/off</td>
    </tr>
    <tr>
      <td style="text-align:left">shift</td>
      <td style="text-align:left">
        Amount to shift
      </td>
      <td style="text-align:left">shift expression</td>
    </tr>
  </tbody>
</table>

### Sample

```python
   global sft
   enet1.recv msg # Receive shift amount via Ethernet
   sft=Shift(msg)
   tonl on,sft
   move L,spd=50mm/s,accu=0,tool=1
   move L,spd=10mm/s,accu=0,tool=1
   move L,spd=50mm/s,accu=0,tool=1
   tonl off
```

![](../../_assets/tonl.png)


[__SOURCE](10-etc/1-proc/3-seltool.md)
# 10.1.3 seltool

`seltool` is a procedure to change the tool number.

### Description

The tool is divided into a robot tool attached to the robot flange and a station tool installed separately from the robot, and `seltool` changes the tool number of each type.


### Syntax

```python
seltool <tool number>,<tool type>
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">tool number</td>
      <td style="text-align:left">
        tool number<br>
        <ul>
        <li>robot tool: 0 ~ 31</li>
        <li>station tool: 0 ~ 3</li>
        </ul>
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
    <tr>
      <td style="text-align:left">tool type</td>
      <td style="text-align:left">
        tool type to change tool number<br>
        <ul>
        <li>robot tool: robot</li>
        <li>station tool: station</li>
        </ul>
      </td>
      <td style="text-align:left">robot/station</td>
    </tr>
  </tbody>
</table>

### Sample

```python
   move P,spd=30%,accu=0,tool=1
   seltool 0,station
   move SP,spd=30%,accu=0,tool=1
   move SL,spd=30mm/s,accu=0,tool=1
   move SL,spd=30mm/s,accu=0,tool=1
   delay 0.5
   move P,spd=30%,accu=0,tool=1
   end
```

[__SOURCE](10-etc/1-proc/4-triggout.md)
# 10.1.4 triggout

`triggout` is a procedure that allows you to adjust the signal output time-point to be output-ahead (-) or output-behind (+).

### Description

In the interval of contpath 1, or 2 for continuous processing of commands, you can adjust the signal output time-point when the command position arrives at the target position (Accuracy OK) to be output-ahead (-) or output-behind (+).


### Syntax

```python
triggout <output variable>,val=<output value>,time=<ahead/behind time>
triggout <output variable>,val=<output value>,dist=<ahead/behind distance>,x=<X-direction absolute position>
triggout <output variable>,val=<output value>,dist=<ahead/behind distance>,y=<Y-direction absolute position>
triggout <output variable>,val=<output value>,dist=<ahead/behind distance>,z=<Z-direction absolute position>
triggout <output variable>,val=<output value>,dist=<ahead/behind distance>,j=<tcp or axis-direction relative distance>
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">output variable</td>
      <td style="text-align:left">
        Variable corresponding to output signal<br>
        <ul>
        <li>user output variable; do, dob, dow, dol, dof</li>
        <li>system output variable; so, sob, sow, sol, sof</li>
        </ul>
      </td>
      <td style="text-align:left">output variable</td>
    </tr>
    <tr>
      <td style="text-align:left">output value</td>
      <td style="text-align:left">
        When it is bit output(do, so), 0 is off, not 0 is on
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
    <tr>
      <td style="text-align:left">ahead/behind time</td>
      <td style="text-align:left">
        -10.00 ~ 2.00 [s]<br>
        If it is (-), the signal is output before the target position is reached; if it is (+), it is output after it is reached.
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
    <tr>
      <td style="text-align:left">ahead/behind distance</td>
      <td style="text-align:left">
        -3000 ~ 3000 [mm]<br>
        If it is (-), the signal is output before the target position is reached; if it is (+), it is output after it is reached.
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
    <tr>
      <td style="text-align:left">Absolute position in x, y, z direction</td>
      <td style="text-align:left">
        -3000 ~ 3000 [mm]
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
    <tr>
      <td style="text-align:left">tcp or axial relative distance<br>
      tcp : if j=0 then<br>
      axis-direction : if j=1 over then<br>
      </td>
      <td style="text-align:left">
        tcp : -3000 ~ 3000 [mm], axis-direction : -3000 ~ 3000 [mm] or [deg]<br>
        If it is (-), the signal is output before the relative distance is reached; if it is (+), it is output after it is reached.
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
  </tbody>
</table>

### Sample

```python
   move L,spd=300mm/s,accu=3,tool=1
   triggout do1,val=1,time=-0.5 #turn on do1 0.5 seconds before reaching the step
   triggout do1,val=1,dist=-100.0,j=0 #do1 turns on when tcp reaches step position and relative distance -100mm
   triggout do1,val=1,dist=-3.0,j=1 #do1 turns on when axis 1 reaches step position and relative distance -100mm
   triggout do1,val=1,x=-100.0 #do1 turns on when the X coordinate value reaches -100mm
   triggout do1,val=1,x=-100.0,y=-100.0 #do1 turns on when the X, Y coordinate value reaches -100mm
   move L,spd=30%,accu=2,tool=1
   end
```

{% hint style="warning" %}
* **The step that contains the `triggout` command** is used as the reference point, and the system checks whether a signal is output **up to the moment when the following step ends**.  
* If **no signal is output within that time frame**, the following warning is displayed:  
  **W0241: _"The triggout signal was not output within the step range."_**

{% endhint %}

[__SOURCE](10-etc/1-proc/5-intr_def.md)
# 10.1.5 intr_def

`intr_def` is a procedure that specifies interrupt condition, watch-interval, and program to run when an interrupt occurs.

### Syntax

An interrupt function is a type of program call. When the robot works in an interrupt watch-interval, it calls a specified job when it meets the predefined interrupt conditions. When the called-program finishes running, it returns to the previous running program's location and continues to run.


![](../../_assets/intr_def_1.png)


### Brief

- Operates only in interrupt watch intervals.
- Arithmetic expressions are supported as interrupt conditional expressions.
- Allow another interrupt handling (multiple interrupt) while performing an interrupt program.


### Timepoint when the interrupt is cleared

All defined interrupts are automatically cleared if the following actions occur.

- When performing 'R0: Task Reset'
- The first time the program runs
- When starting after changing the program counter (step/func #)


### Sample

```python
intr_def <on/off>,no=<interrupt number>,var=<interrupt condition>,val=<condition matching value>,job=<call program number>,[once]
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">on/off</td>
      <td style="text-align:left">
        Define interrupts or delete defined interrupts<br>
        <ul>
        <li>on: Defines a new interrupt.</li>
        <li>off: Deletes defined interrupt. (3rd and later parameters are ignored.)</li>
        </ul>
      </td>
      <td style="text-align:left">on/off</td>
    </tr>
    <tr>
      <td style="text-align:left">interrupt number</td>
      <td style="text-align:left">
        The interrupt number to define or delete.<br>
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
    <tr>
      <td style="text-align:left">interrupt condition</td>
      <td style="text-align:left">
        The conditional expression that will cause an interrupt.
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">condition matching value</td>
      <td style="text-align:left">
        The value of the conditional expression to generate interrupt.
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
    <tr>
      <td style="text-align:left">call program number</td>
      <td style="text-align:left">
        Program number to call when an interrupt occurs.
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
    <tr>
      <td style="text-align:left">[once]</td>
      <td style="text-align:left">
        handles only one interrupt in the interrupt watch interval without processing additional interrupts.
      </td>
      <td style="text-align:left">once</td>
    </tr>
  </tbody>
</table>


### Errors

- E1351 : Occurs when redefine an already-defined interrupt number without deletion. Please check the program that was created.


### Sample

```python
   intr_def on,no=1,var=di5,val=1,job=24,once # Defines interrupt
   move P,spd=30%,accu=3,tool=1
   move L,spd=30mm/s,accu=3,tool=1
   ...
   move L,spd=30mm/s,accu=3,tool=1
   move P,spd=30%,accu=3,tool=1
   intr_def off,no=1 # Deletes interrupt
   move P,spd=30%,accu=3,tool=1
   end
```

[__SOURCE](10-etc/1-proc/6-typeof.md)
# 10.1.6 typeof

`typeof` is the procedure for getting the type of a variable or an expression. The result is returned from the `result()` function.


### Syntax

```python
typeof <expression>
```


### Sample

```python
     global done=true,msg="Timeout Error"
     var a=-2000, b=3.14
     var myarr=[1,2,3]
     var myobj={x:30, y:"off"}
     var po=Pose(0,90,0,0,0,0)

     typeof done
     print result() # "bool" 
     typeof msg
     print result() # "string"
     typeof a
     print result() # "int"
     typeof b
     print result() # "double"
     typeof myarr
     print result() # "array"
     typeof myobj
     print result() # "object"
     typeof po
     print result() # "object"
     end
```

[__SOURCE](10-etc/1-proc/7-gasp_check.md)
# 10.1.7 gasp_check

The `gasp_check` statement estimates the pressure of the gas spring mounted on the robot and checks whether it is normal.

### Description

![](../../_assets/gasp_check.png)

- To estimate the pressure, the axis equipped with the gas spring is reciprocated by -20 degrees from its current position.(Recommended to be performed at the H-axis 140 degree position)
- You can monitor pressure by saving the estimated pressure as a variable.
- User can enter normal pressure and tolerance. If the estimated pressure exceeds the range, the set error output signal turns on.

### Syntax

```python
gasp_check pres=<estimated pressure>,ref=<reference pressure>,tol=<tolerance>
gasp_check pres=<estimated pressure>,ref=<reference pressure>,tol=<tolerance>,os=<error output signal>
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">estimated pressure</td>
      <td style="text-align:left">
         Variables in which the estimated gas spring pressure is stored[bar]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">normal pressure</td>
      <td style="text-align:left">
        Normal pressure to be the reference value for error occurrence[bar]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">tolerance</td>
      <td style="text-align:left">
        estimated pressure error tolerance[bar]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">error output signal</td>
      <td style="text-align:left">
        Signal output when an error occurs
      </td>
      <td style="text-align:left">output signal variable</td>
    </tr>
  </tbody>
</table>

### Errors
- E21011 : Occurs when the estimated gas spring pressure is below the minimum error criterion.
- E21012 : Occurs when the estimated gas spring pressure is higher than the maximum error reference.
- E21013 : Occurs on robots that do not support gas spring pressure inspection.


### Sample

```python
   var v0
   move P,spd=50%,accu=3,tool=1
   gasp_check pres=v0,ref=120,tol=20,os=do50    # Normal if the estimated pressure is 100 to 140 bar
   end
```
{% hint style="warning" %}
* Do not enter the operating area or touch the robot while the product is operating. There is a risk of injury.
{% endhint %}

{% hint style="info" %}
* Supported only on robots equipped with the gas spring
* For accurate estimation, [Axis add weight setting](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-${cont_model}-tp630/7-system/4-robot-parameter/7-axis-add-weight/README) and [Load estimation function](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-${cont_model}-tp630/7-system/7-auto-calibration/3-load-estimation) must be preceded before using the function.
* For a detailed description of the gas spring pressure check monitoring function, please refer to the link below.
[](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-${cont_model}-tp630/6-monitoring/4-system/2-system-diagnosis/2-gas-pressure-check)
* The estimated gas spring pressure may vary depending on the initial posture at the start of measurement.
During the robot's initial setup, please manage the pressure values based on the measurements taken at each reference posture, and regularly measure the pressure in the same posture to compare it with the initial values.
If a significant difference is observed in the measured values, please inspect the condition of the equipment.  

{% endhint %}


[__SOURCE](10-etc/1-proc/8-optime.md)
# 10.1.8 optime

The `optime` statement is a procedure used to start or update the measurement of operating time.

### Description

Normally, the measurement of operating time starts when the start button is pressed, and the operating time is automatically updated when the program executes `end`.  
However, if the program jumps back to the beginning using a `goto` statement without executing `end`, the operating time continues to increase. In this case, the monitored operating-time value becomes meaningless.

To address this situation, the `optime` statement allows the user to explicitly specify the points at which operating-time measurement starts and is updated.

### Syntax
```python
optime <parameter>
```
### Parameters
| Item      | Description                                                             | Remarks |
| --------- | ----------------------------------------------------------------------- | ------- |
| Parameter | - cycle_start: Start measurement<br>- cycle_end: Update measurement     |         |

```python
  *start
   optime cycle_start
   move P, spd=30%, accu=0, tool=1
   delay 0.5
   move P, spd=30%, accu=0, tool=1
   move L, spd=30mm/s, accu=0, tool=1
   move L, spd=30mm/s, accu=0, tool=1
   delay 0.5
   move P, spd=30%, accu=0, tool=1
   optime cycle_end
   goto *start
   end
```
[__SOURCE](10-etc/1-proc/9-count_up.md)
# 10.1.9 count_up

The `count_up` statement is a procedure that increments the value of a specified variable by 1, and resets it to the init value when it exceeds the preset value.

### Description

This statement increases the value of the specified variable by 1 each time it is executed.  
If the variable value exceeds the value specified by preset value, the variable is reset to the value specified by init value.

Executing  
```python
count_up cnt, init=0, preset=100`  
```
produces the same result as executing the following four lines:

```python
cnt = cnt + 1
if cnt > 100
    cnt = 0
endif
```

### Syntax
```python
count_up <variable>, init=<initial value>, preset=<final value>
```

### Parameters
| Item     | Description                                                              | Remarks |
| -------- | ------------------------------------------------------------------------ | ------- |
| Variable | The variable whose value will be incremented as a counter                |         |
| init     | The initial value to assign when the variable exceeds the preset value   |         |
| preset   | The maximum value of the variable                                        |         |

### Example
```python
   global work_no
   move P, spd=30%, accu=0, tool=1
   delay 0.5
   move P, spd=30%, accu=0, tool=1
   move L, spd=30mm/s, accu=0, tool=1
   move L, spd=30mm/s, accu=0, tool=1
   delay 0.5
   move P, spd=30%, accu=0, tool=1
   count_up work_no, init=0, preset=99
   end
```
[__SOURCE](10-etc/1-proc/10-count_dn.md)
# 10.1.10 count_dn Statement

The `count_dn` statement is a procedure that decrements the value of a specified variable by 1, and resets it to the init value when it becomes smaller than the preset value.

### Description

This statement decreases the value of the specified variable by 1 each time it is executed.  
If the variable value becomes less than the value specified by preset value, the variable is reset to the value specified by init value.

Executing  
```python
count_dn cnt, init=100, preset=0
```
produces the same result as executing the following four lines:

```python
cnt = cnt - 1
if cnt < 0
    cnt = 100
endif
```

### Syntax
```python
count_dn <variable>, init=<initial value>, preset=<final value>
```

### Parameters
| Item     | Description                                                                        | Remarks |
| -------- | ---------------------------------------------------------------------------------- | ------- |
| Variable | The variable whose value will be decremented as a counter                          |         |
| init     | The initial value to assign when the variable becomes less than the `preset` value |         |
| preset   | The minimum value of the variable                                                  |         |


### Example
```python
   global work_no
   move P,spd=30%,accu=0,tool=1
   delay 0.5
   move P,spd=30%,accu=0,tool=1
   move L,spd=30mm/s,accu=0,tool=1
   move L,spd=30mm/s,accu=0,tool=1
   delay 0.5
   move P,spd=30%,accu=0,tool=1
   count_dn work_no,init=99,preset=0
   end
```

[__SOURCE](10-etc/1-proc/11-cycle_end.md)
# 10.1.11 cycle_end

The `cycle_end` statement is a procedure that clears all call stacks that are being managed as a result of executing `call` statements.

### Description

When a program executes the `end` statement while a call stack exists, program execution returns to the position where the `call` statement was executed and continues running.  
However, when the `cycle_end` statement is executed, all managed call stacks are cleared. As a result, the program does not return to the position of the `call` statement and instead stops execution.

### Syntax

```python
cycle_end
```

### Example

```python
   0001.job
   ...
   move P,spd=30%,accu=0,tool=1
   call 10
   move P,spd=30%,accu=0,tool=1
   move L,spd=30mm/s,accu=0,tool=1
   move L,spd=30mm/s,accu=0,tool=1
   delay 0.5
   move P,spd=30%,accu=0,tool=1
   end


   0010.job
   ...
   move P,spd=30%,accu=0,tool=1
   delay 0.5
   cycle_end


```

[__SOURCE](10-etc/1-proc/12-speed_out.md)
# 10.1.12 speed_out Statement

The `speed_out` statement is a procedure that calculates a value proportional to the robot's current movement speed and assigns the result to a specified variable.  
It operates only while executing a `move` statement with interpolation set to `L` or `C`.

### Description

This statement calculates a value proportional to the robot's current moving speed and stores the calculated result in the specified variable.  

If the following command is executed, as shown in the figure, the value **y** corresponding to the current robot speed **x** is calculated and assigned to dow10.
...  
speed_out on,min_spd=100,max_spd=2000,min_val=10,max_val=100,var=dow10  

![](../../_assets/speed_out.png)

### Syntax
```python
speed_out <on/off>, min_spd=<minimum speed>, max_spd=<maximum speed>, min_val=<minimum value>, max_val=<maximum value>, var=<numeric variable>
```

### Parameters
| Item    | Description                                                    | Remarks          |
| ------- | -------------------------------------------------------------- | ---------------- |
| on/off  | Specifies the section in which the function is enabled         |                  |
| min_spd | Specifies the minimum robot movement speed [mm/s]              |                  |
| max_spd | Specifies the maximum robot movement speed [mm/s]              |                  |
| min_val | Specifies the value corresponding to the minimum robot speed   |                  |
| max_val | Specifies the value corresponding to the maximum robot speed   |                  |
| var     | Specifies the variable in which the calculated value is stored | Numeric variable |

### Example

```python
   move P,spd=30%,accu=0,tool=1
   speed_out on,min_spd=100,max_spd=2000,min_val=10,max_val=100,var=dow10
   move L,spd=30mm/s,accu=0,tool=1
   move L,spd=30mm/s,accu=0,tool=1
   speed_out off
   move P,spd=30%,accu=0,tool=1
   end
```

[__SOURCE](10-etc/1-proc/13-task.md)
# 10.1.13 task Statement

The `task` statement is a procedure used to perform multitasking functions.  
For detailed information about the `task` statement, refer to the link below:  
[${cont_model} Controller Function Manual - Multitasking](https://hrbook-hrc.web.app/#/view/doc-multi-task/en/README)  

### Syntax

```python
task start, sub=<subtask number>, job=<program number>
task wait,  sub=<subtask number>
task sync,  id=<identifier>, no=<number of executions with the same id>
task stop,  sub=<subtask number>
task reset, sub=<subtask number>
```

[__SOURCE](10-etc/1-proc/14-toolchng.md)
# 10.1.14 toolchng

The `toolchng` statement is a procedure used to change the servo tool assigned to an additional axis.  
For detailed information about the `toolchng` statement, refer to the link below:  
[${cont_model} Robot Controller Function Manual - Servo Tool Change](https://hrbook-hrc.web.app/#/view/doc-svtool-change/en/README)

### Syntax

```python
toolchng on/off, tg=<change target>, di=<connection complete signal>, wait=<waiting time>
```
[__SOURCE](10-etc/1-proc/15-json_parse.md)
# 10.1.15 json_parse

Supported from V60.32-00

The `json_parse` procedure parses a JSON string to build an object, an array, or a value.

### Syntax

Right after the procedure starts, the `result()` function returns a result object used for checking the status and storing the result data.
```python
    json_parse <json string literal/value>
    var r = result()
```

You must wait for this procedure to complete.
```python
    wait r.status == "finished"
```

The result of parsing will be stored in `r.data`. An error may occur if the procedure is not allowed to finish before accessing the result.


##### status

<table>
  <thread>
    <th style="text-align:left">status</th>
    <th style="text-align:left">details</th>
  </thread>
  <tbody>
  <tr>
    <td style="text-align:left">parsing</td>
    <td style="text-align:left">The JSON string is still being parsed. The data cannot be used yet.</td>
  </tr>
  <tr>
    <td style="text-align:left">finished</td>
    <td style="text-align:left">JSON string parsing is complete. The data can now be used.</td>
  </tr>
  </tbody>
</table>



### Examples
```python
    json_parse "[1, 2, 3, 4]"
    var r = result()
    wait r.status == "finished", 10 # Wait for the process to complete, with a maximum timeout of 10 seconds.
    var jr = r.data   # The type of r.data is array
    print jr          # [1, 2, 3, 4] printed
```

```python
    json_parse "3.141592"
    var r = result()
    wait r.status == "finished", 10 # Wait for the process to complete, with a maximum timeout of 10 seconds.
    var jr = r.data    # The type of r.data is double
    print jr           # 3.141592 printed
```
```python
    json_parse "{\"test\": \"value\"}" # Double quotes must be escaped inside a JSON string.
    var r = result()
    wait r.status == "finished", 10 # Wait for the process to complete, with a maximum timeout of 10 seconds.
    var jr = r.data    # The type of r.data is JObject
    print jr           # { _type: "JObject", _sub_file: "", _desc: "", test: "value" } printed
```

[__SOURCE](10-etc/1-proc/16-brake_check.md)
# 10.1.16 brake_check

The `brake_check` statement is a procedure that applies torque to each axis motor to diagnose whether the brake is functioning correctly.

### Description

![](../../_assets/brake_check.png)

* **Hold test**  
  With the brake engaged, torque is applied to each axis for 3 seconds and the change in motor angle is checked to see if it is below the threshold.

* **Release test**  
  With the brake released, torque is applied to each axis for 3 seconds and the change in motor angle is checked to see if it is above the threshold.

### Syntax

```python
brake_check  
brake_check os=<error output signal> 
brake_check job=<return program>
brake_check os=<error output signal>,job=<return program>
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">Error output signal</td>
      <td style="text-align:left">
         Signal to be output when the angle change exceeds the threshold<br>
         - If specified, a warning occurs and the signal is output.<br>
         - If not specified, an error occurs.
      </td>
      <td style="text-align:left">Variable</td>
    </tr>
    <tr>
      <td style="text-align:left">Return program</td>
      <td style="text-align:left">
        Program number to execute when the angle change exceeds the threshold.
      </td>
      <td style="text-align:left">Variable</td>
    </tr>
  </tbody>
</table>

### Settings
When you touch the [Properties] button in the brake_check command, you will enter the brake diagnostic settings screen.  
![](../../_assets/brake_check_setting.png)

- **Mode**  
  Set whether to run threshold-setting mode or diagnostic mode.

- **Brake test items**  
  Set whether to perform Hold and Release tests for each axis.

- **Torque ratio (%)**  
  Set how much torque to apply for each axis.

- **Error detection threshold**  
  When running in diagnostic mode, set the threshold angle for error detection for each axis.  
  When running in threshold-setting mode, the values are set automatically.  
  Only editable with engineer-level privileges or higher.

### Error codes
- E1509: Occurs when the brake test is not completed within 6 seconds.
- E1510: Occurs when the brake does not release.
- E1525 ~ E1527: Occur when the return program is missing or its configuration differs.
- E1529: Occurs when the brake test cannot be performed because the robot is moving, running independently, etc.
- E1530: Occurs when execution of the brake test is delayed.
- E21005/W21005: Occur when the angle change during the Hold test is greater than the angle change during the Release test.

### Example

```python
   var v0
   move P,spd=50%,accu=3,tool=1
   brake_check os=do50,job=9000    # On error, output do50 and execute job program number 9000
   end
```

{% hint style="warning" %}
* Do not enter the operating area or touch the robot while the product is operating. There is a risk of injury.
{% endhint %}

{% hint style="info" %}
* Supported only on robots equipped with the gas spring
* For accurate estimation, [Axis add weight setting](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-${cont_model}-tp630/7-system/4-robot-parameter/7-axis-add-weight/README) and [Load estimation function](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-${cont_model}-tp630/7-system/7-auto-calibration/3-load-estimation) must be preceded before using the function.
* For a detailed description of the brake check monitoring function, please refer to the link below.
[](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-${cont_model}-tp630/6-monitoring/4-system/2-system-diagnosis/1-brake-check)
{% endhint %}
[__SOURCE](10-etc/2-func/README.md)
# 10.2 Etc. functions


[__SOURCE](10-etc/2-func/1-rducs.md)
# 10.2.1 rducs - user coordinate system

### Description

Function to read the generated user coordinate system as a pose.

- Copies the location/direction of the created user coordinate system to its pose value.
- If it is not created or the parameter is not valid, the job execution is interrupted with an error.


### Syntax

```python
<result variable> = rducs(<user coord. system number>,<pose variable>)
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">result variable</td>
      <td style="text-align:left">
        result of background execution<br>
        <ul>
        <li>0: Successfully completed.</li>
        </ul>
      </td>
      <td style="text-align:left">Variable</td>
    </tr>
    <tr>
      <td style="text-align:left">user coord. system number</td>
      <td style="text-align:left">
        Number of the user coordinate system to read
      </td>
      <td style="text-align:left">[1~20]</td>
    </tr>
    <tr>
      <td style="text-align:left">pose variable</td>
      <td style="text-align:left">
        Variable to get position/direction
      </td>
      <td style="text-align:left">pose variable</td>
    </tr>
  </tbody>
</table>

### Return value


<table>
  <thead>
    <tr>
      <th style="text-align:left">Value</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Etc.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>
        OK
      </td>
      <td></td>
    </tr>  
  </tbody>
</table>


### Errors

- E14613 : Occurs when the actual parameter does not match the formal parameter. Check the actual parameters.
- E14614 : Occurs when the user coordinate number is not a number. Please specify the user coordinate number again.
- E14615 : Occurs when the user coordinate number is not a number between 1 and 20. Please change the user coordinate number.
- E1336 : Occurs if it is an unregistered user coordinate number. Please change the user coordinate number.


### Sample

```python
   var p_uc2=Pose(0,0,0,0,0,0,"base")
   var res=rducs(2,p_uc2)
   end
```

![](../../_assets/rducs.png)


[__SOURCE](10-etc/2-func/2-segment.md)
# 10.2.2 segment

`segment` is the function that divides the distance between the start and end positions evenly.


### Description

Divides the distance between the start and end positions of the function factors evenly and stores the pose value considering the position and posture corresponding to the specified counter in the pose variable.
![](../../_assets/image_segment_1.png)

For example, if P3=segment(P1,P2,3,2), divide the distance between the P2 target positions from the P1 start position into 3 equal parts and store the pose value of the position and rotation of the 2nd pose in the P3 pose variable.

When you add the via position as a paramter of the function, the distance on the arc consisting of the start position, the via point, and the target position is evenly divided and the pose value of the position and rotation is stored in the pose variable.

![](../../_assets/image_segment_2.png)

For example, if P10=segment (P1,P2,P3,4,2),
The distance on the arc consisting of the P1 starting pose and P2 via pose P3 target pose is divided into 4 equal parts, and the pose value of the position and rotation of the specified 2nd pose is stored in the P10 pose variable.

<br>

### Syntax

```python
result=segment(<start pose>,<end pose>,<division number>,<counter>)
```

```python
result=segment(<start pose>,<via pose>,<end pose>,<division number>,<counter>)
```

### Return value

The result pose.

### Parameters
<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">start pose</td>
      <td style="text-align:left">
        start pose
      </td>
      <td style="text-align:left">pose expression</td>
    </tr>
    <tr>
      <td style="text-align:left">via pose</td>
      <td style="text-align:left">
        via pose
      <td style="text-align:left">pose expression</td>
    </tr>
    <tr>
      <td style="text-align:left">end pose</td>
      <td style="text-align:left">
        end pose
      </td>
      <td style="text-align:left">pose expression</td>
    </tr>
    <tr>
      <td style="text-align:left">division number</td>
      <td style="text-align:left">
        division number<br>
        (1 ~ 30000)
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
    <tr>
      <td style="text-align:left">counter</td>
      <td style="text-align:left">
        counter number of the pose to store<br>
        (0 ~ 300000, 0: start pose)
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
  </tbody>
</table>

### Sample

```python
     var po1,po2,po3
     po1=Pose(1000.000,0.000,1938.000,0.000,0.000,0.000) # start pose
     po2=Pose(2000.000,0.000,1938.000,0.000,0.000,0.000) # end pose
     po3=segment(po1,po2,4,2)
     end
```

```python
     var po1,po2,po3,po10
     po1=Pose(1000.000,0.000,1938.000,0.000,0.000,0.000) # start pose
     po2=Pose(1500.000,500.000,1938.000,0.000,0.000,0.000) # via pose
     po3=Pose(2000.000,0.000,1938.000,0.000,0.000,0.000) # end pose
     po10=segment(po1,po2,po3,5,3)
     end
```


[__SOURCE](10-etc/2-func/3-intersection.md)
# 10.2.3 intersection

You can use the `intersection` function to find a point that meets a straight line at the shortest distance of one point, or to find an intersection with a straight line at the shortest distance that passes.

### Description

If you specify two points that form a straight line and another point as the parameters, you obtain a cross-pose of a straight line that connects the straight line and one point at the shortest distance.

![](../../_assets/image_intersection_1.png)

If you specify two points that form a straight line and two points that form another straight line as the parameters, you can find the intersection of the two straight lines at the shortest distance. The intersection point is the intersection with the first straight line you specify.

![](../../_assets/image_intersection_2.png)


### Syntax

```python
result=intersection(<straight-line ref.pose 1>,<straight-line ref.pose 2>,<position ref.pose>)
```

```python
result=intersection(<straight-line ref.pose 1>,<straight-line ref.pose 2>,<straight-line ref.pose 3>,<straight-line ref.pose 4>)
```

### Return value

The result pose.


### Parameters
<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">straight-line ref.pose 1</td>
      <td style="text-align:left">
        1st reference pose of 1st straight-line
      </td>
      <td style="text-align:left">pose expression</td>
    </tr>
    <tr>
      <td style="text-align:left">straight-line ref.pose 2</td>
      <td style="text-align:left">
        2nd reference pose of 1st straight-line
      <td style="text-align:left">pose expression</td>
    </tr>
    <tr>
      <td style="text-align:left">position ref.pose</td>
      <td style="text-align:left">
        Pose referenced to find a straight line and shortest distance position
      </td>
      <td style="text-align:left">pose expression</td>
    </tr>
    <tr>
      <td style="text-align:left">straight-line ref.pose 3</td>
      <td style="text-align:left">
        1st reference pose of 2nd straight-line
      </td>
      <td style="text-align:left">pose expression</td>
    </tr>
    <tr>
      <td style="text-align:left">straight-line ref.pose 4</td>
      <td style="text-align:left">
        2st reference pose of 2nd straight-line
      </td>
      <td style="text-align:left">pose expression</td>
    </tr>
  </tbody>
</table>

### Sample

```python
     var po1,po2,po3,result
     po1=Pose(1000.000,0.000,1938.000,0.000,0.000,0.000)
     po2=Pose(2000.000,0.000,1938.000,0.000,0.000,0.000)
     po3=Pose(2500.000,500.000,1938.000,0.000,0.000,0.000)
     result=intersection(po1,po2,po3)
     end
```

```python
     var po1,po2,po3,po4,result
     po1=Pose(1000.000,0.000,1938.000,0.000,0.000,0.000)
     po2=Pose(1500.000,500.000,1938.000,0.000,0.000,0.000)
     po3=Pose(2000.000,0.000,2000.000,0.000,0.000,0.000)
     po4=Pose(2000.000,0.000,2000.000,0.000,0.000,0.000)
     result=intersection(po1,po2,po3,po4)
     end
```


[__SOURCE](10-etc/2-func/4-rand.md)
# 10.2.4 rand

You can generate random numbers using the rand function.

### Description
Depending on the function's arguments, it generates a random real number between 0 and 1 or a random integer number within a specified range.

### Syntax
```python
# random real number between 0 and 1
v0=rand() 
```

```python
# random integer number within a specified range
v1=rand(<minimum value>,<maximum value>) 
```

### Parameters
<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">minimum value</td>
      <td style="text-align:left">
        minimum random integer number to generate
      </td>
      <td style="text-align:left">integer constant</td>
    </tr>
    <tr>
      <td style="text-align:left">maximum value</td>
      <td style="text-align:left">
        maximum random integer number to generate
      <td style="text-align:left">integer constant</td>
    </tr>
  </tbody>
</table>

### Sample

```python
     var v0, v1
     var min=1
     var max=100
     v0=rand()          # generate random real number between 0 and 1
     v1=rand(min,max)   # generate random integer number between 1 and 100
     end
```


[__SOURCE](10-etc/2-func/5-sig2int.md)
# 10.2.5 sig2int

Using the sig2int function, a specific range of input/output signals can be expressed as an int type value.

### Description
- Enter the name of the input/output signal to be expressed in int type.
- Set how many bits to read from input/output signals.

### Syntax

```python
result=sig2int(<input/output signal>,<number of bits>)
```

### Parameters
<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">input/output signal</td>
      <td style="text-align:left">
        input/output signal variable name
      </td>
      <td style="text-align:left">input/output signal variable</td>
    </tr>
    <tr>
      <td style="text-align:left">number of bits</td>
      <td style="text-align:left">
        Number of bits to read from input/output signals
      <td style="text-align:left">variable</td>
    </tr>
  </tbody>
</table>

### Sample

```python
     var result1,result2,result3
     result1=sig2int(di4,4)
     result2=sig2int(fb2.do0,1)
     result3=sig2int(fn1.di24,8)
     end
```


[__SOURCE](10-etc/3-sysvar/README.md)
# 10.3 System variables

[__SOURCE](10-etc/3-sysvar/_acc_rate.md)
# _acc_rate

Get or set the rate of acceleration in the speed-profile.

### Description

- unit : %
- range : 1 to 100
- default value : 100

### Syntax

```python
var res
res = _acc_rate
```

### Sample

```python
   ...
   # Print current accel-rate, and set to 70%.
   print _acc_rate
   _acc_rate=70
   ...
   end
```

[__SOURCE](10-etc/3-sysvar/_dec_rate.md)
# _dec_rate

Get or set the rate of deceleration in the speed-profile.

### Description

- unit : %
- range : 1 to 100
- default value : 100

### Syntax

```python
var res
res = _dec_rate
```

### Sample

```python
   ...
   # Print current decel-rate, and set to 70%.
   print _dec_rate
   _dec_rate=70
   ...
   end
```

[__SOURCE](10-etc/3-sysvar/_intr_no.md)
# _intr.no

`_intr.no` system variable is the occured interrupt number.

### Description

When an interrupt occurs because the conditional expression in the `intr_def` procedure is satisfied, you can use `_intr.no` to determine by which interrupt number the program is called.


### Syntax

```python
var res
res = _intr.no
```


### Sample

```python
   ...
   if _intr.no==1  # If interrupt number 1 occures
   print "By sensor 1 activation, interrupt occures."
   else if _intr.no==2 # If interrupt number 2 occures
   print "By sensor 2 activation, interrupt occures."
   stop # robot stops
   endif
   ...
   end
```



[__SOURCE](10-etc/3-sysvar/_intr_target.md)
# _intr.target

`_intr.target` system variable adjusts the robot's target position reach state.


### Description

In the move statement, this is used to adjust the position when the an interrupt occurs while moving and returns to the position of the previous program after the execution of the call program ends.


### Syntax

```python
_intr_target=1
```

### Sample

```python
- _intr.target=-1
```

![](../../_assets/intr_target_1.png)


```python
- _intr.target=1 or 0
```
![](../../_assets/intr_target_2.png)


[__SOURCE](10-etc/3-sysvar/_spd_rate.md)
# _spd_rate

Get or set the playback speed-rate.

### Description

Same setting as cond.set - Playback speed rate.

- unit : %
- range : 1 to 100
- default value : 100

### Syntax

```python
var res
res = _spd_rate
```

### Sample

```python
   ...
   # If playback speed is less than 50%, raise it to 100%.
   if _spd_rate<50
     _spd_rate=100
   ...
   end
```

[__SOURCE](10-etc/3-sysvar/_task_enable.md)
# _task.enable

### Description

A system variable to determine whether a subtask is active.


### Syntax

```python
var res
res = _task[1].enable
```


### Sample

```python
   ...
   if _task[1].enable==1  # If subtask 1 is active
   print "Subtask 1 is active"
   endif
   ...
   end
```



[__SOURCE](10-etc/3-sysvar/_tool.md)
# _tool

`_tool` is a system variable for reading or changing tool data.


### Description

- Read the registered tool data (weight/center of mass/inertia) or change the tool data.
- If the tool data is not registered or if the member is not valid, an error occurs and the job execution is interrupted.


### Syntax

```python
<shift variable> = _tool3
_tool3 = <shift>
_tool[3] = <shift>
_tool[5].mass = <arithmetic expression>
_tool[5].cx = <arithmetic expression>
_tool[5].cy = <arithmetic expression>
_tool[5].cz = <arithmetic expression>
_tool[5].ixx = <arithmetic expression>
_tool[5].iyy = <arithmetic expression>
_tool[5].izz = <arithmetic expression>
```


### Errors

- E14550 : Occurs when the member of the tool data is not valid. Make sure that the members of the set tool data are mass, cx, cy, cz, ixx, iyy, izz.
- E14286 : Occurs when the right side of the assignment statement is not a shift type or when the member of the tool variable is not valid. Please specify the right side correctly.


### Sample

```python
   var sft=Shift(100,20,30,0,0,0,"tool")
   _tool3=sft
   move L,spd=30%,accu=1,tool=3
   end
```

[__SOURCE](10-etc/3-sysvar/_vel_rpm_cmd.md)
# _vel_rpm_cmd

Reads or sets the speed at which the motor rotates when controlling speed for an additional axis.

### Description

The additional axis must be set to speed control mode on the jig axis.<br>
The unit is rpm. You can set a value between -10000 and 10000, and the default value is 0. <br>
If specified as -, the motor rotates in reverse.

### Syntax

```python
var res
_vel_rpm_cmd[6] = 1000 # Rotate the 7-axis motor at 1000 rpm 
res = _vel_rpm_cmd[6] # Assign the rotation speed of the 7-axis motor 
```

### Sample

```python
   ...
   # After print the current 7-axis motor rotation speed, set it to 1000 rpm.
   print _vel_rpm_cmd[6]
   _vel_rpm_cmd[6]=1000
   ...
   end
```

[__SOURCE](10-etc/3-sysvar/_weaving.md)
# _weaving

### Description

_weaving is used to change the currently selected weaving conditions.

### Syntax

```python
_weaving.frequency=2
_weaving.angle=5
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">item</th>
      <th style="text-align:left">meanings</th>
      <th style="text-align:left">etc</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">weave</td>
      <td style="text-align:left">
         Weaving type (0=single vibration, 1=triangle, 2=L-shaped, 3=circular)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">frequency</td>
      <td style="text-align:left">
        Frequency[Hz]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">left_distance</td>
      <td style="text-align:left">
        Distance towards left[mm]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">right_distance</td>
      <td style="text-align:left">
        Distance towards right[mm]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">angle</td>
      <td style="text-align:left">
        Angle[deg]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">offset_angle</td>
      <td style="text-align:left">
        Offset angle[deg]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">wall_direction</td>
      <td style="text-align:left">
        Wall direction (0=vertical, 1=horizontal, 2=torch orientation)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">forward_angle</td>
      <td style="text-align:left">
        Forward angle[deg]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">boundary_limit</td>
      <td style="text-align:left">
        Boundary limit (0=valid, 1=invalid)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">segment_time_1</td>
      <td style="text-align:left">
        Segment (1~4) moving time[s]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">segment_delay_1</td>
      <td style="text-align:left">
        Segment (1~4) timer(weaving stop)[s]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">height_sensing_mode</td>
      <td style="text-align:left">
        Height sensing mode (0=current change, 1=left fixed, 2=right fixed)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">side_sensing_mode</td>
      <td style="text-align:left">
        Left/Right sensing mode (0=Center, 1=Left, 2=Right)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">asymetric_sensing_ratio</td>
      <td style="text-align:left">
        Asymmetric sensing ratio (-50~50) [%]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">side_sensing_sensitivity</td>
      <td style="text-align:left">
        Left and right sensing sensitivity (0~10)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">height_sensing_sensitivity</td>
      <td style="text-align:left">
        Height sensing sensitivity (0~10)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
  </tbody>
</table>




### Sample

```python
   weaving on,cnd=1
   move P,spd=50%,accu=3,tool=1
   _weaving.frequency=5    # Change the weaving frequency to 5Hz
   move P,spd=50%,accu=3,tool=1
   weaving off
   end
```


[__SOURCE](10-etc/3-sysvar/_pc.md)
# _pc

### Description

_Pc is used to obtain current program counter information. <br>
The program counter consists of a program number, a step number, and a function number.

### Syntax

```python
var sno=_pc.cur_sno  # Assign the current step number
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">item</th>
      <th style="text-align:left">meaning</th>
      <th style="text-align:left">etc</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">cur_sno</td>
      <td style="text-align:left">
         Step number where the cursor is currently located
      </td>
      <td style="text-align:left">variable</td>
    </tr>
  </tbody>
</table>




### cur_sno sample : If the until condition is not satisfied, move to the previous step.

```python
   S6 move P,spd=50%,accu=3,tool=1,until di6
      if (result()==0)
        goto S[_pc.cur_sno-1]
      endif
   S7 move P,spd=50%,accu=3,tool=1,until di7
      if (result()==0)
        goto S[_pc.cur_sno-1]
      endif
   S8 move P,spd=50%,accu=3,tool=1,until di8
      if (result()==0)
        goto S[_pc.cur_sno-1]
      endif
   ...
```

