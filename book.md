# Hi6 Robot Controller Function Manual - Robot Language HRScript

{% hint style="warning" %}
The information presented in this manual is the property of Hyundai Robotics.

The manual may neither be copied, in part or in full, nor redistributed without prior written consent from Hyundai Robotics.

It may neither be provided to any third party nor used for any other purposes.



Hyundai Robotics reserves the right to modify this document without prior notification.



**Copyright ⓒ 2020 by Hyundai Robotics**
{% endhint %}
# 1. Overview

  


# 1.1 Introduction of HRScript

Hyundai Robotics’ Hi6 Controller allows the user to program the robot’s tasks in a robot language called HRScript. Created programs can be saved as several files with the extension .job.

HRScript is a scripting language that will be interpreted and executed line by line by the interpreter without a compilation procedure. It is similar to the Python or JavaScript languages but has a simpler syntax.



# 2. Basic Syntax

Described in this section are the basic terms of HRScript. The basic concept of the job program could be understood by following the method for defining a variable, constructing a simple expression using operators, and assigning the resulting value to a variable.

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





# 2.2 Identifiers

Names must be given to commands, variables, functions, and labels that are described. These names are collectively referred to as “identifiers.” When deciding an identifier, it must comply with the following rules for the HRScript’s identifiers.

* It must consist only of uppercase and lowercase letters, numbers, and underscores.
* The first character must only be either a lowercase or uppercase letter or an underscore, not a number.
* It should not contain a space or tab.
* Identifiers already defined in the system, such as “if” and “for,” cannot be used.
* There is no limit to the length.

The following shows correct and incorrect examples of identifiers:

```text
myvar (O) 
myvar2 (O)
_myvar (O)
MyVar (O)
310a (X) – Started with a number
move (X) – An identifier already defined in the system
v300$ (X) – Used a symbol other than an underscore ($)
my var (X) – Included a space
```



# 2.3 Types of Statements

The four types of statements of HRScript are as follows:



* procedure
* assignment
* comment
* label



# 2.3.1 Procedures

A procedure consists of a command and a 0–N number of parameters.

```python
move P,po3,spd=80%,accu=1,tool=3 until do33
```

The three types of procedure parameters are as follows:

| Type | Syntax | Example |
| :--- | :--- | :--- |
| Position parameter | &lt;value&gt; | P, po3 |
| Keyword parameter | &lt;keyword&gt; = &lt;value&gt; | spd=80%, accu=1, tool=3 |
| Preposition parameter | &lt;preposition&gt;  &lt;value&gt; | until do33 |

The position parameter’s role is determined by its position, so it should not be moved and must always be at the front of the procedure. 

Keyword parameters should be placed after position parameters. However, the order between keyword parameters does not affect the operation.



The preposition parameters are placed last.





# 2.3.2 Assignment Statements

An assignment statement consists of the left side, the assignment operator \(=\), and the right side. The left side \(lvalue\) must be a variable that can store a value. No constants or expressions are allowed. 

On the other hand, constants, variables, and expressions are allowed on the right side \(rvalue\).



```python
height=(500+margin)/2
```

# 2.3.3 Comment Statements

A comment statement is used to describe the contents of the job program in a way that they can be understood easily. Even if the comment statement is executed, no operation is performed. As shown below, a description is attached after the hash sign \(\#\). It can be used as a single statement or attached after another statement.

```python
# robot has to wait sensor2 input
var work_w,work_h  # width and height of a workpiece
```



# 2.3.4 Labels

A label is used to mark the target point to move to according to the goto statement. It consists of an asterisk \(\*\) and an identifier.

# 2.4 First Program - Hello, World!

Let us create a simple job program that prints a string on the teach pendant screen. After creating a new job, record the print statement as shown below, and attach the string parameter "Hello, World!"

```python
print "Hello, World !"
```

The print statement is used to print the value at the bottom of the teach pendant's job panel. Now, when you run the program, you can see the text, "Hello, World!" printed at the bottom of the job panel.
# 2.5 Data Type

# 2.5.1 String Data Type

The first program in the previous paragraph used the data “Hello, World!” as the print statement’s parameter, a string data type. The value of the string data type begins and ends with double quotes. There is no limit for the length of the string.

```python
print "Welcome to the Robot World."
```

A sequence beginning with a backslash \(\\) represents double quotes or special characters in a string. This sequence is called the “escape character.”

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



# 2.5.4 Array Type and Object Type

In addition, there are array types and object types. These will be discussed in further detail in Sections 4.1 and 4.2.

# 2.6 Variables

A variable can store values and has an identifier name. Variables are divided into global and local variables, and the difference between them will be described later. Examples of local variables are first described here.



Variables can be created with the var command, as shown in the following. This is called defining a variable. Multiple identifiers can be created at once by enumerating multiple identifiers after the var command.



```python
var myvar
var width, height, depth
```

Storing a value in a variable is called “assignment.” The assignment may be performed while defining or after defining a variable. If the assignment is not performed while defining, the variable will have a number value of 0 by default.

```python
var myvar=0
var message, width=200
message="Invalid input value"
```

In HRScript, \(=\) does not mean equal. It is used as an assignment operator and means that the value on the operator’s right side is assigned to the variable on the left side. The value stored in the variable may be printed through the print statement.

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



# 2.7 Binary and Hexadecimal

All the number type values previously described as examples are interpreted as decimal numbers. It can represent binary or hexadecimal values just by adding 0b or 0x prefixes, respectively, as shown in the following.

```python
var binary = 0b10010011
var hexadecimal = 0xFF4A38C0
```

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

# 2.9 Functions

What is the process of converting the angle 60 to a radian value or finding the length of the string that the variable mystr contains? 

HRScript provides various functions that receive inputs through parameters, perform some processing, and return the result values. 

Functions can be used as part of an expression, as shown below.

```python
var dg=60, rd
rd=deg2rad(dg)

var limit=40, message="Input your code number"
var validity= len(message) < limit
```

The list of functions provided in HRScript is as follows. \(The tables are sorted in the ascending order of names.\)

# 2.9.1 Math Functions

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
      <td style="text-align:left">abs(<b>a</b>)</td>
      <td style="text-align:left">Returns the absolute value of <b>a</b>
      </td>
      <td style="text-align:left">abs(-300)</td>
      <td style="text-align:left">300</td>
    </tr>
    <tr>
      <td style="text-align:left">acos(<b>a</b>)</td>
      <td style="text-align:left">Returns the arc cosine value of <b>a</b> in radian format</td>
      <td style="text-align:left">acos(0.5)</td>
      <td style="text-align:left">1.0472</td>
    </tr>
    <tr>
      <td style="text-align:left">asin(<b>a</b>)</td>
      <td style="text-align:left">Returns the arc sine value of <b>a</b> in radian format</td>
      <td style="text-align:left">asin(0.5)</td>
      <td style="text-align:left">0.5236</td>
    </tr>
    <tr>
      <td style="text-align:left">atan(<b>a</b>)</td>
      <td style="text-align:left">Returns the arctangent value of <b>a</b> in radian format</td>
      <td style="text-align:left">atan(0.5)</td>
      <td style="text-align:left">0.4636</td>
    </tr>
    <tr>
      <td style="text-align:left">atan2(<b>a</b>, <b>b</b>)</td>
      <td style="text-align:left">Returns the arctangent value of a triangle with <b>a</b> for the y length
        and <b>b</b> for the x length in radian format</td>
      <td style="text-align:left">atan2(2,1)</td>
      <td style="text-align:left">1.1071</td>
    </tr>
    <tr>
      <td style="text-align:left">cos(<b>r</b>)</td>
      <td style="text-align:left">Returns the cosine value of <b>r</b> in radian format</td>
      <td style="text-align:left">cos(3.1415)</td>
      <td style="text-align:left">-1</td>
    </tr>
    <tr>
      <td style="text-align:left">deg2rad(<b>d</b>)</td>
      <td style="text-align:left">Returns the radian value of <b>d</b> in degree format</td>
      <td style="text-align:left">deg2rad(-90)</td>
      <td style="text-align:left">-1.570796</td>
    </tr>
    <tr>
      <td style="text-align:left">dist(<b>x</b>, <b>y</b>)</td>
      <td style="text-align:left">Returns the Euclidean distance from the origin to the (<b>x</b>, <b>y</b>)
        coordinate</td>
      <td style="text-align:left">dist(3.5,10)</td>
      <td style="text-align:left">10.59481</td>
    </tr>
    <tr>
      <td style="text-align:left">max(<b>a</b>, <b>b</b>)</td>
      <td style="text-align:left">Returns the greater value between <b>a</b> and <b>b</b>
      </td>
      <td style="text-align:left">max(-1.23, -3)</td>
      <td style="text-align:left">-1.23</td>
    </tr>
    <tr>
      <td style="text-align:left">min(<b>a</b>, <b>b</b>)</td>
      <td style="text-align:left">Returns the lesser value between <b>a</b> and <b>b</b>
      </td>
      <td style="text-align:left">max(-1.23, -3)</td>
      <td style="text-align:left">-3</td>
    </tr>
    <tr>
      <td style="text-align:left">near(<b>a</b>, <b>b</b> [,<b>e</b>])</td>
      <td style="text-align:left">Returns 1 if the difference between the real number values &#x200B;&#x200B;<b> a</b> and <b>b</b> is
        less than or equal to <b>e</b> and returns 0 if the difference is larger
        than <b>e</b>
      </td>
      <td style="text-align:left">
        <p>near(0.005, 0.0058)</p>
        <p>near(0.005, 0.006)</p>
        <p>near(0.005, 0.006, 0.1)</p>
      </td>
      <td style="text-align:left">
        <p>1</p>
        <p>0</p>
        <p>1</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">rad2deg(<b>r</b>)</td>
      <td style="text-align:left">Returns the degree value of <b>r</b> in radian format</td>
      <td style="text-align:left">rad2deg(1.570796)</td>
      <td style="text-align:left">90</td>
    </tr>
    <tr>
      <td style="text-align:left">sin(<b>r</b>)</td>
      <td style="text-align:left">Returns the sine value of <b>r</b> in radian format</td>
      <td style="text-align:left">sin(1.5*3.1415)</td>
      <td style="text-align:left">-1</td>
    </tr>
    <tr>
      <td style="text-align:left">sqr(<b>a</b>)</td>
      <td style="text-align:left">Returns the square root of <b>a</b>
      </td>
      <td style="text-align:left">
        <p>sqr(16)</p>
        <p>sqr(0)</p>
      </td>
      <td style="text-align:left">
        <p>4</p>
        <p>0</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">tan(<b>r</b>)</td>
      <td style="text-align:left">Returns the tangent value of <b>r</b> in radian format</td>
      <td style="text-align:left">tan(3.141592/4)</td>
      <td style="text-align:left">0.9999</td>
    </tr>
  </tbody>
</table>





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
        <p>Refer to &quot;<a href="../../array-object/array/">4.1 Arrays</a>&quot;.</p>
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
        <p>Refer to &quot;<a href="../../moving-robot/pose.md">5.1 Pose</a>&quot;.</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Pose object</td>
    </tr>
    <tr>
      <td style="text-align:left">Shift(element)</td>
      <td style="text-align:left">
        <p>Creates and returns a shift object</p>
        <p>Refer to &quot;<a href="../../moving-robot/shift.md">5.2 Shift</a>&quot;.</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Shift object</td>
    </tr>
  </tbody>
</table>



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
        <p>Returns the current pose of the robot to the &#x201C;crd&#x201D; coordinate
          system</p>
        <p>For values that can be used as &#x201C;crd&#x201D; elements, see the table
          under &quot;<a href="../../moving-robot/pose.md">5.1 Pose</a>&quot;.</p>
        <p>If the mode is &#x201C;cmd,&#x201D; it is the command value, and if the
          mode is &#x201C;cur,&#x201D; it is the current value.</p>
        <p>The &#x201C;crd&#x201D; and &#x201C;mode&#x201D; parameters may be omitted,
          and their default values are &#x201C;base&#x201D; and &#x201C;cur,&#x201D;
          respectively.</p>
      </td>
      <td style="text-align:left">cpo(&quot;joint&quot;, &quot;cmd&quot;)</td>
      <td style="text-align:left">Pose* that stores the command value of the robot to the axis coordinate
        system</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>mkucs(n,po)</p>
        <p>mkucs(n,po1,po2
          <br />,po3)</p>
      </td>
      <td style="text-align:left">
        <p>Creates and registers the nth user coordinate system object</p>
        <p>Refer to &quot;<a href="../../moving-robot/ucs.md">5.5 User Coordinate System (UCS)</a>&quot;.</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>0: OK</p>
        <p>&lt;0: Error code</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">result()</td>
      <td style="text-align:left">For some procedures, it may be necessary to check the results. If the
        result() function is called right after the procedure is executed, the
        execution result can be returned.</td>
      <td style="text-align:left">result()</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

\* Pose is a data type that represents the posture of the robot or the position of the tool tip. Details will be described later in "[5.1 Pose](../../moving-robot/pose.md)".

# 3. Flow-Control Statements and Sub-Program

The statements in the job program are executed line by line in top-to-bottom order. However, depending on certain conditions, the statements can be skipped without being executed, or certain statements can be executed repeatedly. Let us look at the control statements that can control the flow of the program in this manner. 

# 3.1 Address

Moving to another position in the program without executing the next line in order is called a “branch.”

The address is the destination of the branch.

There are two ways to define an address: line number and label. In the following example, “10” in the second statement is the line number, and the last statement “\*err\_handle” is the label.



```python
     move P,po3,spd=80%,accu=1,tool=3 until do33
10   z_pos = (base_height+offset)*1.05
     # robot has to wait sensor2 input
     *err_handle
```



# 3.2 Stop or Wait Statement

This statement can stop the execution of a program or make it wait for a certain period of time or until the conditions are satisfied.

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

# 3.3 Branch Statement

Makes it possible to go to a different address, without conditions.

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
        <p>Address to go to
          <br />
        </p>
        <p>An arithmetic expression is possible in the case of a line number.
          <br
          />
        </p>
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



# 3.4 Conditional Statements

These statements allow a certain operation to be or not to be executed depending on certain conditions.

# 3.4.1 Single-Line if

### Description

The form of a single-line if statement is as follows: If &lt;Boolean expression&gt; is true, branching to &lt;address&gt; will occur. If false, moving to the next statement will occur.

### Syntax

```python
if <bool expression> then <address>
```

### Example

Below is an example of the single-line if statement. If the condition that pressure is greater than the limit is true, branching to the label address “\*err will occur,” making it possible to print a warning that the pressure is too high. If the condition is false, the next statement will be executed one after the other without branching, so “In normal operation ” will be printed, ending the program.

```python
var pressure=95, limit=90
if pressure > limit then *err
print "in normal operation."
end
*err
print "warning: pressure is too high."
```

# 3.4.2 if-endif

### Description

If the single-line if statement is true, only the operation of branching to a specific address will occur. If executing other operations or multiple statements is necessary, the if-endif block should be used.

The form is as follows: If &lt;Boolean expression&gt; is true, the multiple number of &lt;statement&gt; between if and endif will be executed in order. If &lt;Boolean expression&gt; is false, skipping to the position after endif will occur without the &lt;statements&gt; being executed.

### Syntax

```python
if <bool expression>
	<statement>
	…
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

# 3.4.3 if-else-endif Statement

### Description

If the expression is false and if there are statements to be executed, the following form is used:

If the expression is true, statement A will be executed. If false, statement B will be executed.

### Syntax

```python
if <bool expression>
	<statement A>
	…
else
	<statement B>
	…
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



# 3.4.4. if-elseif-else-endif

### Description

In the case of multiple conditions, the elseif statement can be used in the following form.

### Syntax

```python
if <bool expression>
	<statement A>
	…
elseif <bool expression>
	<statement B>
	…
elseif <bool expression>
	<statement C>
	…
else
	<statement N>
	…
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
	…
	break
case <expression B1>
case <expression B2>
	<statement B>	… (1)
case <expression C>
	<statement C>	… (2)
	…
	break		… (3)
default
	<statement N>	… (4)
	…
	break		… (5)
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

# 3.5. Nested Flow-Control Statements

### Description

In the control statement block, another control statement block can be placed, as shown in the following example. In the following form, two nesting  levels are shown, but multiple nesting levels can be made as much as necessary.

### Syntax

```python
if <bool expression>
	if <bool expression>
		<statement A>
		…
	else
		<statement B>
		…
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



# 3.6 Loop Statements

Loop statements can be used when the same operation needs to be repeated multiple times.

# 3.6.1 for-next

### Description

The format of the for-next statement, which repeats the same operation, is as follows.

First, the initial value will be assigned to the index variable. When the next statement is encountered while the statements under the for statement are executed, the index variable will add increment/decrement values and perform repetition from the point of the for statement. When the index variable passes the end value, the repetition will end.

If a step is not specified, 1 will be applied.

### Syntax

```python
for <index variable>=<initial value> to <end value> [step <increment/decrement value>]
	<statement>
	…
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

# 3.7 Call, Jump Statement and Subprograms

If an entire large-scale robot operation is created as one job program, the program becomes large and complex, making it difficult to add functions or find and solve problems.

For the program’s maintainability, it is preferable to divide the unit operations that make up the entire program into subprograms. For example, when routines, such as a routine performs communication with a sensor, a routine that calculates the target position of the tool tip with the received data, and a routine that generates an appropriate message when an error occurs, are turned into individual subprograms and allow the main program to call them, it will be easier to grasp the overall structure of the program. It will also be useful to reuse divided subprograms in other projects.





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
param x,y
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

In job no. 1, the dist2d subprogram is called with the **call** statement, and "x, y," which are local variables, are passed. In the dist2d subprogram, "ldX", and "ldY" defined with the **param** statement are called "formal parameters", and "x, y" passed to the **call** statement are called "actual parameters."

The dist2d program transports resulting values to external destinations through **return** statements. Returned values can be obtained by calling a result\(\) function in the called program.

(A **return** statement and an **end** statement have the same action as they end a called program and return to the main program. However, a **return** statement is different from **end** statement as the former can designate a resulting value as an element).
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
# 3.8 Local Variables and Global Variables

## 

# 3.8.1 Local Variables

### Description

Examples have been described only using the examples of local variables defined with the var statement. Local variables are created by a var statement in one job program and are automatically destroyed when the program ends after the encounter with the end statement. Moreover, their values cannot be read or written by other programs. 

### Example

“main\_v” is a local variable accessible only within 0001.job, and “sub\_v” is a local variable accessible only within 0107.job.   Attempting to access it from another program will cause an error. 

The local variable “x” is defined in both 0001.job and 0107.job. The local variable “x” respectively defined in both programs has the same name but are different. So the value 5 for the variable “x” is set in subprogram 0107, 3 will be printed instead of 5 after the return to main program 0001.



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
        <p>x=x+1
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
        <p>x=x+1
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

# 4. Arrays and Objects

# 4.1 Arrays





# 4.1.1 Arrays

An array is a variable type that collects and stores several values under a single name and allows access through an index number.

Arrays are defined as **var** or **global**, like any other variable. Array definitions and access formats are as follows.

|  |  |
| :--- | :--- |
| Definition | var array name = \[ Value, Value, …\] |
| Access | Array name \[Index\] |

The values that make up an array are called “elements.” Distances, an array shown in the following example, has a total of five elements. The index starts from 0. Element 0 and e lement 1 of “distances” are 10 and 10.5, respectively.



The \[ \] operator is used as follows to read or write the value of an array’s specific element value. The following shows an example of an object that is defined and accessed.

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







# 4.1.2 Multidimensional Arrays

An array can also be nested as an element of an array. When accessing the elements of a multidimensional array, you can use the \[ \] operator consecutively. In the following example, “arr\_y” is a two-dimensional array. \(1\)

arr\_y\[1\] is an array of elements of index 1, namely \["abc", "jqk", "xyz"\], and it is assigned to the new variable “arr\_x.” \(2\)

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

# 4.1.3 Array Constructor Function

It is difficult to create an array with hundreds of elements with the notation \[ \] alone. Any number of arrays may be created by calling the constructor function. Each element will be initialized to 0.

```python
var name = Array(900)	# creates an array of 900 elements
```

If two or more elements are designated, a multidimensional array can be created. In the following example of a 3-dimensional array, \[4\] is the lowest dimension.

```python
var name = Array(3,2,4)	# [3][2][4] numbers of 3-dimensional arrays are created
# [ [[0,0,0,0], [0,0,0,0]], [[0,0,0,0], [0,0,0,0]], [[0,0,0,0], [0,0,0,0]] ]
```



# 4.2 Object

As previously seen, it was found that an array could store multiple element values and are accessed by index. 

Objects are like arrays in that they store multiple element values. The difference is that an object is accessed by a key, not with an index. Moreover, the key is a string, not a number. 

Objects are defined as var or global, like any other variables. The definition of an object and format of its access are as follows.

|  |  |
| :--- | :--- |
| Definition | var object name = { key : value, key : value, …} |
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



The object’s key must be in the format of an identifier, but the element’s value can be of any type and can also be of different types. 

An object can contain other objects or arrays as its elements. Likewise, an array can also contain other arrays or objects as its elements. In the following example, “work,” which is an object, contains “size,” which is an object, and “heights,” which is an array.

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



# 4.4 Call-by-reference and call-by-value

In the description of call statements and jump statements given in Section 3.4, the concepts of formal parameters and actual parameters were explained. When an actual parameter has been transported to a sub-program, if the sub-program ends after changing the value of the parameter, will it be reflected to the main program?

For example, let’s assume that a sub-program 0005\_pow3.job raises a value to the third power as follows:



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

Although we expected that 8 is output because 2×2×2 is 8, the result is 2. It is because, when a numeric-type actual parameter is transported to a sub-program, the value is copied as a parameter. In other words, in \(1\), because the value raised to the third power was assigned to the copied version, it did not affect the value of the original parameter, x.

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



# 5. Moving a Robotwith Robot Language

After understanding the pose that expresses the target position of the robot, let us learn about the commands to move the robot.

# 5.1 Pose

Pose is an object type embedded in the Hi6 Controller and represents each axis of the robot or the Cartesian coordinates and direction of the tool tip. 

Poses are created by calling the constructor function Pose\( \). All function parameters are position parameters. Meanwhile, crd and cfg are string types, and the rest are number types.

{% hint style="info" %}
The cfg element specifies the robot configuration. For more information, refer to "[2.3.2.2 Base and Robot Recording Coordinates](https://hrbook-asoe72.web.app/#/view/doc-hi6-operation/english/operation/step/step-pose-modify/base-robot-crd-sys)" in the Hi6 Robot Controller Operation Manual.
{% endhint %}



```python
var <pose variable name> = Pose(j1, j2, j3, …)					# axis coordinate
var <pose variable name> = Pose(x, y, z, rx, ry, rz, j7, j8,…, crd, cfg)		# base coordinate
```

Refer to the following examples of creating the poses for 6 axes + 1 additional axis and for Cartesian + 1 additional axis.

```python
var po1 = Pose(10, 90, 0, 0, -30, 0, -1240.8)				# axis coordinate
var po2 = Pose(1850, 0, 2010.5, 0, -90, 0, -1240.8, "base", "fl;r2")	# base coordinate
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

![](../_assets/image_9.png)

1. For V60.06-06 or older versions, fl is non-fl.

The pose element values can be accessed as shown in the following example.

```python
po1.j2 = po1.j2 + 5
print po2.z, po2.cfg
```



# 5.2 Shift

Shift is an object type embedded in the Hi6 Controller and represents the pose’s change value. 

Shifts are created by calling the constructor function Shift\( \). All function parameters are position parameters. Meanwhile, crd and cfg are string types, and the rest are number types.



```python
var <shift variable name> = Shift(j1, j2, j3, …)				# axis coordinate
var <shift variable name> = Shift(x, y, z, rx, ry, rz, j7, j8,…, crd)		# base coordinate
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

# 5.3 Pose Expression

The expression in which the result value becomes a pose is called a “pose expression.” 

All the following forms are recognized as poses.

```python
Pose
Pose+Shift
Pose-Shift
Pose+Shift+Shift+…
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

# 5.4 move

The move statement is a procedure for moving the robot. The format is as follows.

### Description

The robot’s tool tip moves to the pose position.

### Syntax

move &lt;interpolation&gt;, \[tg=&lt;pose/shift&gt;\], spd=&lt;speed&gt;, accu=&lt;accuracy&gt;

, tool=&lt;tool number&gt; \[until &lt;conditional expression&gt;\]

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
move P,tg=+Shift(0,0,0,0,-10,0),spd=80%,accu=1,tool=3 until di2  (hidden pose)
if result() then *sensor_on
```

If the \[Record\] button of the teach pendant is pressed, a move statement in hidden pose type will be recorded as the current robot position. The hidden pose value can be checked or edited by placing the cursor on the move statement and pressing the \[Property\] button. 

When the \[Command\] button is pressed and the \[Motion\] group is opened, select the move menu. As a result, a pose-type move statement is recorded.





# 5.5 User Coordinate System \(UCS\)

The user coordinate system is a coordinate system in which the user can set the position and direction.

It is created by calling the constructor function Ucs\( \). 



Function parameters are one pose or three poses. When calling is performed with one pose, the pose’s position and direction will be set as the origin and direction of the coordinate system. When calling is performed with three poses, the coordinate system will be created so that pose1 is positioned on the coordinate system’s origin, pose2 is on the x axis of the coordinate system, and pose3 is positioned on the XY plane of the coordinate system.



```python
var <UCS variable name> = Ucs(pose1)
var <UCS variable name> = Ucs(pose1, pose2, pose3)
```

The mkucs function should be used to register a user coordinate system in the system. The argument is similar to the Ucs constructor, but the user coordinate system number \(one or more\) will be inputted as the first argument.

```python
var res = mkucs(num, pose1)
var res = mkucs(num, pose1, pose2, pose3)
```

0 will be returned if successful. An error code of a negative number will be returned if failed.

# 6. Communicating with External Devices

# 6.1 FB Object: Digital I/O

Digital input/output \(I/O\) can be performed through 10 FB objects that can be accessed from HRScript. “FB” refers to fieldbus block, and each FB object is set to be mapped to the I/O hardware installed in the robot controller and contains input and output variables as elements.

# 6.1.1 Input/Output Variables

![](../../_assets/image_8.png)

In do, dob, dow, dol, and dof, the suffixes b, w, l, and f mean “byte,” “word,” “long,” and “float,” respectively, and all are signed values. These are not separate memory spaces and represent the same 960-byte space just with different data types. For example, do\[1~16\], dob\[1~2\], and dow\[1\] are all the same output signals.

![](../../_assets/image_2.png)

If a value is assigned to an output variable that starts with “do,” I/O signal output will be performed. The I/O signal currently being inputted can be acquired by reading the input variable value that starts with “di.” The do variable can be read and written, but the di variable can only be read.



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

# 6.2    ENet Module: Ethernet TCP/UDP Communication

Using the general-purpose Ethernet port of the Hi6 Controller makes it possible to transmit or receive a string with an external device through Ethernet TCP or UDP communication. It is required to create an ENet object after importing the ENet module to use this function, as shown below.

```python
import enet
var udp=enet.ENet("udp")
```

In the following example, the selection of protocol is needed by passing "udp" or "tcp" as a parameter of the ENet constructor. The default is "udp," so like in the example, it can be omitted when UDP communication is performed.

```python
var udp=enet.ENet()
```

Communication must be performed in the following order:

1. Create an ENet object with the constructor.
2. Set an IP address and port number with the member variable.
3. Open the communication connection with the open member procedure, and check the state with the state\(\) member variable.

   \(In the case of TCP communication, the connect procedure should also be performed after opening\).

4. Perform transmission/reception with the send and receive member procedures.
5. Close the communication connection with the close member procedure.









# 6.2.1 Constructor

### Description

It creates an Ethernet object and returns the reference

### Syntax

ENet\(&lt;protocol&gt;\)

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
      <td style="text-align:left">protocol</td>
      <td style="text-align:left">
        <p>&quot;tcp&quot; : TCP communication
          <br />
        </p>
        <p>&quot;udp&quot; : UDP communication
          <br />
        </p>
        <p>
          <br />
        </p>
        <p>
          <br />
        </p>
      </td>
      <td style="text-align:left">If omitted, it will be recognized as &quot;udp.&quot;</td>
    </tr>
  </tbody>
</table>

### Return Value

Reference of the created object

### Example

```python
enet0 = ENet()
var tcp = ENet("tcp")
```



# 6.2.2 Member Variables

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
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>Allows reading/writing</p>
        <p>Designates or acquires the IP address of the communication counterpart</p>
        <p>Applicable only when calling the open statement</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">rport</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>Allows reading/writing</p>
        <p>Designates or acquires the port number of the communication counterpart
          (Remote)</p>
        <p>Applicable only when calling the open statement</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">lport</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>Allows reading/writing</p>
        <p>Used in UDP communication and ignored in TCP communication</p>
        <p>Designates or acquires the port number of the controller itself (Local)</p>
        <p>The default value is 0 (if not designated), in which case the controller&#x2019;s
          port number will be automatically created.</p>
        <p>Applicable only when calling the open statement</p>
      </td>
    </tr>
  </tbody>
</table>

# 6.2.3 Member Procedures

# open

### Description

ns a connection for Ethernet TCP or UDP communication

### Syntax

&lt;ENet object&gt;.open

### Example

```python
enet_to_sensor.open
```

# connect

### Description

Performs a connection for Ethernet TCP communication

### Syntax

&lt;ENet object&gt;.connect

### Example

```python
enet_to_sensor.connect
```

# send

### Description

Transmits the values to the set Ethernet object

### Syntax

&lt;ENet object&gt;.send &lt;value&gt;, &lt;value&gt;, …



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
      <td style="text-align:left">Value</td>
      <td style="text-align:left">
        <p>Data value to be output.
          <br />
        </p>
        <p>Arguments separated by commas will be printed separated by spaces.
          <br
          />
        </p>
        <p>
          <br />
        </p>
        <p>
          <br />
        </p>
        <p>
          <br />
        </p>
      </td>
      <td style="text-align:left">All data types</td>
    </tr>
  </tbody>
</table>

### Example

```python
enet_to_sensor.send "rob:", 10, ", command:"+cmd, "\n"
```



# recv

### Description

Receives the values to the set Ethernet object

### Syntax

&lt;ENet object&gt;.recv &lt;variable&gt;\[, &lt;waiting time&gt;\]



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
      <td style="text-align:left">Variable</td>
      <td style="text-align:left">A variable to which the received string is to be passed</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Waiting time</td>
      <td style="text-align:left">
        <p>Time of time-out
          <br />
        </p>
        <p>
          <br />
        </p>
        <p>
          <br />
        </p>
        <p>
          <br />
        </p>
      </td>
      <td style="text-align:left">msec</td>
    </tr>
  </tbody>
</table>

### Example

```python
enet_to_sensor.recv  msg, 5000
```

# close

### Description

Close the connection for Ethernet UDP communication

### Syntax

&lt;ENet object&gt;.close

### Example

```python
enet_to_sensor.close
```

# 6.2.4 Member Function

# state

### Description

Returns the state of the Ethernet object

### Syntax

&lt;ENet object&gt;.state\(\)



### Return Value

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
      <td style="text-align:left">1</td>
      <td style="text-align:left">
        <p>Connected
          <br />
        </p>
        <p>(In the case of UDP, just opening it will be considered a connection.
          In the case of TCP, connecting after opening will be considered a connection.)
          <br
          />
        </p>
        <p>
          <br />
        </p>
        <p>
          <br />
        </p>
        <p>
          <br />
        </p>
        <p>
          <br />
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">0</td>
      <td style="text-align:left">Not connected</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">-1</td>
      <td style="text-align:left">Failed to create the Ethernet socket</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">-2</td>
      <td style="text-align:left">Failed to bind the Ethernet device</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### Example

```python
ret = enet_to_sensor.state()
```

# 6.2.5 Examples of TCP and UDP Communication

```python
     import enet
     global msg
     global enet0=enet.ENet() # ENet("tcp") in case of TCP communication

     # port no. 49152–65535 contains dynamic or private ports
     enet0.ip_addr="192.168.1.172"
     enet0.lport=51001 # necessary only in case of UDP communication
     enet0.rport=51002

     enet0.open
     enet0.connect # necessary only in case of TCP communication
     print enet0.state() # normal if it is 1
     enet0.send "hello, "+"udp", 300, "\n"

     enet0.recv msg, 8000 # wait for 8 seconds
     print msg
     delay 1.5
     enet0.close
     print enet0.state() # normal if it is 0
     delay 1.5
     end

```

# 6.3    Http\_Cli Module: HTTP Client

Using the general-purpose Ethernet port of the Hi6 Controller makes it possible to access remote web services to receive HTTP services. 

To use this function, it is required to create an HttpCli object after importing the http\_cli module, as shown in the following example.

```python
import http_cli
var cli=http_cli.HttpCli()
```

After the HttpCli object is created, it must request a service by calling the get, put, post, and delete member procedures.

The HttpCli object has a property named “body.”

When a get service is requested and a response is received successfully, the remote server’s data will have the body property. The body property value can be a string, number, array, or object. When requesting the put service, it is required to assign the data to be transmitted to the body property in advance.

When requesting the post service, it is required to assign the data to be transmitted to the body property in advance, and the data sent as a response from the remote server is to be stored in the body property.

The delete service does not use the body property.





# 6.3.1 Constructor

### Description

It creates an HttpCli object and returns the reference.

### Syntax

HttpCli\(\)

### Return Value

Reference of the created object

### Example

```python
var cli = HttpCli()
```



# 6.3.2 Member Variables

<table>
  <thead>
    <tr>
      <th style="text-align:left">Variable</th>
      <th style="text-align:left">Data type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">body</td>
      <td style="text-align:left">All types are possible</td>
      <td style="text-align:left">
        <p>It is required to put the data, which is to be loaded on the put and post
          requests, in advance.
          <br />
        </p>
        <p>Responses for the get and post requests will be stored.
          <br />
        </p>
        <p>
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

# 6.3.3 Member Procedure

# get

### Description

Requests the HTTP get service

The response data is to be received to the body property.



### Syntax

&lt;HttpCli object&gt;.get &lt;URL string&gt;

### Example

```python
var domain="http://192.168.1.200:8888"
cli.get domain+"/setting/max_torque"
```



# put

### Description

Requests the HTTP put service

It is required to assign the data, which is to be transmitted, to the body property in advance.

### Syntax

&lt;HttpCli object&gt;.put &lt;URL string&gt;

### Example

```python
var domain="http://192.168.1.200:8888"
cli.body=500
cli.put domain+"/setting/max_torque"
```



# post

### Description

Requests the HTTP post service.

It is required to assign the data, which is to be transmitted, to the body property in advance.

The response data is to be received to the body property.

### Syntax

&lt;HttpCli object&gt;.post &lt;URL string&gt;

### Example

```python
var domain="http://192.168.1.200:8888"
cli.body={ name: "WORK #32", color: "green", state: "OK" }
cli.post domain+"/display/update"
```

# delete

### Description

Request the HTTP delete service. 

The body property is not be used.

### Syntax

&lt;HttpCli object&gt;.delete &lt;URL string&gt;

### Example

```python
var domain="http://192.168.1.200:8888"
cli.delete domain+"/items/3"
```

# 6.3.4 Examples of HTTP Client Communication

```python
import http_client
var cli=http_client.HttpClient()

var domain="http://192.168.1.200:8888"

# get
cli.get domain+"/device/direction"
print cli.body.ry
     
# put
cli.body.ry=90
cli.put domain+"/device/direction"
     
# post
cli.body=={ name: "WORK #32", color: "green", state: "OK" }
cli.post domain+"/display/update"

# delete
cli.delete domain+"/items/3"

end
```

# 6.4 Getting input from console bar

# 6.4.1 input

### Description

Use the **input** statement to enter a string as a keystroke of the Teach Pendant and store it in a variable. If not entered by the timeout, proceed to the following statement or branch to the timeout address.

### Syntax

input &lt;variable&gt;\[,&lt;timeout&gt;,&lt;timeout address&gt;\]



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
          <br
          />
        </p>
        <p>
          <br />
        </p>
        <p>
          <br />
        </p>
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



# 7. Alias

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
