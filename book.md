
[__SOURCE](README.md)
# ${cont_model} 控制器功能手册 - 机器人语言 HRScript
[__SOURCE](0-about-this-manual/precautions.md)
# 注意事项

{% include file="zh/precautions.md" %}
[__SOURCE](1-intro/README.md)
# 1. 概述
[__SOURCE](1-intro/1-hrscript.md)
# 1.1 HRScript简介

HD Hyundai Robotics的${cont_model}控制器允许用户使用一种名为HRScript的机器人语言编程机器人的任务。创建的程序可以保存为多个扩展名为.job的文件。

HRScript是一种脚本语言，将由解释器逐行解释和执行，而无需编译过程。它类似于Python或JavaScript语言，但语法更简单。
[__SOURCE](2-basic-syntax/README.md)
# 2. 基本语法

本节描述了HRScript的基本术语。通过以下定义变量的方法、使用运算符构造简单表达式以及将结果值分配给变量的方式，可以理解作业程序的基本概念。
[__SOURCE](2-basic-syntax/1-statements.md)
# 2.1 声明

声明是指每个命令字符串，该字符串成为作业程序的执行单元。HRScript 每行只允许一个声明。请注意下面四个声明示例的写法，特别是它们的外观。

```python
     move P,po3,spd=80%,accu=1,tool=3 until do33
10   z_pos = (base_height+offset)*1.05
     # robot has to wait sensor2 input
     *err_handle
```

对于除了步骤声明（如移动声明等）之外的其他声明，您可以选择在行首添加一个行号（1 到 9999）。第二行中的数字 10 是行号的示例。

在声明前后有任意数量的空格或制表符都无关紧要。

为了提高可读性，建议在声明中使用适当的缩进。缩进允许使用空格和制表符，在执行过程中不会影响操作。
[__SOURCE](2-basic-syntax/2-identifier.md)
# 2.2 标识符

命令、变量、函数和标签必须被命名。这些名称统称为`标识符`。在决定标识符时，必须遵循以下HRScript标识符的规则。

* 它只能由大写字母和小写字母、数字以及下划线组成。
* 它区分大小写。 （全局变量中的顶层数组名称除外）
* 第一个字符只能是小写字母、大写字母或下划线，而不能是数字。
* 它不应包含空格或标签。
* 系统中已经定义的标识符，如`if`和`for`，不能使用。
* 长度没有限制。

以下展示了标识符的正确和错误示例：

```text
myvar (O) 
myvar2 (O)
_myvar (O)
MyVar (O)
310a (X) - 以数字开头
move (X) - 已在系统中定义的标识符
v300$ (X) - 使用了下划线以外的符号 ($)
my var (X) - 包含了空格
```

{% hint style="warning" %}

例外的是，全局变量中的顶层数组名称不区分大小写。
（这是因为顶层全局数组被保存为.csv文件，而文件名不区分大小写。）

例如，以下两个变量不能一起使用：

    global MyArr = Array(10)
    global myarr = Array(10)

{% endhint %}
[__SOURCE](2-basic-syntax/3-statement-type/README.md)
# 2.3 语句类型

HRScript 的四种语句类型如下：

* 过程
* 赋值
* 注释
* 标签
[__SOURCE](2-basic-syntax/3-statement-type/1-procedure.md)
# 2.3.1 程序

一个程序由一个命令和 0-N 个参数组成。

```python
move P,po3,spd=80%,accu=1,tool=3 until do33
```

三种类型的程序参数如下：

| 类型 | 语法 | 示例 |
| :--- | :--- | :--- |
| 位置参数 | &lt;value&gt; | P, po3 |
| 关键字参数 | &lt;keyword&gt; = &lt;value&gt; | spd=80%, accu=1, tool=3 |
| 介词参数 | &lt;preposition&gt;  &lt;value&gt; | until do33 |

位置参数的角色由其位置决定，因此不应移动，并且必须始终位于程序的前面。

关键字参数应放在位置参数之后。然而，关键字参数之间的顺序不会影响操作。

介词参数应放在最后。
[__SOURCE](2-basic-syntax/3-statement-type/2-assignment.md)
# 2.3.2 赋值语句

赋值语句由左侧、赋值运算符 \(=\) 和右侧组成。左侧 \(lvalue\) 必须是一个可以存储值的变量。常量或表达式是不允许的。

另一方面，右侧 \(rvalue\) 允许常量、变量和表达式。 

```python
height=(500+margin)/2
```
[__SOURCE](2-basic-syntax/3-statement-type/3-comment.md)
# 2.3.3 注释语句

注释语句用于以易于理解的方式描述作业程序的内容。即使注释语句被执行，也不会执行任何操作。如下面所示，描述附加在井号 \(\#\) 之后。它可以作为单独的语句使用或附加在另一个语句之后。

```python
# robot has to wait sensor2 input
var work_w,work_h  # width and height of a workpiece
```
[__SOURCE](2-basic-syntax/3-statement-type/4-label.md)
# 2.3.4 标签

标签用于标记根据 goto 语句移动的目标点。它由一个星号 \(\*\) 和一个标识符组成。
[__SOURCE](2-basic-syntax/4-hello-world.md)
# 2.4 第一个程序 - 你好，世界！

让我们创建一个简单的作业程序，在教学挂件屏幕上打印字符串。在创建新作业后，如下所示记录打印语句，并附加字符串参数“你好，世界！”

```python
print "Hello, World !"
```

打印语句用于在教学挂件的作业面板的底部打印值。现在，当你运行程序时，可以看到文本“你好，世界！”打印在作业面板的底部。
[__SOURCE](2-basic-syntax/5-type/README.md)
# 2.5 数据类型
[__SOURCE](2-basic-syntax/5-type/1-type-string.md)
# 2.5.1 字符串数据类型

前一段中的第一个程序使用了数据 "Hello, World!" 作为打印语句的参数，属于字符串数据类型。字符串数据类型的值以双引号开始和结束。字符串的长度没有限制。

```python
print "欢迎来到机器人世界。"
```

以反斜杠 \(\\) 开头的序列表示字符串中的双引号或特殊字符。这个序列称为“转义字符”。

支持的转义字符如下表所示。

|  |  |
| :--- | :--- |
| \" | 双引号 |
| \\ | 反斜杠 |
| \t | 制表符 |
| \n | 换行符 |

```python
print "信息:\n请按 \"确定\" 按钮。"

# 打印结果
信息:
请按 "确定" 按钮。
```
[__SOURCE](2-basic-syntax/5-type/2-number-type.md)
# 2.5.2 数值数据类型

数值数据类型存储整数或实数。让我们使用打印语句进行打印。如果在打印语句中列出多个用逗号 \(,\) 分隔的值，如下例所示，则每个值将以空格分隔显示。

```python
280
3.141592
-99
print 280, -99
```

在系统内部，整数和实数分别处理。每种数据大小如下：

| 数据类型 | 数据大小 \(字节\) |
| :--- | :--- |
| 整数 | 4 |
| 实数 | 8 |
[__SOURCE](2-basic-syntax/5-type/3-bool-type.md)
# 2.5.3 布尔数据类型

作为以下逻辑和比较操作的结果，只有两个值，true 和 false。

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
# 2.5.4 数组类型和对象类型

此外，还有数组类型和对象类型。这将在第 4.1 节和第 4.2 节中进行更详细的讨论。
[__SOURCE](2-basic-syntax/6-variable.md)
# 2.6 变量

变量可以存储值并具有标识符名称。变量分为全局变量和局部变量，它们之间的区别将在后面描述。局部变量的示例将在这里首次介绍。

变量可以使用 var 命令创建，如下所示。这被称为定义变量。可以通过在 var 命令后列举多个标识符一次性创建多个标识符。

```python
var myvar
var width, height, depth
```

将值存储到变量中称为“赋值”。赋值可以在定义变量时或在定义变量后进行。如果在定义时未进行赋值，则变量默认具有数值 0。

```python
var myvar=0
var message, width=200
message="无效的输入值"
```

在 HRScript 中，\(=\) 并不表示相等。它用作赋值运算符，意味着运算符右侧的值被赋给左侧的变量。存储在变量中的值可以通过 print 语句打印出来。

```python
var myvar=0
var message, width=200
message="无效的输入值"
print width, message
```

可以给已经赋值的变量赋一个不同的值。之所以称为变量，是因为其值可以改变。

```python
var width=200
width=300
```
[__SOURCE](2-basic-syntax/7-binary-hex-number.md)
# 2.7 二进制和十六进制

之前作为示例描述的所有数字类型值都被解释为十进制数。只需添加 0b 或 0x 前缀，即可表示二进制或十六进制值，如下所示。

```python
var binary = 0b10010011
var hexadecimal = 0xFF4A38C0
```
[__SOURCE](2-basic-syntax/8-operator-expression.md)
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
[__SOURCE](2-basic-syntax/9-function/README.md)
# 2.9 函数

将角度 60° 转换为弧度值的过程是什么，或者如何找到变量 mystr 所包含的字符串的长度？

HRScript 提供了各种函数，这些函数通过参数接收输入，执行一些处理，并返回结果值。

函数可以作为表达式的一部分使用，如下所示。

```python
var dg=60, rd
rd=deg2rad(dg)

var limit=40, message="Input your code number"
var validity= len(message) < limit
```

HRScript 提供的函数列表如下。\(表格按名称的升序排列。\)
[__SOURCE](2-basic-syntax/9-function/1-func-math.md)
# 2.9.1 数学函数

<table style="text-align:left">
  <thead>
    <tr>
      <th>函数</th>
      <th>描述</th>
      <th>用法示例</th>
      <th>结果</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>abs(<b>a</b>)</td>
      <td>返回<b>a</b>的绝对值
      </td>
      <td>abs(-300)</td>
      <td>300</td>
    </tr>
    <tr>
      <td>acos(<b>a</b>)</td>
      <td>返回<b>a</b>的弧度余弦值</td>
      <td>acos(0.5)</td>
      <td>1.0472</td>
    </tr>
    <tr>
      <td>asin(<b>a</b>)</td>
      <td>返回<b>a</b>的弧度正弦值</td>
      <td>asin(0.5)</td>
      <td>0.5236</td>
    </tr>
    <tr>
      <td>atan(<b>a</b>)</td>
      <td>返回<b>a</b>的弧度反正切值</td>
      <td>atan(0.5)</td>
      <td>0.4636</td>
    </tr>
    <tr>
      <td>atan2(<b>a</b>, <b>b</b>)</td>
      <td>返回一个三角形的弧度反正切值，其<b>a</b>为y轴长度，
        <b>b</b>为x轴长度</td>
      <td>atan2(2,1)</td>
      <td>1.1071</td>
    </tr>
		<tr>
			<td>ceil(x)</td>
			<td>返回<b>x</b>的向上取整数值。</td>
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
      <td>返回<b>r</b>的余弦值，单位为弧度格式</td>
      <td>cos(3.1415)</td>
      <td>-1</td>
    </tr>
    <tr>
      <td>deg2rad(<b>d</b>)</td>
      <td>返回<b>d</b>的弧度值，单位为度格式</td>
      <td>deg2rad(-90)</td>
      <td>-1.570796</td>
    </tr>
    <tr>
      <td>dist(<b>x</b>, <b>y</b>)</td>
      <td>返回从原点到（<b>x</b>, <b>y</b>）坐标的欧几里得距离</td>
      <td>dist(3.5,10)</td>
      <td>10.59481</td>
    </tr>
		<tr>
			<td>floor(x)</td>
			<td>返回<b>x</b>的向下取整值。</td>
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
      <td>返回<b>a</b>和<b>b</b>之间的较大值
      </td>
      <td>max(-1.23, -3)</td>
      <td>-1.23</td>
    </tr>
    <tr>
      <td>min(<b>a</b>, <b>b</b>)</td>
      <td>返回<b>a</b>和<b>b</b>之间的较小值
      </td>
      <td>max(-1.23, -3)</td>
      <td>-3</td>
    </tr>
    <tr>
      <td>near(<b>a</b>, <b>b</b> [,<b>e</b>])</td>
      <td>如果实数值<b>a</b>和<b>b</b>之间的差小于或等于<b>e</b>，则返回1；如果差大于<b>e</b>，则返回0</td>
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
      <td>返回<b>r</b>的弧度值的角度格式</td>
      <td>rad2deg(1.570796)</td>
      <td>90</td>
    </tr>
		<tr>
			<td>round(x)</td>
			<td>返回<b>x</b>的四舍五入值。</td>
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
      <td>返回<b>r</b>的正弦值，弧度格式</td>
      <td>sin(1.5*3.1415)</td>
      <td>-1</td>
    </tr>
    <tr>
      <td>sqr(<b>a</b>)</td>
      <td>返回<b>a</b>的平方根</td>
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
      <td>返回 <b>r</b> 的切线值，以弧度格式表示</td>
      <td>tan(3.141592/4)</td>
      <td>0.9999</td>
    </tr>
		<tr>
			<td>trunc(x)</td>
			<td>返回 <b>x</b> 的截断整数部分。</td>
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
      返回格式重新解释的 v 值的二进制数据。<br>
			有关支持的格式，请参考下表 [Table 1]。
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

[Table 1] `val_as()` 函数的支持格式
<table style="text-align:left">
	<thead>
		<tr>
			<th>字节序</th>
			<th>格式</th>
			<th>含义</th>
		</tr>
	</thead>
	<tbody>
		<tr><td rowspan="7">小端<br>字节序</td>
		     <td>u1</td><td>无符号1字节</td></tr>
		<tr><td>u2</td><td>无符号2字节</td></tr>
		<tr><td>s1</td><td>有符号1字节</td></tr>
		<tr><td>s2</td><td>有符号2字节</td></tr>
		<tr><td>s4</td><td>有符号4字节</td></tr>
		<tr><td>f4</td><td>浮点数4字节</td></tr>
		<tr><td>f8</td><td>双精度8字节</td></tr>
		<tr><td rowspan="7">大端<br>字节序</td>
		     <td>U1</td><td>无符号1字节</td></tr>
		<tr><td>U2</td><td>无符号2字节</td></tr>
		<tr><td>S1</td><td>有符号1字节</td></tr>
		<tr><td>S2</td><td>有符号2字节</td></tr>
		<tr><td>S4</td><td>有符号4字节</td></tr>
		<tr><td>F4</td><td>浮点数4字节</td></tr>
		<tr><td>F8</td><td>双精度8字节</td></tr>
	</tbody>
</table>
[__SOURCE](2-basic-syntax/9-function/2-func-string.md)
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
[__SOURCE](2-basic-syntax/9-function/3-func-datetime.md)
# 2.9.3 日期和时间函数

<table>
  <thead>
    <tr>
      <th style="text-align:right">函数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">使用示例</th>
      <th style="text-align:left">结果</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:right">date( )</td>
      <td style="text-align:left">
        <p>返回当前日期，字符串类型</p>
        <p>(YYYY-MM-DD 格式)</p>
      </td>
      <td style="text-align:left">date( )</td>
      <td style="text-align:left">&quot;2019-04-17&quot;</td>
    </tr>
    <tr>
      <td style="text-align:right">time( )</td>
      <td style="text-align:left">
        <p>返回当前时间，字符串类型</p>
        <p>(HH:MM:SS 格式)</p>
      </td>
      <td style="text-align:left">time( )</td>
      <td style="text-align:left">&quot;08:48:14&quot;</td>
    </tr>
    <tr>
      <td style="text-align:right">timer( )</td>
      <td style="text-align:left">返回从开机时起经过的时间（秒）</td>
      <td style="text-align:left">timer( )</td>
      <td style="text-align:left">2796.37</td>
    </tr>
  </tbody>
</table>
[__SOURCE](2-basic-syntax/9-function/4-func-creator.md)
# 2.9.4 构造函数

这些函数接收参数输入，然后创建并返回一个对象。

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
      <td style="text-align:left">
        <p>Array(n)</p>
        <p>Array(a, b, c)</p>
      </td>
      <td style="text-align:left">
        <p>创建并返回一个包含“n”个元素的数组</p>
        <p>元素的初始值为0。</p>
        <p>如果指定两个或更多元素，则会创建一个多维数组。</p>
        <p>参见 &quot;<a href="../../4-array-object/1-array/3-array-creator">4.1.3 数组构造函数 - Array()</a>&quot;。</p>
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
        <p>创建并返回一个姿态对象</p>
        <p>参见 &quot;<a href="../../5-moving-robot/1-pose.md">5.1 姿态</a>&quot;。</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">姿态对象</td>
    </tr>
    <tr>
      <td style="text-align:left">Shift(element)</td>
      <td style="text-align:left">
        <p>创建并返回一个位移对象</p>
        <p>参见 &quot;<a href="../../5-moving-robot/2-shift.md">5.2 位移</a>&quot;。</p>
      </td>
      <td style="text-align:left"></td>
<td style="text-align:left">移动对象</td>
    </tr>
  </tbody>
</table>
[__SOURCE](2-basic-syntax/9-function/5-func-etc.md)
# 2.9.5 其他功能

<table>
  <thead>
    <tr>
      <th style="text-align:left">功能</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">使用示例</th>
      <th style="text-align:left">结果</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">cpo(crd, mode)</td>
      <td style="text-align:left">
        <p>返回机器人的当前姿态到"crd"坐标系</p>
        <p>有关可以作为"crd"元素使用的值，请参见 "<a href="../../5-moving-robot/1-pose.md">5.1 姿态</a>" 下的表格。</p>
        <p>如果模式为"cmd"，则为命令值；如果模式为"cur"，则为当前值。</p>
        <p>"crd"和"mode"参数可以省略，它们的默认值分别为"base"和"cur"。</p>
      </td>
      <td style="text-align:left">cpo("joint", "cmd")</td>
      <td style="text-align:left">姿态*，保存机器人的命令值到轴坐标系</td>
    </tr>
    <tr>
      <td style="text-align:left">gather_state()</td>
      <td style="text-align:left">通过执行 <a href="../../10-etc/1-proc/1-gather.md">gather</a> 语句返回当前的数据收集状态</td>
      <td style="text-align:left">gather_state()</td>
      <td style="text-align:left">
        0 : 不在收集状态。<br>
        1 : 在收集状态。<br>
        2 : 将收集结果保存为文件。
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>mkucs(n,po)</p>
        <p>mkucs(n,po1,po2,po3)</p>
        <p>mkucs(n,"OXY",po1,po2,po3)</p>
      </td>
      <td style="text-align:left">
        <p>创建并注册第 n 个用户坐标系对象</p>
        <p>请参考 "<a href="../../5-moving-robot/5-ucs.md">5.5 用户坐标系统 (UCS)</a>"。</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
<p>0: 好</p>
        <p>&lt;0: 错误代码</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">result()</td>
      <td style="text-align:left">对于某些程序，可能需要检查结果。如果在执行程序之后立即调用result()函数，则可以返回执行结果。</td>
      <td style="text-align:left">result()</td>
      <td style="text-align:left"></td>
    </tr>
   <tr>
      <td style="text-align:left">mkshift(3,ref_po,mea_po,2.0) <br>
      mkshift(5,ref_po,mea_sft)
      </td>
      <td style="text-align:left">优化的偏移值是根据多个参考姿势的测量姿势或偏移数据计算并返回的。 <br>
      如果指定的与公差相关的第4个参数大于0，并且计算的偏移值大于该值，则会停止并报告错误。 <br>
      # 注 <br>
      ref_po（参考姿势）和 mea_po（测量姿势）是姿势变量的数组类型，mea_sft（测量偏移）是偏移变量的数组类型。 <br>
      如果没有与公差相关的第4个参数，则不会检测到错误。 <br>
      我们目前支持最多100个位置。
      </td>
      <td style="text-align:left">sft1=mkshift(4,ref_po,mea_po,3.0)</td>
      <td style="text-align:left">偏移</td>
    </tr> 
    <tr>
      <td style="text-align:left">calshift(po1,po2) <br>
      calshift(po1,po2,"TV")
      </td>
      <td style="text-align:left">返回两个姿势之间的差异作为偏移值。 <br>
      如果存在“TV”参数，则返回工具的垂直方向作为偏移值。
      </td>
      <td style="text-align:left">sft1=calshift(po1,po2)</td>
      <td style="text-align:left">偏移</td>
    </tr> 
    <tr>
      <td style="text-align:left">po.valid()
      </td>
      <td style="text-align:left">
        返回与机器人的运动范围内姿势对象有关的信息。 <br>
        # 示例 <br>
        if po1.valid()==0 <br>
            stop # 机器人停止<br>
        endif <br>        
      </td>
      <td style="text-align:left">var ret=po1.valid()
      </td>
      <td style="text-align:left">0: 超出操作范围 <br>
      1: 在操作范围内
      </td>
    </tr>
<tr>
      <td style="text-align:left">po.str_array()
      </td>
      <td style="text-align:left">
        返回关于姿态对象的信息，以数组格式的字符串形式表示。 <br>
        # 示例 <br>
        var msg=cpo().str_array() <br>
        print msg # [1850.000,2010.500,0.000,0.000,-90.000,0.000,"base"]
      </td>
      <td style="text-align:left">msg=po1.str_array()
      </td>
      <td style="text-align:left">字符串</td>
    </tr>
    <tr>
      <td style="text-align:left">sft.str_array()
      </td>
      <td style="text-align:left">
        返回关于位移对象的信息，以数组格式的字符串形式表示。 <br>
        # 示例 <br>
        var sft1=Shift(0.000,0.000,30.000,0.000,0.000,0.000,"base") <br>
        var msg=sft1.str_array() <br>
        print msg # [0.000,0.000,30.000,0.000,0.000,0.000,"base"]
      </td>
      <td style="text-align:left">msg=sft1.str_array()
      </td>
      <td style="text-align:left">字符串</td>
    </tr>
    <tr>
      <td style="text-align:left">upo(crd)
      </td>
      <td style="text-align:left">
        <p>在执行移动 ~ 直到语句时，当直到条件满足时返回当前姿态，返回值为crd坐标系。</p>
        <p>有关可以用作“crd”元素的值，请参见
          "<a href="../../5-moving-robot/1-pose.md">5.1 姿态</a>" 下的表格。</p>
         <p>“crd”参数可以省略，默认值为“base”。</p>
      </td>
      <td style="text-align:left">upo(&quot;joint&quot;)
      </td>
      <td style="text-align:left">姿态*</td>
    </tr>

  </tbody>
</table>

\* 姿态是一种数据类型，表示机器人姿态或工具尖端的位置。详细信息将在"[5.1 姿态](../../5-moving-robot/1-pose.md)"中描述。
[__SOURCE](2-basic-syntax/10-import.md)
# 2.10 `import`

### 描述

某些功能不是 hrspace 的内置功能，但也以插件模块的形式得到支持。

一些模块作为默认选项预先安装，而另一些则需要您自行安装。  
该模块必须在机器人语言中通过 `import` 语句加载到控制器中，然后才能使用。

### 语法

import &lt;module name&gt; [as &lt;alias&gt;]

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">module name</td>
      <td style="text-align:left">
        模块的名称
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">alias</td>
      <td style="text-align:left">
			在机器人语言程序中使用的名称。<br>
			如果指定，可以代替模块名称使用。
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

例如，为了在机器人语言中执行以太网 TCP 或 UDP 通信，您必须 `import` 名为 `enet` 的默认选项模块。

在执行 `import` 后，一个名为 `enet` 的模块对象将在全局作用域中创建。正如下面的例子 `enet.ENet()`，您可以访问模块对象的成员变量或调用成员函数，特别是在调用成员函数中的 `creator` 时，您可以创建新的对象。

### 示例

在下面的示例中，  
(1) `enet` 模块对象已被 `import`。
(2) 调用了 `enet.ENet()` 创建函数以创建一个新的以太网套接字对象，并将其分配给名为 `cli` 的局部变量。  
(3) 将一个字符串分配给对象 `cli` 的成员变量 `ip_addr`。

```python
import enet # (1)
var cli=enet.ENet() # (2)
cli.ip_addr="192.168.1.172" # (3)
```

以下面的方式编写时也会执行相同的操作。

```python
import enet as enet_module # (1)
var cli=enet_module.ENet() # (2)
cli.ip_addr="192.168.1.172" # (3)
```

* 本节仅涵盖了 `import` 声明的粗略语法。您将在后面的章节中看到关于模块功能的 `import` 使用示例。
[__SOURCE](3-flowcontrol-subprogram/README.md)
# 3. 流控制语句和子程序

作业程序中的语句按从上到下的顺序逐行执行。然而，根据某些条件，语句可以被跳过而不被执行，或者某些语句可以被重复执行。让我们看看可以以这种方式控制程序流程的控制语句。
[__SOURCE](3-flowcontrol-subprogram/1-address.md)
# 3.1 地址

在程序中移动到另一个位置而不按顺序执行下一行称为“分支”。
地址是分支的目的地。

定义地址有三种方法：

<table>
  <thead>
    <tr>
      <th style="text-align:left">类型</th>
      <th style="text-align:left">格式</th>
      <th style="text-align:left">示例</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">行号</td>
      <td style="text-align:left">
        介于 1~9999 之间的整数。可以附加在语句的左侧，而不是步骤。
      </td>
      <td style="text-align:left">99</td>
    </tr>
    <tr>
      <td style="text-align:left">标签</td>
      <td style="text-align:left">
        标签不是附加在语句上的语法，而是语句本身。<br>
        其形式为 \* 后跟 [标识符](2-identifier.md)。但标识符不得超过 128 个字符。
      </td>
      <td style="text-align:left">*timeout</td>
    </tr>
    <tr>
      <td style="text-align:left">步骤编号</td>
      <td style="text-align:left">
        步骤编号在步骤递增时自动附加。<br>
        其形式为 S 后跟步骤编号。可以指定 S1~S999。
      </td>
      <td style="text-align:left">S15</td>
    </tr>
  </tbody>
</table>


在下面的示例中，第二个语句中的 `10` 是行号，`*err_handle` 是标签，`S12` 是步骤编号。

```python
     move P,po3,spd=80%,accu=1,tool=3 until do33
  10 z_pos = (base_height+offset)*1.05
     # robot has to wait sensor2 input
     *err_handle
S12  move P,spd=80%,accu=1,tool=3
```

[__SOURCE](3-flowcontrol-subprogram/2-stop-wait/README.md)
# 3.2 停止或等待语句

该语句可以停止程序的执行，或使其等待特定时间或直到条件满足。
[__SOURCE](3-flowcontrol-subprogram/2-stop-wait/1-stop.md)
# 3.2.1 `停止 (stop)`

### 描述

这将停止程序。当程序重新启动时，执行将从下一行继续。

### 语法

stop

### 示例 

```python
if di9
  stop
endif
```
[__SOURCE](3-flowcontrol-subprogram/2-stop-wait/2-end.md)
# 3.2.2 `end`

### 描述

这将停止程序。当处于连续播放模式或重启模式时，执行将从主程序的开头重新开始。

### 语法

end

### 示例

```python
move p,spd=70%,accu=1,tool=0
move p,spd=70%,accu=1,tool=0
end
```
[__SOURCE](3-flowcontrol-subprogram/2-stop-wait/3-delay.md)
# 3.2.3 `延迟 (delay)`

### 描述

使得在等待指定时间后可以继续执行下一个命令语句。

### 语法

delay &lt;time&gt;

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">时间</td>
      <td style="text-align:left">等待的时间</td>
      <td style="text-align:left">
        <p>算术表达式
          <br />
        </p>
        <p>0.1~60.0 秒
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

### 示例

```python
delay 3.5
```
[__SOURCE](3-flowcontrol-subprogram/2-stop-wait/4-wait.md)
# 3.2.4 `wait`

### 描述

在等待指定条件变为真之后，可以移动到下一个命令语句。

### 语法

wait &lt;condition&gt;\[,&lt;timeout&gt;,&lt;timeout address&gt;\]

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">条件</td>
      <td style="text-align:left">需要等待的条件</td>
      <td style="text-align:left">条件表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">超时</td>
      <td style="text-align:left">当条件为假时，等待发生的最大时间限制（超时）</td>
      <td style="text-align:left">
        <p>算术表达式</p>
        <p>0.1~60.0 秒</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">超时地址</td>
      <td style="text-align:left">超时超过时将用于跳转的地址。</td>
      <td
      style="text-align:left">地址</td>
    </tr>
  </tbody>
</table>

### 示例

```python
wait sensor_ok
wait (sensor_ok and pos_ok),10,*timeout
```

[__SOURCE](3-flowcontrol-subprogram/3-branch/README.md)
# 3.3 分支语句

使得在没有条件的情况下可以转到不同的地址。
[__SOURCE](3-flowcontrol-subprogram/3-branch/1-goto.md)
# 3.3.1 `goto`

### 描述

使得能够转到指定地址。

### 语法

goto &lt;address&gt;

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">address</td>
      <td style="text-align:left">
        分支地址<br/>
        对于行号，可以使用算术表达式。
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### 示例

```python
goto 99
goto addr
goto *err_hdl
```
[__SOURCE](3-flowcontrol-subprogram/3-branch/2-gosub.md)
# 3.3.2 `gosub`~`retsub`

### 描述

当遇到 `gosub` 语句时，它会跳转到指定的地址。当遇到 `retsub` 语句时，它会返回到 `gosub` 语句之后的下一个位置。`gosub` 可以嵌套多层，并且没有嵌套的数量限制。

### 语法
```python
gosub <address>
...
end
  
<address>
...  
retsub
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">address</td>
      <td style="text-align:left">
        <p>要跳转的地址</p>
        <p>在行号的情况下，可以使用算术表达式。</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### 示例

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
# 3.4 条件语句

这些语句允许某些操作根据特定条件执行或不执行。
[__SOURCE](3-flowcontrol-subprogram/4-conditional/1-simple-if.md)
# 3.4.1 单行 `if`

### 描述

单行 `if` 语句的形式如下：如果 &lt;布尔表达式&gt; 为真，将分支到 &lt;地址&gt;。如果为假，则移动到下一个语句。

### 语法

```python
if <bool expression> then <address>
```

### 示例

下面是单行 if 语句的示例。如果压力大于限制的条件为真，则将分支到标签地址 "\*err"，使得可以打印出压力过高的警告。如果条件为假，则下一个语句将一个接一个地执行，而不会分支，因此将打印 "正常运行中" 并结束程序。

```python
var pressure=95, limit=90
if pressure > limit then *err
print "in normal operation."
end
*err
print "warning: pressure is too high."
```
[__SOURCE](3-flowcontrol-subprogram/4-conditional/2-if-endif.md)
# 3.4.2 `if`-`endif`

### 描述

如果单行 `if` 语句为真，则仅会执行跳转到特定地址的操作。如果需要执行其他操作或多个语句，则应使用 `if`-`endif` 块。

形式如下：如果 &lt;布尔表达式&gt; 为真，则将依次执行位于 `if` 和 `endif` 之间的多个 &lt;语句&gt;。如果 &lt;布尔表达式&gt; 为假，则会跳过 `endif` 后的位置，而不执行 &lt;语句&gt;。

### 语法

```python
if <bool expression>
	<statement>
	...
endif
```

### 示例

在以下示例中，如果压力大于限制，则将执行以下赋值和打印语句。否则，将跳转到结束而不执行语句。

```python
var pressure=95, limit=90, exceed
if pressure > limit
	exceed = pressure - limit
	print "warning: pressure is too high."
endif
end
```

在示例程序中，`if` 和 `endif` 之间的语句缩进了两个空格。这些语句的缩进使得更容易识别它们是嵌套在 `if` 和 `endif` 之间的代码块。
[__SOURCE](3-flowcontrol-subprogram/4-conditional/3-if-else-endif.md)
# 3.4.3 `if`-`else`-`endif` 语句

### 描述

如果表达式为假，并且 `if` 有要执行的语句，则使用以下形式：

如果表达式为真，则执行语句 A。如果为假，则执行语句 B。

### 语法

```python
if <bool expression>
	<statement A>
	...
else
	<statement B>
	...
endif
```

### 示例

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
# 3.4.4. `if`-`elseif`-`else`-`endif`

### 描述

在多个条件的情况下，可以以以下形式使用 `elseif` 语句。

### 语法

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

### 示例

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
# 3.4.5 `switch`-`case`-`break`-`end_switch`

### 描述

`switch` 语句评估一个数值表达式，并将其与由 `case` 语句指定的数值表达式的结果进行比较。它从相等值的 `case` 语句开始执行，直到遇见 `break` 语句。

在以下示例中，如果表达式 `X` 的结果值等于表达式 `B1` 或 `B2` 的结果值，则将执行 \(1\) 到 \(3\)，并移动到 `end_switch` 语句的位置 \(请注意，这里没有位于命令语句 B\ 下方的 `break`\)。与此同时，如果表达式 `X` 的结果值等于表达式 `C` 的结果值，则将执行 \(2\) 到 \(3\)。

如果表达式 `X` 的结果值不等于任何 `case` 语句的结果值，将移动到 `默认 (default)`，并将执行 \(4\) 到 \(5\)。然后，可以省略 `默认 (default)` 部分。

### 语法

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

任何表达式，例如布尔值、数值、字符串常量、参数和数值，都是允许的。

### 示例

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
# 3.5. 嵌套流程控制语句

### 描述

在控制语句块中，可以放置另一个控制语句块，如下例所示。在以下形式中，显示了两个嵌套级别，但可以根据需要进行多个嵌套级别。

### 语法

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

### 示例

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
# 3.6 循环语句

当需要多次重复相同操作时，可以使用循环语句。
[__SOURCE](3-flowcontrol-subprogram/6-loop/1-for-next.md)
# 3.6.1 `for`-`next`

### 描述

重复相同操作的 `for`~`next` 语句的格式如下。

首先，初始值将被分配给索引变量。当在执行 `for` 语句下的语句时遇到 `next` 语句时，索引变量将增加或减少值，并从 `for` 语句的点开始重复。当索引变量超过结束值时，重复将结束。

如果未指定步长，将应用 1。

### 语法

```python
for <索引变量>=<初始值> to <结束值> [step <增量/减量值>]
	<语句>
	...
next
```

### 示例

下面是一个使用 `for`-`next` 语句将 1 到 10 累加到总和的例子。当重复结束时，11 和 55 将在屏幕上打印出来。

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
# 3.6.2 `break`, `continue`

### 描述

`break` 和 `continue` 用于本节前面解释的 `for`~`next` 语句之间。

- 当在 `for`~`next` 块中遇到 `break` 时，循环停止重复，并跳转到 `next` 语句。
- 当在 `for`~`next` 块中遇到 `continue` 时，不会继续到下一个语句，而是对索引变量进行递增/递减，并跳转到 `for` 语句。

### 语法

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

### 示例

这是一个使用 `for`~`next` 语句输出数组中所有名称的示例，但不包括超过 5 个字符的名称，并在遇到空字符串时停止。

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
安娜
詹姆斯
汤姆
```
[__SOURCE](3-flowcontrol-subprogram/7-call-jump/README.md)
# 3.7 `call`, `jump` 语句和子程序

如果整个大规模机器人操作作为一个工作程序创建，程序将变得庞大而复杂，使得添加功能或找到并解决问题变得困难。

为了程序的可维护性，最好将构成整个程序的单元操作划分为子程序。例如，当例程，如与传感器进行通信的例程、使用接收到的数据计算工具尖端目标位置的例程，以及当发生错误时生成适当消息的例程，变成独立的子程序并允许主程序调用时，将更容易掌握程序的整体结构。这在其他项目中重用分割的子程序也会有所帮助。
[__SOURCE](3-flowcontrol-subprogram/7-call-jump/1-call.md)
# 3.7.1 `call`

### 描述

HRScript中主程序和子程序的格式没有显著区别。通过启动按钮或信号执行的第一个任务是主程序，所有通过`call`语句调用的其他任务则是子程序。

### 语法

```python
call <作业编号，文件名或用户函数名> [,参数1,参数2,...]
```

在`call`语句后指定作业文件名的作业编号（不包括扩展名）。然后，在执行程序`A`时，如果遇到调用`B`，将停止执行`A`，并继续执行子程序`B`的第一条语句。如果在执行`B`时遇到`end`或`return`语句，程序`A`的执行将在返回到之前调用的程序`A`的`call`语句的下一条语句的位置继续。

### 示例

以下显示了通过`call`语句调用的子程序的示例及结果。将程序分成两个似乎没有意义，因为子程序必须仅处理一个打印语句。不过，将在后面展示一个更实用的例子。

* 请参见[3.7.3 def](./3-def.md)以获取调用用户函数的示例。

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

结果
```python
main job start
sub-program
main job end
```
[__SOURCE](3-flowcontrol-subprogram/7-call-jump/2-param-return.md)
# 3.7.2 参数和 `param`， `return`

在作业程序中，正式参数作为输入和输出传递的通道。 `param` 语句将在作业程序的开头定义正式参数。

在以下示例中，作业编号 105 被命名为 "dist2d"，因为它是一个子作业，获取从原点到坐标值 \(x, y\) 的欧几里得距离并将其返回到 len。

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
# 计算二维欧几里得距离
param dx,dy
var tmp

tmp=x*x+y*y
var len=sqr(tmp) # 从原点的距离
return len
```

<br>

结果
```python
13.742
```

在作业编号 1 中，dist2d 子程序通过 `call` 语句被调用，"x, y," 作为局部变量被传递。在 dist2d 子程序中，通过 `param` 语句定义的 "dx" 和 "dy" 被称为 "正式参数"，而传递给 `call` 语句的 "x, y" 被称为 "实际参数"。

dist2d 程序通过 `return` 语句将结果值传输到外部目的地。返回的值可以通过在被调用程序中调用 result\(\) 函数来获取。

(`return` 语句和 `end` 语句具有相同的作用，因为它们结束被调用程序并返回到主程序。然而，`return` 语句与 `end` 语句不同，因为前者可以将结果值指定为元素)。
[__SOURCE](3-flowcontrol-subprogram/7-call-jump/3-def.md)
# 3.7.3 `def` (定义用户函数)

since V60.05-06

### 描述

您可以在作业中使用 `def` 语句定义用户函数，并使用 `call` 语句调用它。与 `param` 语句类似，`def` 语句可以指定形式参数的列表。`call` 语句的实际参数值会传递给形式参数。使用 `def` 语句定义的函数执行完后，会在 `call` 语句的下一个语句处返回，当执行 `return` 语句或 `end` 语句时。

用户函数是通过名称调用而不是编号，因此其可读性优于子程序。您可以将多个相关函数分组到一个子程序中，以改善项目结构。

### 语法

```python
def <用户函数名称> [,parameter1[=默认值],parameter2[=默认值],...]
```

在 `def` 后指定用户函数名称。函数名称必须遵循第 [2.2 标识符](../../2-basic-syntax/2-identifier.md) 节中定义的规则。此外，它应该是全局唯一的名称。注意不要与其他函数名称或变量名称重复新的名称。
之后，指定形式参数。您还可以为每个参数指定默认值。如果在 `call` 语句中省略了实际参数，形式参数将被初始化为默认值。如果您开始为特定形式参数指定默认值，则必须为最后一个参数之前的所有参数指定默认值。

```python
# 默认值的形式参数示例
def set_work,mass,cx=0,cy=0,cz=0 # 合法示例
def set_work,mass,cx=0,cy,cz     # 非法示例
```

### 示例

以下是带有 `call` 语句的用户函数调用示例及其结果。我们在前一节中介绍了欧几里得距离的示例以描述子程序。现在，让我们分别定义欧几里得距离和曼哈顿距离的用户函数，并调用它们。

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

# 计算 2D 欧几里得距离
def euclid_dist,x,y
var tmp
tmp=x*x+y*y
var len=sqr(tmp) # 从原点的距离
return len

# 计算 2D 曼哈顿距离
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
# 3.7.4 `jump`

### 描述

此格式与 `call` 语句完全相同，其动作也与 `call` 语句类似。

唯一的区别是，`call` 语句使用 `end` 语句返回到主程序，而 `jump` 语句则不这样做。

### 语法

```python
jump <作业编号或文件名称> [,参数 1,参数 2,???]
```

### 示例

如果将此示例程序的 `jump` 语句替换为 `call` 语句，则替换后的程序结果如下。当遇到子程序 \(0102\_err\) 的 `end` 时，动作循环将结束。如果执行下一个动作循环，主程序 \(0001\) 将从头开始执行。

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

结果
```python
main job start
sub-program
```
[__SOURCE](3-flowcontrol-subprogram/8-local-global-var/README.md)
# 3.8 本地变量和全局变量

## 
[__SOURCE](3-flowcontrol-subprogram/8-local-global-var/1-local-var.md)
# 3.8.1 局部变量

### 描述

示例仅使用 var 语句定义的局部变量进行描述。局部变量是在一个作业程序中通过 var 语句创建的，并在程序结束后自动销毁。此外，其他程序无法读取或写入它们的值。

### 示例

"main\_v" 是一个仅在 0001.job 中可访问的局部变量，"sub\_v" 是一个仅在 0107.job 中可访问的局部变量。从其他程序尝试访问它会导致错误。

局部变量 "x" 同时在 0001.job 和 0107.job 中定义。在两个程序中分别定义的局部变量 "x" 同名但不同。因此，在子程序 0107 中为变量 "x" 设置的值 5，在返回主程序 0001 后将打印 3，而不是 5。

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
        <p>打印 sub_v # ok
          <br />
        </p>
        <p>打印 main_v # error
          <br />
        </p>
        <p>x=5
          <br />
        </p>
        <p>结束</p>
      </td>
    </tr>
  </tbody>
</table>
[__SOURCE](3-flowcontrol-subprogram/8-local-global-var/2-global-var.md)
# 3.8.2 全局变量

### 描述

另一方面，定义为全局的全局变量始终可以从所有作业程序中访问。如果一个全局变量被定义，它在程序周期通过结束语句或主程序的 R0 \[Enter\] 操作重置时不会被清除。

### 示例

如果全局 x 首次被执行，变量 x 将被创建，并且值将初始化为默认值 0。然后，它将在下一行增加到 1。如果在下一个程序周期再次执行全局 x，它不会再次被定义，值 1 将被保留，因为 x 已经被定义。另一方面，global y=10 将执行定义和赋值，因此当它在下一个程序周期中被执行时，变量 y 的值将重置为 10。

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
        <p> 在 x=2 的情况下
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
        <p>结束
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

因此，如果要将全局变量用作程序循环次数的计数器，则不应在定义时分配任何值。

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
        <p>错误
          <br />
        </p>
        <p>教学
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
        <p>结束
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>正确
          <br />
        </p>
        <p>教学
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>全局计数
          <br />
        </p>
        <p>count=count+1
          <br />
        </p>
        <p>&#x2026;
          <br />
        </p>
        <p>结束</p>
      </td>
    </tr>
  </tbody>
</table>
[__SOURCE](3-flowcontrol-subprogram/8-local-global-var/3-precedence.md)
# 3.8.3 优先级

当存在具有相同名称的局部变量和全局变量时，将优先访问局部变量。例如，在执行 0005.job 时，如下所示，全局变量 x 和局部变量 x 将同时存在。这时，如果读取 x 的值，将读取局部变量。之后，0005.job 返回到 0001.job 时，如果读取 x 的值，将读取全局变量，因为此时只有全局变量存在。

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
# 4. 数组和对象
[__SOURCE](4-array-object/1-array/README.md)
# 4.1 数组
[__SOURCE](4-array-object/1-array/1-1d-array.md)
# 4.1.1 数组

数组是一种变量类型，它在一个名称下收集和存储多个值，并允许通过索引号访问。

数组的定义可以是 `var` 或 `global`，就像其他任何变量一样。

{% hint style="warning" %}
[全局变量中顶层数组的名称是大小写不敏感的，请注意。](../../2-basic-syntax/2-identifier.md)
{% endhint %}


数组的定义和访问格式如下。

|  |  |
| :--- | :--- |
| 定义 | var array name = \[ 值, 值, ...\] |
| 访问 | Array name \[Index\] |

构成数组的值称为 `元素。` 以下示例所示的数组 `distances` 总共有五个元素。索引从 0 开始。`distances` 的元素 0 和元素 1 分别为 10 和 10.5。



以下使用 \[ \] 运算符来读取或写入数组特定元素的值。下面显示了一个定义和访问的对象示例。

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
      <td style="text-align:left">结果</td>
      <td style="text-align:left">
        <p>10</p>
        <p>20.5</p>
      </td>
    </tr>
  </tbody>
</table>

数组中的元素数量可以通过使用 `len()` 函数获得。之前，`len()` 函数被介绍为获取字符串长度的函数。如果将数组作为 `len()` 的参数，它将返回数组中元素的数量。

<table>
  <thead>
    <tr>
      <th style="text-align:left">函数名称</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">使用示例</th>
      <th style="text-align:left">结果</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">len(<b>a</b>)</td>
      <td style="text-align:left">如果 <b>a</b> 是字符串，则返回字符串的长度。如果 <b>a</b> 是数组，则返回数组中的元素数量</td>
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



`for-next` 语句主要用于对数组的所有元素进行某些处理。

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
<p>打印距离[i]</p>
<p>下一个</p>
<p>结束</p>
</td>
</tr>
<tr>
<td style="text-align:left">结果</td>
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



数组中存储的值类型不同没有关系。

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
<td style="text-align:left">结果</td>
<td style="text-align:left">
<p>10</p>
<p>abc</p>
<p>true</p>
</td>
</tr>
</tbody>
<table>
[__SOURCE](4-array-object/1-array/2-md-array.md)
# 4.1.2 多维数组

数组也可以作为数组的元素进行嵌套。访问多维数组的元素时，可以连续使用 `[ ]` 操作符。在以下示例中，`arr_y` 是一个二维数组。 \(1\)

`arr_y[1]` 是索引为 1 的元素数组，即 `["abc", "jqk", "xyz"]`，并将其赋值给新变量 `arr_x`。 \(2\)

所以，`arr_x[1]` 是 `jqk`，而 `arr_y[1][2]` 是 `xyz`，因为它指向 `arr_y[1]` 的 `[2]`。



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
      <td style="text-align:left">结果</td>
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
# 4.1.3 数组构造函数 - `Array()`

仅使用 `[ ]` 符号创建包含数百个元素的数组是很困难的。通过调用构造函数可以创建任意数量的数组。每个元素将初始化为 0。

```python
var name = Array(900)	# 创建一个包含 900 个元素的数组
```

如果指定两个或更多元素，可以创建多维数组。在以下 3 维数组的示例中，`[4]` 是最低维度。

```python
var name = Array(3,2,4)	# 创建 [3][2][4] 数量的三维数组
# [ [[0,0,0,0], [0,0,0,0]], [[0,0,0,0], [0,0,0,0]], [[0,0,0,0], [0,0,0,0]] ]
```
[__SOURCE](4-array-object/1-array/4-array-append.md)
# 4.1.4 `append_arr` 程序用于向数组添加元素

支持版本 V60.32-00

`append_arr` 程序可以用于向数组添加元素

```python
var arr = [1, 2]
append_arr arr, 3   # 添加 3 作为 arr 的元素
print arr       # [1, 2, 3]
```

任何值，包括另一个数组，都可以作为元素添加，因为数组可以包含不同类型的元素。

```python
var arr = [1, 2]
append_arr arr, [3, 4]  # 将 [3, 4] 作为 arr 的元素添加
print arr           # [1, 2, [3, 4]]
```
[__SOURCE](4-array-object/1-array/5-array-extend.md)
# 4.1.5 `extend_arr` 过程将一个数组的所有元素添加到另一个数组

支持版本：V60.32-00

`extend_arr` 过程可用于将一个数组的所有元素添加到另一个数组。

```python
var arr = [1, 2]
var brr = [3, 4]
extend_arr arr, brr
print arr   # [1, 2, 3, 4]
```

它可以像下面这样使用。

```python
var arr = [1, 2]
extend_arr arr, [3, 4, 5]
print arr   # [1, 2, 3, 4, 5]
```
[__SOURCE](4-array-object/2-object.md)
# 4.2 对象

如前所述，发现数组可以存储多个元素值，并通过索引访问。

对象与数组类似，都是存储多个元素值。不同之处在于，对象是通过键访问的，而不是通过索引。此外，键是字符串，而不是数字。

对象的定义方式为 `var` 或 `global`，与其他变量相同。对象的定义和访问格式如下。

|  |  |
| :--- | :--- |
| 定义 | var object name = { key : value, key : value, ...} |
| 访问 | 对象名 键 |




以下是一个定义和访问对象的示例。

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
      <td style="text-align:left">结果</td>
      <td style="text-align:left">210 152.6</td>
    </tr>
  </tbody>
</table>



对象的键必须是标识符格式，但元素的值可以是任何类型，也可以是不同类型。

对象可以包含其他对象或数组作为其元素。同样，数组也可以包含其他数组或对象作为其元素。在以下示例中，“work”是一个对象，包含“size”，这是一个对象，以及“heights”，这是一个数组。

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
        <p>var work = { part_no:3, name: &quot;齿轮&quot;, tested : false</p>
        <p>, size : { x : 150, y : 80 }</p>
        <p>, heights : [ 72.89, 74.91, 81.03, 87.60, 87.11 ] }</p>
        <p>print work.tested, work.size.y, work.heights[3]</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">结果</td>
      <td style="text-align:left">false, 80, 87.600000</td>
    </tr>
  </tbody>
</table>
[__SOURCE](4-array-object/3-array-object-assignment.md)
# 4.3 数组和对象的复制赋值

如果赋值语句的右侧包含对象变量，则所有变量的整个值将被复制到左侧的变量。当一个数组或对象以复杂的方式包含子数组和子对象作为元素值时，这种包含结构将被复制，这称为深拷贝。

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
      <td style="text-align:left">结果</td>
      <td style="text-align:left">[10, 20]</td>
    </tr>
  </tbody>
</table>

![](../_assets/image.png)
[__SOURCE](4-array-object/4-call-by-reference-call-by-value.md)
# 4.4 通过引用调用和通过值调用

在第3.4节中给出的`call`语句和`jump`语句的描述中，解释了形式参数和实际参数的概念。当实际参数被传送到子程序时，如果子程序在更改参数的值后结束，这种更改会反映到主程序中吗？

例如，假设一个子程序`0005_pow3.job`将一个值提升到三次方，如下所示：

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
      <td style="text-align:left">结果</td>
      <td style="text-align:left">2</td>
    </tr>
  </tbody>
</table>

虽然我们预期输出为8，因为2x2x2是8，但结果是2。这是因为，当数字类型的实际参数传输到子程序时，值会作为参数被复制。换句话说，在\(1\)中，因为赋值给复制版本的是三次方的值，所以没有影响到原参数x的值。

因此，教学程序应该进行修正，以便通过返回语句传输结果值。



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
        <p>返回 p
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">结果</td>
      <td style="text-align:left">8</td>
    </tr>
  </tbody>
</table>

另一方面，对于数组或对象，将传递实际参数的引用，而不是复制的版本。引用指的是参数的位置。

在以下示例中，子程序 0006\_pow3.job 将数组的每个元素提高到三次方，实际参数数组的元素值会发生变化。



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
        <p>调用 0006_pow3,x
          <br />
        </p>
        <p>打印 x
          <br />
        </p>
        <p>结束
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
        <p>变量 t
          <br />
        </p>
        <p>对于 i=0 到 len(arr)-1
          <br />
        </p>
        <p>t=p[i]
          <br />
        </p>
        <p>p[i] = t*t*t
          <br />
        </p>
        <p>下一个
          <br />
        </p>
        <p>结束
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">结果</td>
      <td style="text-align:left">[27, 8, 64]</td>
    </tr>
  </tbody>
</table>

当调用子程序时，如果实际参数的复制值被传输，则称为按值调用；如果传输的是引用，则称为按引用调用。是否为按值调用或按引用调用由以下的值类型决定：

|  |  |
| :--- | :--- |
| 按值调用 | 布尔值、数字和字符串类型 |
| 按引用调用 | 数组和对象类型 |

![](../_assets/image_3.png)
[__SOURCE](5-moving-robot/README.md)
# 5. 使用机器人语言移动机器人

在理解了表示机器人目标位置的姿势之后，让我们学习移动机器人的命令。
[__SOURCE](5-moving-robot/1-pose.md)
# 5.1 姿态

姿态是嵌入在 ${cont_model} 控制器中的对象类型，表示机器人的每个轴或工具尖端的笛卡尔坐标和方向。

姿态通过调用构造函数 `Pose()` 创建。所有函数参数都是位置参数。第一个字符串元素被识别为 `format`，第二个字符串元素被识别为 `config`。其余元素都是数字类型。

### format
多个子元素包括坐标系统，使用分号（;）分隔。每个子元素都是可选的，可以以任何顺序出现。

<table>
  <tr>
    <th>子元素名称</th>
    <th>类型</th>
    <th>描述</th>
  </tr>
  <tr>
    <td>crd</td>
    <td>字符串</td>
    <td>坐标系统.<br>如果省略，则使用关节坐标系统.<br>请参见下表。</td>
  </tr>
  <tr>
    <td>sync(p1,p2)</td>
    <td>p1, p2 : 实数</td>
    <td>传感器同步（1或2个位置值）</td>
  </tr>
  <tr>
    <td>mi(mech#[, ...])</td>
    <td>每个机械编号 : 整数 0~7</td>
    <td>机制配置.<br>（mi代表 mech.info.）<br>如果省略，则包含所有机制。</td>
  </tr>
</table>

格式示例；
```python
"base,mi(0,2)" # 基础坐标，包含机械 0 和 2
"" # 坐标省略（关节），没有传感器同步，机制信息省略（所有机械）
"sync(20.5,-12.0),robot" # 传感器同步（pos.1=20.5, pos.2=-12.0），机器人坐标。
```

{% hint style="info" %}
cfg 元素指定机器人配置。有关更多信息，请参阅 ${cont_model} 机器人控制器操作手册中的 "[2.3.2.2 基础和机器人记录坐标](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/2-operation/3-step/2-step-pose-modify/2-base-robot-crd-sys?cont_model=${cont_model})"。
{% endhint %}



```python
var <pose variable name> = Pose(j1, j2, j3, ...)		# 轴坐标
var <pose variable name> = Pose(x, y, z, rx, ry, rz, j7, j8,..., crd, cfg)		# 基础坐标。
```
参考以下创建姿势的示例，适用于6轴加1额外轴，以及笛卡尔坐标加1额外轴。

```python
var po1 = Pose(10, 90, 0, 0, -30, 0, -1240.8)				# axis coordinate
var po2 = Pose(1850, 0, 2010.5, 0, -90, 0, -1240.8, "base", "fl;r2")	# base coord.
var po3 = Pose(-1140.8, "mi(2)")	# joint coord., mech. 2
```

另外，姿势构造函数可以通过单个数组或字符串参数调用。通过此方法，可以将文件或数据转换为姿势，通过远程通信获取并使用。

```python
var <pose variable name> = Pose(array)
var <pose variable name> = Pose(string)
```

参考以下示例。

```python
var arr = [10, 90, 0, 0, -30, 0, -1240.8]
var str = "[1850, 0, 2010.5, 0, -90, 0, -1240.8, \"base\", \"fl;r2\"]"
var po3 = Pose(arr)
var po4 = Pose(str)
```

可以通过以下键访问姿势对象的元素。



<!--![](../_assets/image_5.png)-->

<table>
  <tr>
    <th>键</th>
    <th>类型</th>
    <th>值范围</th>
    <th>描述</th>
    <th>单位，备注</th>
  </tr>
    <tr>
    <td>nj</td>
    <td>整数</td>
    <td>1~32</td>
    <td>轴数量</td>
    <td> </td>
  </tr>
   </tr>
    <tr>
    <td>j1~j32</td>
    <td>实数</td>
<td>8字节实数</td>
<td>轴值</td>
<td>毫米，度</td>
</tr>
</tr>
<tr>
<td>x, y, z</td>
<td>实数</td>
<td>8字节实数</td>
<td>工具在笛卡尔坐标中的位置</td>
<td>毫米</td>
</tr>
</tr>
<tr>
<td>rx, ry, rz</td>
<td>实数</td>
<td>8字节实数</td>
<td>工具方向的欧拉角</td>
<td>度</td>
</tr>
<tr>
<td rowspan="4">crd</td>
<td rowspan="4">字符串</td>
<td>关节</td>
<td>关节坐标（默认）</td>
<td rowspan="4"></td>
</tr>
<tr>
<td>基座</td>
<td>基座坐标</td>
</tr>
<tr>
<td>机器人</td>
<td>机器人坐标</td>
</tr>
<tr>
<td>u1 ~ u10</td>
<td>用户坐标</td>
</tr>
<tr>
<td rowspan="8">cfg</td>
<td rowspan="8">字符串</td>
<td>s</td>
<td>|S|>=180</td>
<td rowspan="7">可以通过<br>用";"分割来进行组合<br><br>默认情况下所有标志均关闭。</td>
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
    <td>后</td>
  </tr>
  <tr>
    <td>dn</td>
    <td>下</td>
  </tr>
  <tr>
    <td>nf</td>
    <td>非翻转</td>
  </tr>
  <tr>
    <td>auto</td>
    <td>自动 (自动决策)</td>
    <td></td>
  </tr>
  <tr>
    <td>mechinfo</td>
    <td>整数</td>
    <td>-1 ~ 255</td>
    <td>位字段<br>(bit0:M0, bit1:M1, .... bit7:M7)<br>-1表示所有机械。</td>
    <td>仅对应于包含机制的位被设置为1。</td>
  </tr>
  <tr>
    <td>nsync</td>
    <td>整数</td>
    <td>0~2</td>
    <td>传感器同步的数量</td>
    <td></td>
  </tr>
  <tr>
    <td>sync</td>
    <td>字符串 (p1, p2; 整数)</td>
    <td>sync(p1,p2)</td>
    <td>传感器同步值</td>
    <td>sync(220.5,195.3)</td>
  </tr>
</table>


1. 对于 V60.06-06 或更早版本，`fl` 为 `非翻转`。
姿态元素值可以通过以下示例访问。

```python
po1.j2 = po1.j2 + 5
print po2.z, po2.cfg
```
[__SOURCE](5-moving-robot/2-shift.md)
# 5.2 移动

移动是嵌入在 ${cont_model} 控制器中的对象类型，表示姿态的变化值。

通过调用构造函数 `Shift()` 创建移动。所有函数参数均为位置参数。同时，`crd` 和 `cfg` 为字符串类型，其他为数字类型。

```python
var <shift variable name> = Shift(j1, j2, j3, ...)				# 轴坐标
var <shift variable name> = Shift(x, y, z, rx, ry, rz, j7, j8,..., crd)		# 基座坐标
```

请参阅以下创建 6 轴 + 1 额外轴和笛卡尔 + 1 额外轴的移动示例。

```python
var sft1 = Shift(30, 0, 0, 0, -5.8, 0, -120)				# 轴坐标
var sft2 = Shift(0, 0, 55.2, 0, -5, 0, -120, "base")			# 基座坐标
```

另外，构造函数 shift 也可以通过单个数组或字符串参数调用。通过此方法，可以将文件或数据转换为移动，通过远程通信获取并使用。

```python
var <shift variable name> = Shift(array)
var <shift variable name> = Shift(string)
```

请参考以下示例。

```python
var arr = [30, 0, 0, 0, -5.8, 0, -120]
var str = "[0, 0, 55.2, 0, -5, 0, -120, \"base\"]"
var sft3 = Shift(arr)
var sft4 = Shift(str)
```

可以通过以下键访问移动对象的元素。

![](../_assets/image_7.png)
[__SOURCE](5-moving-robot/3-pose-expression.md)
# 5.3 位姿表达

结果值成为位姿的表达式被称为 `位姿表达式`。

以下所有形式被识别为位姿。

```python
位姿
位姿+偏移
位姿-偏移
位姿+偏移+偏移+...
```

请参考以下将位姿表达式的结果赋值给另一个位姿变量的示例。

```python
var po1 = Pose(10, 90, 0, 0, -30, 0)
var po2 = Pose(1850, 0, 2010.5, 0, -90, 0, "base", "fl;r2")
var po3 = cpo("robot")
var sft1 = Shift(30, 0, 0, 0, -5.8, 0)
var po4 = po1-sft1
var po5 = po2+sft1+Shift(0, 0, 55.2, 0, -5, 0, "base")
```
[__SOURCE](5-moving-robot/4-move.md)
# 5.4 `移动 (move)`

`移动 (move)` 语句是用于移动机器人的过程。格式如下。

### 描述

机器人的工具尖端移动到姿态位置。

### 语法

move &lt;插值&gt;, \[tg=&lt;姿态/偏移&gt;\], spd=&lt;速度&gt;, accu=&lt;精度&gt;

, tool=&lt;工具编号&gt; \[x=&lt;赋值语句&gt;,\] \[直到 &lt;条件表达式&gt;\]

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">插值</td>
      <td style="text-align:left">
        <p>P: 轴插值;</p>
        <p>L: 线性插值;</p>
        <p>C: 圆形插值;</p>
        <p>SP: 静态轴插值;</p>
        <p>SL: 静态工具线性插值;</p>
        <p>SC: 静态工具圆形插值</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">姿态/偏移</td>
      <td style="text-align:left">
        <p>要移动到的目标姿态（pose）</p>
        <p>如果存在隐藏姿态，将被省略。</p>
        <p>如果以 + 或 - 符号指定了偏移表达式，将会应用（隐藏姿态 + 
          偏移表达式）作为目标姿态。</p>
      </td>
      <td style="text-align:left">姿态表达式或带符号的偏移表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">速度</td>
      <td style="text-align:left">
<p>工具尖端的移动速度</p>
<p>应该添加一个单位（mm/秒，cm/分钟，秒，%）。</p>
</td>
<td style="text-align:left">算术表达式</td>
</tr>
<tr>
<td style="text-align:left">准确性</td>
<td style="text-align:left">
<p>算术表达式</p>
<p>值越低，越准确。如果为0，则操作将不连续地发生。</p>
</td>
<td style="text-align:left">0~7</td>
</tr>
<tr>
<td style="text-align:left">工具编号</td>
<td style="text-align:left">机器人操作时使用的工具编号</td>
<td style="text-align:left">0~31</td>
</tr>
<tr>
<td style="text-align:left">赋值语句</td>
<td style="text-align:left">
<p>当移动开始时，将按从左到右的顺序执行赋值语句。</p>
</td>
<td style="text-align:left">如果不为0则为真，如果为0则为假
<p>"&lt;赋值语句1;赋值语句2;...&gt;"<\p>
</td>
</tr>
<tr>
<td style="text-align:left">条件表达式</td>
<td style="text-align:left">
<p>一旦条件表达式为真，机器人操作将结束，指定的姿势将被视为已达到。</p>
<p>条件表达式的结果可以通过result()函数获得。</p>
</td>
<td style="text-align:left">如果不为0则为真，如果为0则为假</td>
</tr>
</tbody>
</table>

### 示例

```python
move L,tg=po[0]+sft[1],spd=800mm/sec,accu=0,tool=1
move P,tg=+Shift(0,0,0,0,-10,0),spd=80%,accu=1,tool=3,x="do1=1;do2=2",until di2  (hidden pose)
if result() then *sensor_on
```
如果按下教学挂件的 `[Record]` 按钮，隐式姿态类型的 `移动 (move)` 语句将记录为当前机器人位置。通过将光标放在 `移动 (move)` 语句上并按下 `[Property]` 按钮，可以检查或编辑隐式姿态值。 

当按下 `[Command]` 按钮并打开 `[Motion]` 组时，选择移动菜单。因此，录制了一条姿态类型的 `移动 (move)` 语句。
[__SOURCE](5-moving-robot/5-mkucs.md)
# 5.5 `mkucs` - 创建用户坐标系

### 描述

一个创建用户坐标系的命令，使用三个姿态或一个姿态。

- 当使用三个姿态创建时，按照指定的步骤顺序创建原点姿态、轴姿态和平面姿态。
- 如果没有指定步骤顺序，则使用原点姿态、X轴姿态和XY平面姿态进行创建。
- 当使用一个姿态创建时，创建原点姿态，位置/方向基于姿态值。
- 如果无法进行计算，则作业执行会由于错误而中断。

### 语法

```python
<result variable> = mkucs(<user coord. system number>,<step order>,<origin pose>,<axis pose>,<plane pose>)
or
<result variable> = mkucs(<user coord. system number>,<origin pose>)
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">result variable</td>
      <td style="text-align:left">
        后台执行的结果<br>
        <ul>
        <li>0: 成功完成。</li>
        <li>-1: 创建用户坐标系失败。</li>
        </ul>
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">user coord. system number</td>
      <td style="text-align:left">
        要创建的用户坐标系的编号
      </td>
      <td style="text-align:left">[1~20]</td>
    </tr>
    <tr>
      <td style="text-align:left">步骤顺序</td>
      <td style="text-align:left">
        如果未指定，以下三个姿势的顺序将为"OXY" <br>
        （示例） <br>
        "OXY" : 原点姿势, X 轴姿势, XY 平面姿势 <br>
        "OYZ" : 原点姿势, Y 轴姿势, YZ 平面姿势 <br>
      </td>
      <td style="text-align:left">字符串变量</td>
    </tr>
    <tr>
      <td style="text-align:left">原点姿势</td>
      <td style="text-align:left">
        位于原点的姿势
      </td>
      <td style="text-align:left">姿势变量</td>
    </tr>
    <tr>
      <td style="text-align:left">轴姿势</td>
      <td style="text-align:left">
        位于 X、Y、Z 轴上的姿势
      </td>
      <td style="text-align:left">姿势变量</td>
    </tr>
    <tr>
      <td style="text-align:left">平面姿势</td>
      <td style="text-align:left">
        位于 XY、YZ、ZX 平面上的姿势
      </td>
      <td style="text-align:left">姿势变量</td>
    </tr>
  </tbody>
</table>

### 返回值


<table>
  <thead>
    <tr>
      <th style="text-align:left">值</th>
      <th style="text-align:left">含义</th>
      <th style="text-align:left">其他</th>
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


### 错误

- E14613 : 当实际参数与形式参数不匹配时发生。请检查实际参数。
- E14614 : 当用户坐标编号不是数字时发生。请重新指定用户坐标编号。
- E14615 : 当用户坐标编号不是1到20之间的数字时发生。请更改用户坐标编号。
- E1011 : 当教学姿势之间的距离太近时发生。当每个点之间的距离小于1mm时发生。请纠正姿势之间的距离值。
- E1012 : 当三个调用的姿势在一条直线上时发生。


### 示例

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
# 5.6 `selucrd` - 选择用户坐标系统

`selucrd` 语句是一个用于更改指定为条件设置中的用户坐标系统的用户坐标系统编号的过程。

### 描述

与在条件设置中指定用户坐标系统相对应的功能。

### 语法

```python
selucrd <坐标系统编号>
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">坐标系统编号</td>
      <td style="text-align:left">
        要选择的坐标系统编号<br>
        <ul>
        <li>0：取消指定用户坐标系统</li>
        <li>1~20：指定用户坐标系统</li>
        </ul>
      </td>
      <td style="text-align:left">表达式</td>
    </tr>
  </tbody>
</table>

### 示例

```python
   selucrd 1
   end
```
[__SOURCE](5-moving-robot/7-contpath.md)
# 5.7 `contpath`

### 描述

选择 CONTPATH 的模式。

请参阅下面的链接以获取 CONTPATH 的描述。
[操作手册：8.15 手动设置 CONTPATH](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/8-r-code/15-r360?cont_model=${cont_model})

<br><br>

### 语法

```python
contpath <mode number>
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">mode number</td>
      <td style="text-align:left">
        0: 不连续<br>
        1: 连续。然而，输入信号是不连续的（默认）<br>
        2: 连续。输入信号也是连续的
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### 示例

```python
contpath 0
contpath 1
contpath 2
```
{% hint style="info" %}

- 如果`contpath`语句没有被明确执行，则默认使用`contpath 1`。即使明确指定，它在循环开始时也会初始化为`contpath 1`。

- 可以通过标题栏上的`CP0` / `CP1` / `CP2`标志检查状态变化。

{% endhint %}
[__SOURCE](5-moving-robot/8-coldet.md)
# 5.8 `coldet`

机器人语言 `coldet` 用于在功能激活时设置每个轴的碰撞检测级别。

用户应在 TP 菜单中设置功能激活开/关和碰撞级别。`[F2: 系统] - 3: 机器人参数 - 14: 碰撞检测 - 2: 设置碰撞检测（每个轴） ([F2: System] - 3: robot parameter - 14: impact detection - 2: set the collision detection (of each axis))`

该菜单可以显示机器人的碰撞检测设置。

如果功能已启动，默认检测级别为 1。

在手动模式下，默认级别也是相同的。

---

### 描述
* 设置碰撞检测级别 


### 语法 
```python
coldet LV=<level> 
```

### 参数 
* 级别的值可以设置为 0 到 16（0: 关闭）

### 示例 

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
* 第 1 步和第 2 步中的检测级别值为 1。
* 第 3 步的检测级别值为 2，第 4 步和第 5 步的级别值为 3。
* 在第 6 步和第 7 步中，碰撞检测功能被禁用。 
--- 
[__SOURCE](5-moving-robot/9-colsense.md)
# 5.9 `colsense` 

机器人语言 `colsense` 用于在功能激活时设置检测灵敏度。

用户应在 TP 菜单中设置功能激活开关和检测灵敏度。`[F2: 系统] - 3: robot parameter - 14: impact detection - 1: Model-based collision detection ([F2: System] - 3: robot parameter - 14: impact detection - 1: Model-based collision detection)`。

---

### 描述
* 可以设置一般碰撞检测灵敏度
* 可以设置每个轴的碰撞检测灵敏度

### 语法 
```python
colsense general,sensitivity=<一般灵敏度>  
colsense axis,id=<关节编号>,criteria=<每个轴灵敏度> 
```

### 参数 
* 一般阈值范围从 0 到 200，值越大灵敏度越高。(0:0ff,1~200)
* 参数 "id" 设置为关节编号。(1~6)  
* 轴阈值范围从 0 到 100，值越小灵敏度越高。(0:0ff,1~100)"

### 示例 

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
* 步骤 1 和步骤 2 的检测灵敏度值来自于菜单 `[F2: 系统] - 3: robot parameter - 14: impact detection - 1: Model-based collision detection ([F2: System] - 3: robot parameter - 14: impact detection - 1: Model-based collision detection)` 中的设置。
* 步骤 3 中的一般灵敏度为 150，在步骤 4 和步骤 5 中更改为 200 
* 关节 1 和关节 2 上的碰撞检测已被停用，其他关节的碰撞通过一般灵敏度 200 进行检测。  

--- 
{% hint style="info" %}

每个轴的最终灵敏度值与每个轴的灵敏度值成正比，与一般灵敏度值成反比。 
{% endhint %}

[__SOURCE](5-moving-robot/10-softxyz.md)
# 5.10 `softxyz`

`softxyz` 函数是一种无传感器的力控制功能，允许机器人在用户定义的条件下在笛卡尔空间中灵活移动以响应外部力量。

为确保正确操作，`工具数据和附加负载信息必须正确配置`。

{% hint style="warning" %}

由于 `softxyz` 函数是 `无传感器` 的，并且不使用力传感器，  
因此在实现完全平滑和自然运动方面存在 `固有限制`。

然而，通过根据应用环境适当调整 `softxyz_lim` 值，  
您可以在功能限制内实现尽可能平滑的运动。

因为 `softxyz_lim (pos / xnr / vel / thr)` 直接决定机器人如何响应外部力量，  
依据环境、装配过程和工具刚度，`需要进行微调`。

{% endhint %}

### 描述
* 该功能允许机器人在不使用力传感器的情况下，由外部力量在笛卡尔坐标系中位移。

---

### 语法
```python
softxyz on, crd=<reference_coordinate>
softxyz set, dpr=<stiffness>
softxyz off
```

### 参数
- `打开 (on)` : 启动 softxyz 功能  
- `关闭 (off)` : 停止 softxyz 功能  
- `set` : 修改 softxyz 设置  

- `crd` : 外部力位移的参考坐标系  
  - 可用选项：`基础 (base)`，`机器人 (robot)`，`工具 (tool)`，`user_x`

- `dpr` : 刚度值  
  - 范围：`0.0 ~ 2.0`  
  - 较高值 = `更刚性`，在外部力量下位移较少  
  - 默认：`1.0`

```python
softxyz on,  crd="base"     # 基于基础坐标系
softxyz on,  crd="robot"    # 基于机器人坐标系
softxyz on,  crd="tool"     # 基于工具坐标系
softxyz on,  crd="user_1"   # 用户定义的坐标系 #1

softxyz set, dpr=1.0        # 设置刚度 (0.0~2.0, 较高 = 更刚性)
softxyz off                 # 禁用 softxyz 功能
```
### 示例 
> 示例 1) 在允许 X、Y 和 Ry 位移的情况下沿 Z 方向组装
> * 坐标 : 机器人坐标 (crd="robot") <br>
> * 位置 (xnr) 限制 : X 和 Y 方向的范围 [-50,+50](mm)，Ry 方向的范围 [-3,+3] (度) <br>
> * 速度 (vel) 限制 : X 和 Y 方向的最大速度 5(mm/秒)，Ry 的最大速度 3(度/秒)  <br>
> * 力矩 (thr) 限制 : X 方向的阈值 3N，Y 方向的阈值 3N 和 Ry 方向的阈值 1Nm 

```python
S1   move P,spd=100mm/sec,accu=0,tool=0
     delay 2.0   # 在启用 softxyz之前所需
     softxyz_lim xnr, x=50, y=50, ry=3
     softxyz_lim vel, x=5, y=5, ry=3
     softxyz_lim thr, x=20, y=20, ry=3
     softxyz on, crd="robot"

S2   move P,spd=250mm/sec,accu=0,tool=0
     softxyz off
     end
```

> 示例 2) 注射材料处理 
> * 坐标 : 机器人坐标 (crd="robot") <br>
> * 位置 (pos) 限制 : +Y 方向的范围 [0,3]  
(mm)，-Y 方向的范围 [-200,0] (mm) <br>
> * 速度 (vel) 限制 : Y 方向的最大速度 150(mm/秒)<br>

```python
S1   move P,spd=100mm/sec,accu=0,tool=0
     delay 2.0   # 在启用 softxyz之前所需
     softxyz_lim pos, _y=300, y_=200
     softxyz_lim vel, y=150
     softxyz on, crd="robot"

S2   wait ...
     softxyz off
     end
```

--- 
> `信息`
>
> - 在使用 `softxyz on` 之前，您 `必须` 配置 `softxyz_lim` 参数  
>   (`pos`, `xnr`, `vel`, `thr`) 以设置最大位移、速度、  
>   和笛卡尔阈值。
>
> - 为了提高对外部力量的敏感性，建议您  
>   `使用 (保持机器人静止 1-2 秒) 的`delay`命令 ( command)`  
> 在执行 `softxyz on` 之前。
>
> - 如果在 softxyz 操作期间发生振动，建议进行以下调整：
>   1) *增加 `thr` 值*  
>   2) *增加 `dpr` 值*  
>   3) *减少 `vel` 值*
[__SOURCE](5-moving-robot/11-softxyz_lim.md)
# 5.11 `softxyz_lim`

在使用指令 `softxyz on` 之前，用户应设置 `softxyz_lim` 参数，如位置限制(`pos`)、工作空间限制(`xnr`)、速度限制(`vel`)和力阈值限制(`thr`). <br>

--- 

### 描述 
* softxyz_lim 参数设置   

### 语法 
```pythonghlt
softxyz_lim pos,_x=<+X>,x_=<-X>,_y=<+Y>,y_=<-Y>,_z=<+Z>,z_=<-Z> 
softxyz_lim vel,x=<X>,y=<Y>,z=<Z>,rx=<Rx>,ry=<Ry>,rz=<Rz>  
softxyz_lim xnr,x=<X>,y=<Y>,z=<Z>,rx=<Rx>,ry=<Ry>,rz=<Rz> 
softxyz_lim thr,x=<X>,y=<Y>,z=<Z>,rx=<Rx>,ry=<Ry>,rz=<Rz> 
```

### 参数 
* softxyz_lim pos : 基于笛卡尔空间的位置信限制 [mm] <br>
* softxyz_lim vel : 基于笛卡尔空间的最大平移和旋转速度限制 [mm/sec] 或 [deg/sec] 
<br>
* softxyz_lim xnr : 基于笛卡尔空间的工作空间 (位置/旋转) 限制 [mm] 或 [deg] <br>
* softxyz_lim thr : 基于笛卡尔空间的力阈值限制 [N] 或 [Nm] <br>

### 示例
> * 设置位置限制 : +X 方向为 200[mm], -Y 方向为 100[mm], +Z 方向为 300[mm]
```python
softxyz_lim pos, _x=200, y_=100, _z=300
```
> * 设置速度限制 : Z 方向的最大速度为 40[mm/sec] 
```python
softxyz_lim vel, z=40
```
> * 设置工作空间限制 : X 方向的最大位置为 [-200,200][mm]
```python
softxyz_lim xnr, x=200
```
> * 设置扭矩限制 : 扭矩阈值设定为 10[N]
```python
softxyz_lim thr, y=10
```
[__SOURCE](5-moving-robot/12-softjoint.md)
# 5.12 `softjoint`

`softjoint` 指令是无传感器的力控制，允许机器人在关节空间中以用户设定的外部力量为参考进行顺应移动。 <br>

用户应检查机器人工具和附加轴信息的有效性，以提高功能准确性。 <br>



--- 

### 描述 
* 在不使用传感器的情况下，以用户设定的环境中外部力量为参考，在关节空间中顺应移动。 


### 语法 
```python
softjoint on
softjoint off  
```

### 参数
* on : 功能开始
* off : 功能结束 



--- 
{% hint style="info" %}

* 在使用 `softjoint on` 之前，用户应设置 softjoint_lim 参数，例如关节号 (`字母j (j)`)、柔软度 (`sft`)、关节角度限制 (`ang`) 和扭矩阈值 (`thr`)。

* 为了提升无传感器力控制性能，用户应该在 `softjoint on` 之前设置 `延迟 (delay)` 命令为 `delay 1.0`。  

{% endhint %}
[__SOURCE](5-moving-robot/13-softjoint_lim.md)
# 5.13 `softjoint_lim`

在使用指令 `softjoint on` 之前，用户应设置 `softjoint_lim` 参数，例如关节编号（`字母j (j)`）、柔性（`sft`）、关节角度限制（`ang`）和扭矩阈值（`thr`）。 <br>

--- 

### 语法 
```python
softjoint_lim, j=<关节编号>, sft=<柔性>, ang=<关节角度限制>, thr=<扭矩阈值> 
```

### 参数
* j : 关节编号 [1~6]
* sft : 更大的值使移动更柔软 [0:off,0~100]
* ang : 关节角度限制 [度]
* thr : 扭矩阈值 [Nm]


### 示例 
> 示例1）设置关节编号 3(J3) 上的参数 
> * 在 J3 上激活，柔性(50)，关节角度限制 [-30~30] (度) 和扭矩阈值 10(Nm)   
```python
softjoint_lim, j=3, sft=50, ang=30, thr=10
```

> 示例2）设置关节编号 2 和 3(J2, J3) 上的参数
> * 设置柔性 : J2-sft(30), J3-sft(80)  
> * 设置关节角度限制 : J2[-50,+50] (度), J3[最小关节角度限制, 最大关节角度限制] (度) <br>
> * 设置扭矩阈值 : J2-thr(3)(Nm), J3-thr(5)(Nm) 


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

* 使用 `softjoint` 功能时，应设置 `字母j (j)` 和 `sft` 的参数在 `softjoint_lim` 上。如果不设置 `ang` 参数，机器人将在定义的软限制内移动。而扭矩阈值 `thr` 的默认参数值为 0 [Nm]。 

{% endhint %}
[__SOURCE](5-moving-robot/14-external_control.md)
# 5.14 外部控制

### 说明  
* 机器人运动的位置命令由外部设备生成，生成的外部命令通过以太网或串行通信作为字符串数据传输到 ${cont_model} 控制器。 ${cont_model} 控制器接收该命令并控制机器人。 

### 语法  
```python
     global onl_trj
     var msg # 姿态或姿态类型字符串

     onl_trj=online.Traject()
     onl_trj.time_from_start=-1.0
     onl_trj.look_ahead_time=1.0
     onl_trj.interval=0.1
     onl_trj.init
     onl_trj.buf_in msg
 
```

### 参数  
* `time_from_start` : 从起始位置开始经过的时间 (-1: 禁用)  
* `look_head_time` : 机器人移动的时间延迟 (单位 : [s])  
* `interval` : 生成命令之间的时间间隔 (单位 : [s])  
* `init` : 在线轨迹初始化，清除命令缓冲区  
* `buf_in`  : 将姿态或姿态类型字符串添加到命令缓冲区

### 示例  
> 机器人通过接收外部生成的命令通过以太网通信移动。

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
     onl_trj.look_ahead_time=1.0 # 机器人移动开始的延迟时间
     onl_trj.interval=0.1 # 生成命令的采样时间
     onl_trj.init # 缓冲区初始化

     var msg
10   enet0.recv
     str_pose=result()
      if msg == "stop"
       onl_trj.init # 缓冲区清空 (快速停止)
     else
       onl_trj.buf_in msg 
     endif    
     goto 10
     end 
```
--- 
{% hint style="info" %}

* 当前接收的姿态或姿态类型字符串只能采用轴角坐标。
* 姿态字符串只能采用数组格式的轴角坐标（例如 [0.000,90.000,0.000,0.000,-90.000,0.000]）。    

{% endhint %}
[__SOURCE](5-moving-robot/15-convcrd.md)
# 5.15 `convcrd`

### 描述 
* `convcrd` 命令是一个函数指令，用于转换姿态变量的坐标系统。

### 语法 
>* poseA: 要转换的姿态变量。
>* poseB: 转换后的姿态变量。

```python
poseB = poseA.convcrd("base")      # base coordinate
poseB = poseA.convcrd("robot")     # robot coordinate
poseB = poseA.convcrd("tool")      # tool coordinate
poseB = poseA.convcrd("u1")        # user coordinate 1
```

### 示例 
```python
     var pose_A, pose_B
     
     # 关节坐标
     pose_A=Pose(0.00,60.00,0.00,0.00,-30.00,0.00)
     # 基坐标
     pose_B=pose_A.convcrd("base")
```
[__SOURCE](5-moving-robot/16-pose_trans.md)
# 5.16 `pose_trans`

### 描述
* `pose_trans` 命令是一个函数指令，用于将两个位姿变量相乘以获得结果位姿值。

### 语法

```python
poseC = pose_trans(poseA,poseB)
```

### 示例
```python
     var pose_A, pose_B, pose_C
     var pose_inv_B
     var pose_shift
     
     pose_shift=Shift(10.0, 10.0, 10.0, 0.000, 0.000, 0.000, "base")

     # pose_A : (0,60,0,0,-30,0) 
     pose_A=Pose(0.00,60.00,0.00,0.00,-30.00,0.00)
     pose_A=pose_A.convcrd("base")
 
     pose_B=pose_A+pose_shift
     
     # pose_inv_B 是 pose_B 的逆矩阵
     pose_inv_B=pose_B
     pose_inv_B=pose_B.convcrd("base")
     pose_inv_B=pose_inv(pose_B)

     # pose_C 与 pose_A 相同
     pose_C=pose_trans(pose_A,pose_B)
     pose_C=pose_trans(pose_C,pose_inv_B)
          
S1   move P,tg=pose_C,spd=10%,accu=0,tool=0
     
     end
```
[__SOURCE](5-moving-robot/17-pose_inv.md)
# 5.17 `pose_inv`

### 描述

* `pose_inv` 指令是一个将姿态变量转换为与姿态变量的逆矩阵相对应的姿态变量的函数。

### 语法

```python
poseB = pose_inv(poseA)
```

### 示例  
```python
     var pose_A, pose_B, pose_C
     var pose_inv_B
     var pose_shift
     
     pose_shift=Shift(10.0, 10.0, 10.0, 0.000, 0.000, 0.000, "base")

     # pose_A : (0,60,0,0,-30,0) 
     pose_A=Pose(0.00,60.00,0.00,0.00,-30.00,0.00)
     pose_A=pose_A.convcrd("base")
 
     pose_B=pose_A+pose_shift
     
     # pose_inv_B 是 pose_B 的逆矩阵
     pose_inv_B=pose_B
     pose_inv_B=pose_B.convcrd("base")
     pose_inv_B=pose_inv(pose_B)

     # pose_C 与 pose_A 相同
     pose_C=pose_trans(pose_A,pose_B)
     pose_C=pose_trans(pose_C,pose_inv_B)

S1   move P,tg=pose_C,spd=10%,accu=0,tool=0
     
     end
```
[__SOURCE](5-moving-robot/18-axisctrl.md)
# 5.18 `axisctrl`

### 描述
* `axisctrl` 命令指定在执行 `移动 (move)` 命令以移动每个轴时，是否应当额外轴移动到其目标位置。
* 有关 `axisctrl` 声明的详细描述，请参阅以下链接。  
[${cont_model} 控制器功能手册 - 多任务处理](https://hrbook-hrc.web.app/#/view/doc-multi-task/zh/README?cont_model=${cont_model})

### 语法
```python
axisctrl <on/off>,a=<additional axis number>
axisctrl <on/off>,a=[additional axis number, additional axis number, ...]  # 多重指定可能（最多 4 个）
```
[__SOURCE](5-moving-robot/19-smov.md)
# 5.19 `smov`

### 描述
`smov` 语句是用于定位器同步的程序。  
有关 `smov` 语句的详细描述，请参阅以下链接。  
[${cont_model} 控制器功能手册 - 定位器同步](https://hrbook-hrc.web.app/#/view/doc-positioner-sync/zh/README?cont_model=${cont_model})

<br><br>

### 语法
```python
smov S<站点编号>,<插值模式>,tg=<目标位置>,spd=<速度>,accu=<精度>,tool=<工具编号>
smov S<站点编号>,<插值模式>,tg=<目标位置>,spd=<速度>,accu=<精度>,tool=<工具编号> 直到 <输入信号>
```
[__SOURCE](5-moving-robot/20-shift.md)
# 5.20 `shift`

### 描述
`shift` 语句在保持工具方向（工具角度）的同时，转换在 XYZ 坐标系统中已经教好的点。

### 语法
```python
shift crd=<参考坐标>,x=<X 移动值>,y=<Y 移动值>,z=<Z 移动值>
```

### 参数
* crd : 参考坐标系统  
["base": 基础, "robot": 机器人, "tool": 工具, "joint": 关节, "u": 用户]
* x, y, z : X, Y, Z 移动值 [0-3000, mm]

### 示例
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
# 5.21 `shift_lim`

`shift_lim`语句是一个函数，通过设置机器人最大允许偏移量来提高使用偏移功能的安全性。  
如果输入的偏移值超过配置的限制，将产生错误。

### 语法
```python
shift_lim x=<X 偏移限制>, y=<Y 偏移限制>, z=<Z 偏移限制>
```

### 参数
* x, y, z: X, Y, Z 偏移限制值[0~3000,mm]<br><br>

### 错误指南
* E1196: 偏移量超过配置的偏移限制。请减少偏移量或重新调整偏移限制值。

### 示例
```python
     var po1 = Pose(0.691, 99.293, 24.758, -6.528, -48.574, 15.774, 0.000)
S1   move P, tg=po1, spd=10%, accu=0, tool=0
     shift_lim x=120, x=200, z=100
     shift crd="base", x=-150, y=70, z=10  # 偏移限制超出错误发生
S2   move P, tg=po1, spd=10%, accu=0, tool=0
     end
```
[__SOURCE](6-external-comm/README.md)
# 6. 与外部设备通信
[__SOURCE](6-external-comm/1-fb-io/README.md)
# 6.1 `FB` 对象：数字 I/O

数字输入/输出 \(I/O\) 可以通过 10 个可以从 HRScript 访问的 `FB` 对象进行。`FB` 代表现场总线块，每个 `FB` 对象被设置为映射到安装在机器人控制器中的 I/O 硬件，并包含输入和输出变量作为元素。
[__SOURCE](6-external-comm/1-fb-io/1-io-val.md)
# 6.1.1 输入/输出变量

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.tg-kftd{background-color:#efefef;}
</style>

<table>
<thead>
  <tr>
    <td colspan="3"></td>
    <td>类型</td>
    <td>值范围</td>
  </tr>
</thead>
<tbody> 
  <tr>
    <td rowspan="10">fb0 ~ fb9</td>
    <td rowspan="5">数字输出</td>
    <td>do[0~959] <br>
    dob[0~119].x[0~7] <br>
    dow[0~118].x[0~15] <br>
    dol[0~116].x[0~31] </td>
    <td>位</td>
    <td>0, 1</td>
  </tr>
  <tr>
    <td>dob[0~119]</td>
    <td>有符号 1字节整数</td>
    <td>-128 ~ +127</td>
  </tr>
  <tr>
    <td>dow[0~118]</td>
    <td>有符号 2字节整数</td>
    <td>-32768 ~ +32767</td>
  </tr>
  <tr>
    <td>dol[0~116]</td>
    <td>有符号 4字节整数</td>
    <td>-2147483648 ~ +2147483647</td>
  </tr>
  <tr>
    <td>dof[0~116]</td>
    <td>有符号 4字节实数</td>
    <td>3.4E+/-38 (7 位有效数字)</td>
  </tr>
  <tr>
    <td rowspan="5">数字输入</td>
    <td>di[0~959] <br>
    dob[0~119].x[0~7] <br>
    dow[0~118].x[0~15] <br>
    dol[0~116].x[0~31] </td>
    <td>位</td>
    <td>0, 1</td>
  </tr>
  <tr>
    <td>dib[0~119]</td>
    <td>带符号 1字节 整数</td>
    <td>-128 ~ +127</td>
  </tr>
  <tr>
    <td>diw[0~118]</td>
    <td>带符号 2字节 整数</td>
    <td>-32768 ~ +32767</td>
  </tr>
  <tr>
    <td>dil[0~116]</td>
    <td>带符号 4字节 整数</td>
    <td>-2147483648 ~ +2147483647</td>
  </tr>
  <tr>
    <td>dif[0~116]</td>
    <td>带符号 4字节 实数</td>
    <td>3.4E+/-38 (7 个有效数字)</td>
  </tr>
</tbody>
</table>

<br><br>

在 `do`、`dob`、`dow`、`dol` 和 `dof` 中，后缀 `b`、`w`、`l` 和 `字母f (f)` 分别表示 `字节`、`字`、`长` 和 `浮动 (float)`，且均为带符号值。这些不是单独的内存空间，而是代表同一个 960 字节的空间，只是数据类型不同。例如，`do[1~16]`、`dob[1~2]` 和 `dow[1]` 都是相同的输出信号。

![](../../_assets/image_2.png)

如果将值分配给以 `do` 开头的输出变量，则将执行 I/O 信号输出。可以通过读取以 `di` 开头的输入变量值来获取当前输入的 I/O 信号。`do` 变量可以被读写，但 `di` 变量只能被读取。

`FB` 对象名称可以省略，如下所示。

| **对象名称** | **do 记法** | fb.do 记法 |
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
# 6.1.2 示例

请参考以下使用示例。

```python
do2=1		# 打开 fb0 的编号0的位输出值
fb2.dob3=0b00001111  	# 将 fb2 的第3个字节输出值指定为二进制位字符串
fb[4].dob1=0x0F  	# 打开 fb4 的第1个字节输出值的最低4位，并关闭最高4位
var work_no=fb9.dib3    # 将 fb9 的第3个字节输入值分配给 work_no 变量
if fb5.di43 then *err  	# 当 fb5.di42 被打开时，分支到 *err 标签
for idx=21 to 29
  fb3.do[idx]=1  	# 打开 fb3 的所有输出信号 do21 ~ do29 
next
fb2.do3=fb2.do7=fb2.do11=1   # 一次性打开 fb2 的第3、第7和第11个输出信号
```
[__SOURCE](6-external-comm/1-fb-io/3-fn-io.md)
# 6.1.3 `fn` 对象

您可以通过指定 `fb` 对象的特定区域来定义 `fn` 对象。
如果 ${cont_model} 控制器是现场总线主设备，并且有多个现场总线从设备，您可以将每个从设备的区域设置为每个 `fn` 对象，以直观地处理这些从设备。

![](../../_assets/io/io_fn.png)

有关如何设置 `fn` 区域的说明，请参见以下链接。

[操作手册：fn 块分配](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/7-system/3-control-parameter/2-io-signal-setting/12-fn-block?cont_model=${cont_model})

&nbsp;

`fn` 的语法与 `fb` 相同。
`fn` 索引范围为 0 到 63，位索引范围为 0 到 959，与 `fb` 一样。
也就是说，最大可配置索引为 fn0.do0 到 fn63.do959。

当访问未配置的不存在的 `fn` 对象或访问超出 `fn` 设置范围的 do/di 时，会发生错误。

请参见以下用例；



```python
fn2.dob3=0b00001111  	# 将 fn2 的输出字节 3 设置为二进制位
fn[4].dob1=0x0F  	# 打开 fn4 的输出字节 1 的低 4 位，并关闭高 4 位。
var work_no=fn63.dib3    # 将 fn63 的输入字节 3 赋值给 work_no 变量
if fn5.di43 then *err  	# 当 fn5.di42 打开时分支到 *err 标签。
for idx=21 to 29
  fn3.do[idx]=1  	# 打开 fn3 的所有输出信号 do21 ~ do29。
next
fn2.do3=fn2.do7=fn2.do11=1   # 同时打开 fn2 的输出信号 3、7 和 11。
```
[__SOURCE](6-external-comm/1-fb-io/4-pulse.md)
# 6.1.4 `pulse`

`pulse`语句是脉冲类型信号输出的过程。

### 描述

在延迟时间经过后，它以On(高)状态输出cnt次，持续ton时间，然后以Off(低)状态持续toff时间。

### 语法

```python
pulse <Signal>,tlag=<Lag time>,ton=<On time>,toff=<Off time>,cnt=<output count>
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">信号</td>
      <td style="text-align:left">
        要以脉冲形式输出的信号名称<br>
        (仅支持fb.do信号。)
      </td>
      <td style="text-align:left">输出信号</td>
    </tr>
    <tr>
      <td style="text-align:left">延迟时间</td>
      <td style="text-align:left">
        执行该过程后，脉冲信号开始前的等待时间<br>
        (0.0 ~ 100.0[秒])
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">开启时间</td>
      <td style="text-align:left">
        输出信号在On(高)状态下的持续时间<br>
        (0.0 ~ 100.0[秒])
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
<tr>
      <td style="text-align:left">关闭时间</td>
      <td style="text-align:left">
        关闭（低）状态时输出信号的时间<br>
        （0.0 ~ 100.0[秒]）
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">输出次数</td>
      <td style="text-align:left">
        重复脉冲周期的次数
        （0 ~ 1000）
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
  </tbody>
</table>

### 示例

```python
   pulse do10,tlag=0.0,ton=1.5,toff=0.5,cnt=5
   end
```
[__SOURCE](6-external-comm/2-http_cli/README.md)
# 6.2 `http_cli`模块：HTTP客户端

使用${cont_model}控制器的一般用途以太网端口，可以访问远程 Web 服务并使用 HTTP 服务。  
要使用此功能，请导入`http_cli`模块并创建`HttpCli`对象，如下所示。

```python
import http_cli
var cli = http_cli.HttpCli()
```

创建`HttpCli`对象后，可以通过调用`get`、`put`、`post`和`删除 (delete)`成员过程发出服务请求。<br>  
`HttpCli`对象提供一个名为`body`的属性。<br>  
- 当发出`GET`请求并成功接收响应时，远程服务器返回的数据存储在`body`属性中。<br> `body`值的类型可以是字符串、数字、数组或对象。  
- 发出`PUT`请求时，必须事先将要传输的数据分配给`body`属性。  
- 发出`POST`请求时，传输的数据也必须事先分配给`body`属性，响应中远程服务器返回的数据存储在`body`属性中。  
- `DELETE`服务不使用`body`属性。  
提供的 HTTP 客户端通信在同步模式下操作。
[__SOURCE](6-external-comm/2-http_cli/1-http_cli-creator.md)
# 6.2.1 构造函数 

### 描述

创建一个 `HttpCli` 对象并返回对它的引用。

### 语法


HttpCli\(\)

### 返回值

对新创建对象的引用。

### 示例用法

```python
var cli = http_cli.HttpCli()
```
[__SOURCE](6-external-comm/2-http_cli/2-http_cli-member-var.md)
# 6.2.2 成员变量

<table>
  <thead>
    <tr>
      <th style="text-align:left">变量</th>
      <th style="text-align:left">数据类型</th>
      <th style="text-align:left">描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">body</td>
      <td style="text-align:left">任意</td>
      <td style="text-align:left">
        <p>传输的数据必须在 PUT 和 POST 请求之前分配。<br><br>如果将对象以外的值分配给 `body`，在执行期间 URL 的最后路径段将作为键处理。<br><br>来自 GET 和 POST 请求的响应数据存储在 `body` 中。<br><br>在 HRScript 中，不支持直接访问 `body` 的成员变量。要修改或使用数据，首先将其分配给另一个变量。</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">query</td>
      <td style="text-align:left">对象</td>
      <td style="text-align:left">
        用于需要查询参数的 GET 服务。<br>与 GET 请求一起发送的数据必须提前分配。
      </td>
    </tr>
    <tr>
      <td style="text-align:left">status</td>
      <td style="text-align:left">int</td>
      <td style="text-align:left">
        <p>
            返回 HTTP 响应代码和错误代码。 (请参见 [6.2.4 节，HTTP 通信代码](./4-http_cli-code.md))
          <br/>
        </p>
      </td>
    </tr>
  </tbody>
</table>

<br/>

`body` 和 `query` 都使用对象数据类型。

对象类型以 `{ key: value }` 格式支持。

cli.body = { name: "WORK #32", color: "green", state: "OK" }
cli.query = { axis: 3 }
[__SOURCE](6-external-comm/2-http_cli/3-http_cli-member-proc/README.md)
# 6.2.3 成员程序
[__SOURCE](6-external-comm/2-http_cli/4-http_cli-code.md)
# 6.2.4 HTTP通信代码

* 主要HTTP响应代码 
<table>
  <thead>
    <tr>
      <th style="text-align:left">响应类别</th>
      <th style="text-align:left">响应代码</th>
      <th style="text-align:left">描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2">信息</td>
      <td>
        100
      </td>
      <td>
      继续
      </td>
    </tr>
    <tr>
      <td>
        101
      </td>
      <td>
      切换协议
      </td>
    </tr>
    <tr>
    <tr>
      <td rowspan="5">成功</td>
      <td>
        200
      </td>
      <td>
      成功
      </td>
    </tr>
    <tr>
      <td>
        201
      </td>
      <td>
      已创建
      </td>
    </tr>
    <tr>
      <td>
        202
      </td>
      <td>
      已接受
      </td>
    </tr>
    <tr>
      <td>
        203
      </td>
      <td>
      非权威信息
      </td>
    </tr>
    <tr>
      <td>
        204
      </td>
      <td>
      无内容
      </td>
    </tr>
    <tr>
    <tr>
      <td rowspan="3">重定向</td>
      <td>
        301
      </td>
      <td>
      永久移动
      </td>
    </tr>
    <tr>
      <td>
        302
      </td>
      <td>
      非临时
      </td>
    </tr>
    <tr>
      <td>
        303
      </td>
      <td>
      未修改
      </td>
    </tr>
    <tr>
      <td rowspan="11">客户端错误</td>
      <td>
```html
      </td>
      <td>
      错误的请求
      </td>
    </tr>
    <tr>
      <td>
        401
      </td>
      <td>
      未授权 
      </td>
    </tr>
    <tr>
      <td>
        402
      </td>
      <td>
      需要支付
      </td>
    </tr>
    <tr>
      <td>
        403
      </td>
      <td>
      被禁止 
      </td>
    </tr>
    <tr>
      <td>
        404
      </td>
      <td>
      未找到 
      </td>
    </tr>
    <tr>
      <td>
        405
      </td>
      <td>
      方法不允许
      </td>
    </tr>
    <tr>
      <td>
        407
      </td>
```
```html
<td>
      需要代理身份验证
      </td>
    </tr>
    <tr>
      <td>
        408
      </td>
      <td>
      请求超时
      </td>
    </tr>
    <tr>
      <td>
        410
      </td>
      <td>
      消失  
      </td>
    </tr>
    <tr>
      <td>
        412
      </td>
      <td>
      先决条件失败
      </td>
    </tr>
    <tr>
      <td>
        414
      </td>
      <td>
      请求-URI太长
      </td>
    </tr>
    <tr>
      <td rowspan="5">服务器错误</td>
      <td>
        500
      </td>
      <td>
       内部服务器错误 
      </td>
    </tr>
    <tr>
      <td>
        501
      </td>
```
      未实现
      </td>
    </tr>
    <tr>
      <td>
        503
      </td>
      <td>
      服务不可用
      </td>
    </tr>
    <tr>
      <td>
        504
      </td>
      <td>
      网关超时
      </td>
    </tr>
    <tr>
      <td>
        505
      </td>
      <td>
      不支持的HTTP版本
      </td>
    </tr>
  </tbody>
</table>


* 错误代码（异常）

<table>
  <thead>
    <tr>
    <th style="text-align:left">错误名称</th>
      <th style="text-align:left">错误代码</th>
      <th style="text-align:left">描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>RequestException</td>      
      <td>
        -1
      </td>
      <td>
      处理您的请求时发生了模棱两可的异常。
      </td>
</tr>
    <tr>
      <td> 连接错误</td>
      <td>
        -2
      </td>
      <td>
      如果发生网络问题（例如 DNS 失败、拒绝连接等）
      </td>
    </tr>
    <tr>
    <td> HTTP错误
      <td>
        -3
      </td>
      <td>
      如果 HTTP 请求返回了不成功的状态码，则会发生此错误。
      </td>
    </tr>
    <tr>
    <td>必需 URL</td>
      <td>
        -4
      </td>
      <td>
      进行请求需要一个有效的 URL。
      </td>
    </tr>
    <tr>
    <td>重定向过多</td>
      <td>-5</td>
      <td>
      如果请求超过配置的最大重定向次数，将引发 TooManyRedirects 异常。
      </td>
    </tr>
    <tr>
    <td>超时</td>
      <td>
        -6
      </td>
      <td>
      如果请求超时，将引发 Timeout 异常。
      </td>
    </tr>
    <td>会话无效</td>
      <td>
        -7
      </td>
      <td>
        此错误表示会话无效，因为在处理会话请求时发生了运行时错误。会话无效。此错误在会话请求期间发生运行时错误时出现。
      </td>
    </tr>
    <td>未处理的异常</td>
      <td>
        -8
      </td>
      <td>
        在HTTP请求或响应处理期间发生意外错误（例如，会话创建、请求执行或响应解析），并且不符合任何显式处理的异常。因此，请求结果报告为未处理的异常。
      </td>
    </tr>
    <td>无效的超时</td>
      <td>
        -9
      </td>
      <td>
        当超时值超出5毫秒到15毫秒的范围时。
      </td>
    </tr>
  </tbody>
</table>
[__SOURCE](6-external-comm/3-tp-console-bar/README.md)
# 6.3 使用教学挂件控制台栏的输入/输出
[__SOURCE](6-external-comm/3-tp-console-bar/1-print.md)
# 6.3.1 `print`

### 描述

`print` 语句将字符串打印到教导挂件的导引条上。除了字符串常量外，任何类型的表达式（包括常量和变量）都会被转换为字符串并打印出来。如果指定多个表达式，则每个表达式之间以单个空格字符分隔。

### 语法

```python
print <expression>[,<expression>,<expression>...]
```


### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">expression</td>
      <td style="text-align:left">
        <p>要打印的表达式。<br>
        支持所有类型的布尔值、数字、字符串、数组、对象。
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### 示例

```python
input work_no
input work_no,10
input work_no,10,*timeout
```
[__SOURCE](6-external-comm/3-tp-console-bar/2-input.md)
# 6.3.2 `input`

### 描述

使用 `input` 语句作为教导挂件的按键输入字符串并将其存储在变量中。如果超时未输入，则继续执行以下语句或跳转到超时地址。

### 语法

```python
input <variable>;[,<timeout>,<timeout address>]
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">variable</td>
      <td style="text-align:left">
        <p>接收输入的变量。数字也作为字符串类型输入。如果需要数值，请转换为 int( ) 或 double( ) 函数。
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">timeout</td>
      <td style="text-align:left">最大时间限制</td>
      <td style="text-align:left">0.1~60.0 秒
        <br />
      </td>
    </tr>
    <tr>
      <td style="text-align:left">timeout address</td>
      <td style="text-align:left">超时超过时跳转的地址</td>
      <td style="text-align:left">address</td>
    </tr>
  </tbody>
</table>

### 示例

```python
input work_no
input work_no,10
input work_no,10,*timeout
```
![](../../_assets/image_6.png)
[__SOURCE](6-external-comm/4-modbus/README.md)
# 6.4 Modbus模块：Modbus主站

Modbus主站操作可以在HRScript中执行。有关Modbus通信功能的详细信息，请参阅单独的手册。[${cont_model} 控制器功能手册 - Modbus](https://hrbook-hrc.web.app/#/view/doc-modbus/zh/README?cont_model=${cont_model})
[__SOURCE](6-external-comm/5-sci/README.md)
# 6.5 Sci模块：串行通信

串行通信可以通过 ${cont_model} 控制器的 COM 端口进行。

要使用此功能，您必须创建一个 `Sci` 对象作为全局变量，如下所示。

此外，请确保在使用前检查 `[F2: 系统] - 2. 控制参数 - 3. 串口 ([F2: System] - 2. Control Parameters - 3. Serial Port)` 中的设置规格。

```python
global sci2
sci2=com.Sci(2)
```

创建 `Sci` 对象后，只需调用 `send`、`recv`、`open` 和 `关闭 (close)` 成员程序。

调用 `send` 时，您必须提前输入要发送的字符串。

调用 `recv` 时，它会在成功接收后分配给指定的字符串变量。

调用 open 时，将打开端口。

调用 open 时，将关闭端口。
[__SOURCE](6-external-comm/5-sci/1-sci-creator.md)
# 6.5.1 构造函数

### 描述

为 `Sci` 对象创建一个全局变量。

### 语法

com.Sci(端口号)

### 返回值

创建对象的引用

### 示例

```python
global sci2
sci2=com.Sci(2)
```
[__SOURCE](6-external-comm/5-sci/2-sci-member-proc/README.md)
# 6.5.2 成员过程
[__SOURCE](6-external-comm/5-sci/3-sci-example.md)
# 6.5.3 串行通信示例

``` python
Hyundai Robot Job File; { version: 1.6, mech_type: "", total_axis: -1, aux_axis: -1 }
     
     # 使用构造函数创建 Sci 对象并将其分配给全局变量 
     global sci2
     sci2=sci.Sci(2)   #port no. (com2)
     
     # 清除接收缓冲区
     var ret
     ret=sci2.clr_rbuf()

     # 发送
     sci2.send "test"

     # 接收（选项：当超过 3000ms，转到 *timeout）
     var msg
     sci2.recv msg,3000,*timeout
     print msg

     end

     *timeout
     print "error"
     stop

```
[__SOURCE](7-enet-module/README.md)
# 7 `enet` 模块 : 以太网 TCP/UDP 通信

使用 ${cont_model} 控制器的用户 Ethernet 端口，您可以通过以太网 TCP 或 UDP 通信与外部设备发送和接收字符串或二进制数据。

`enet` 模块可以创建两个对象，`ENet` 和 `BBuf`。`ENet` 提供以太网套接字接口，`BBuf` 用于传输二进制数据。

让我们按照客户端示例和服务器示例来理解如何使用它。随后是每个对象的成员变量和函数的参考指南。
[__SOURCE](7-enet-module/1-exam-client/README.md)
# 7.1 点对点，客户端示例

UDP 点对点 (1:1 通信) 或 TCP 客户端示例程序用于字符串和二进制传输解释。
[__SOURCE](7-enet-module/1-exam-client/1-enet-client-str.md)
# 7.1.1 对等, 客户端示例 - 收发字符串数据

遵循以下步骤：

1. 导入 `enet` 模块后，使用构造函数创建一个 `ENet` 对象。
2. 使用成员变量设置 IP 地址和端口号。
   - `警告：控制器上的端口 50000-50005 是预分配的 lports，无法使用。`
3. 使用 `open` 成员过程打开以太网插座，并使用 `state()` 成员变量检查状态。
\(对于 TCP 通信，打开后还必须调用 `连接 (connect)` 过程。\)
1. 使用 `send` 和 `recv` 成员过程进行收发。
2. 使用 `关闭 (close)` 成员过程关闭通信连接。

<br>

### UDP 对等
```python
     # 1. 导入 enet 模块后，使用构造函数创建一个 ENet 对象
     import enet
     var cli=enet.ENet()

     # 2. 设置 IP 地址和端口号
     cli.ip_addr="192.168.1.172" # 远程 (对手) IP 地址
     cli.lport=51001 # 本地 (自己) 端口
     cli.rport=51002 # 远程 (对手) 端口
     # (端口号 49152-65535（除了 50000-50005）包含动态或私有端口)

     # 3. 打开以太网插座
     cli.open
     
     print cli.state() # 如果值为 1，则正常。

     # --------------------------------
     # 4-1. 字符串发送
     cli.send "hello, peer.\n"

     # 4-2. 字符串接收
     #     (如果 5 秒内未收到，则跳转到 *TimeOut 标签)
     var msg
     cli.recv 5000, *TimeOut
     var msg=result() # 接收到的字符串
     print msg
     delay 1.0
     # --------------------------------

     # 5. 关闭以太网插座
     cli.close
     print cli.state() # 如果值为 0，则正常。
     delay 1.5
     end

     *TimeOut
     print "超时！"
     cli.close
     end
```
### TCP 客户端
(只有 `lport` 和 `连接 (connect)` 部分与对等网络不同。)
```python
     # 1. 导入 enet 模块后，使用构造函数创建 ENet 对象
     import enet
     var cli=enet.ENet("tcp") # 用于 udp 通信，ENet("udp") / Enet()

     # 2. 设置 IP 地址和端口号
     cli.ip_addr="192.168.1.172" # 远程 (对手) IP 地址
     cli.lport=0 # 本地 (自己) 端口；随机
     cli.rport=51002 # 远程 (对手) 端口
     # (端口号 49152-65535 包含动态或私有端口)

     # 3. 打开以太网套接字
     cli.open
     cli.connect # 连接到服务器。
     print cli.state() # 如果是 1，就可以了。

     # --------------------------------
     # 4-1. 字符串传输
     cli.send "hello, peer.\n"

     # 4-2. 字符串接收
     #     (如果 5 秒内未接收到，跳转至 *TimeOut 标签)
     var msg
     cli.recv 5000, *TimeOut
     var msg=result() # 接收到的字符串
     print msg
     delay 1.0
     # --------------------------------

     # 5. 关闭以太网套接字
     cli.close
     print cli.state() # 如果是 0，就可以了。
     delay 1.5
     end

     *TimeOut
     print "超时！"
     cli.close
     end
```

[__SOURCE](7-enet-module/1-exam-client/2-enet-client-bin.md)
# 7.1.2 点对点，客户端示例 - 发送接收二进制数据

二进制发送接收是通过 `BBuf`（二进制缓冲区）对象执行的。  
（只有发送接收的部分不同，其余与发送接收字符串数据的部分相同。）

发送

1. 创建 `enet.BBuf` 对象。
2. 使用 `BBuf.append()` 函数将所需的二进制数据附加到 `BBuf` 对象。
3. 作为 `ENET.send_bbuf()` 的一个函数发送 BBuf 对象。


接收

1. 创建 `enet.BBuf` 对象。
2. 使用 `ENET.recv_bbuf()` 函数接收二进制数据到 BBuf 对象中。
3. 使用 `BBuf.read_nums()` 函数从 `BBuf` 对象中读取所需的二进制数据。


<br>

### UDP 点对点
```python
     # 1. 导入 enet 模块后，使用构造函数创建 ENet 对象
     import enet
     var cli=enet.ENet()

     # 2. 设置 IP 地址和端口号
     cli.ip_addr="192.168.1.172" # 远程（对手）IP 地址
     cli.lport=51001 # 本地（自身）端口
     cli.rport=51002 # 远程（对手）端口
     # （端口号 49152-65535（除 50000-50005）为动态或私有端口）

     # 3. 打开以太网套接字
     cli.open
     
     print cli.state() # 如果为 1，则正常。

     # 发送 --------------------------------
     # 4-1. 创建 BBuf 对象
     var bbuf=enet.BBuf()

     # （示例二进制数据）
     var arr=[ -3, 0, 1 ]
     
     # 4-2. 将二进制数据附加到 BBuf 对象
     bbuf.clear()
     bbuf.append("s4", arr) # 附加小端有符号 4 字节数据

     # 4-3. 发送 BBuf 对象
     var ret
     ret=cli.send_bbuf(bbuf)

     # 接收 --------------------------------
     # 4-1. 创建 BBuf 对象
     var bbuf2=enet.BBuf()
     
     # 4-2. 接收二进制数据到 BBuf 对象
     #     （如果 3 秒内没有响应，跳转到 *TimeOut 标签）
     cli.recv_bbuf bbuf2,3000,*TimeOut

     # 4-3. 从 BBuf 对象中读取二进制数据。
     var nums=bbuf2.read_nums("U2", 0, 3) # 读取 3 个大端无符号 2 字节数据
     print nums
     # --------------------------------

     # 5. 关闭以太网套接字
     cli.close
     print cli.state() # 如果为 0，则正常。
     delay 1.5
     end

     *TimeOut
     print "超时！"
     cli.close
     end
```
### TCP 客户端
(仅 `lport` 和 `连接 (connect)` 部分与点对点不同。)
```python
     # 1. 导入 enet 模块后，用构造函数创建一个 ENet 对象
     import enet
     var cli=enet.ENet("tcp")

     # 2. 设置 IP 地址和端口号
     cli.ip_addr="192.168.1.172" # 远程 (对手) IP 地址
     cli.lport=0 # 本地 (自己) 端口；随机
     cli.rport=51002 # 远程 (对手) 端口
     # (端口号 49152-65535 包含动态或私有端口)

     # 3. 打开以太网套接字
     cli.open
     cli.connect # 连接到服务器。
     print cli.state() # 如果为 1，表示正常。

     # 发送 --------------------------------
     # 4-1. 创建 BBuf 对象
     var bbuf=enet.BBuf()

     # (样本二进制数据)
     var arr=[ -3, 0, 1 ]
     
     # 4-2. 将二进制数据附加到 BBuf 对象
     bbuf.clear()
     bbuf.append("s4", arr) # 附加小端符号的4字节数据

     # 4-3. 发送 BBuf 对象
     var ret
     ret=cli.send_bbuf(bbuf)

     # 接收 --------------------------------
     # 4-1. 创建 BBuf 对象
     var bbuf2=enet.BBuf()
     
     # 4-2. 将二进制数据接收进入 BBuf 对象
     #     (如果 3 秒内没有响应，则跳转到 *TimeOut 标签)
     cli.recv_bbuf bbuf2,3000,*TimeOut

     # 4-3. 从 BBuf 对象中读取二进制数据。
     var nums=bbuf2.read_nums("U2", 0, 3) # 读取 3 个大端无符号 2 字节数据
     print nums
     # --------------------------------

     # 5. 关闭以太网套接字
     cli.close
     print cli.state() # 如果为 0，表示正常。
     delay 1.5
     end

     *TimeOut
     print "超时!"
     cli.close
     end
```
* 字符串参数如 "s4" 和 "U2" 决定二进制数据格式，例如字节序类型、符号/无符号和字节数。更多信息，请参见 [7.4.2 Supported format](../4-bbuf/2-format.md)。

[__SOURCE](7-enet-module/2-exam-server/README.md)
# 7.2 TCP 服务器示例

TCP 服务器示例程序解释了传输字符串数据和二进制数据的情况。

当 TCP 客户端使用 `connect()` 函数连接到服务器时，TCP 服务器调用 `listen()` 函数并使用 `accept()` 函数等待客户端的连接。

* 同时只允许一个客户端连接。
* 您不需要指定远程端口。

其余的操作与客户端相同。
[__SOURCE](7-enet-module/2-exam-server/1-enet-server-str.md)
# 7.2.1 ethernet TCP 服务器 - 收发字符串数据

按照以下步骤操作：

1. 导入 `enet` 模块后，用构造函数创建一个 `ENet` 对象。
2. 使用成员变量设置 IP 地址和端口号。 (不需要设置远程端口。)
   - `注意：控制器的端口 50000-50005 已被预分配，无法使用。`
3. 使用 `open` 成员过程打开以太网套接字，并调用 `listen()`、`accept()` 函数。通过 `state()` 成员变量检查状态。
4. 使用 `send` 和 `recv` 成员过程进行收发。
5. 使用 `关闭 (close)` 成员过程关闭通信连接。


```python
     # 1. 导入 enet 模块后，用构造函数创建一个 ENet 对象
     import enet
     var svr=enet.ENet("tcp")
     
     # 2. 设置 IP 地址和端口号
     svr.ip_addr="192.168.1.172" # 远程（对手）IP 地址
     svr.lport=51001 # 本地（自我）端口
     # (端口号 49152-65535（不包括 50000-50005）包含动态或私有端口)
     
     # 3. 打开以太网套接字
     svr.open
     var ret
     ret=svr.listen()
     ret=svr.accept() # 等待客户端连接
     print svr.state() # 如果为 1，则正常。
     
     # --------------------------------
     # 4-1. 字符串发送
     svr.send "欢迎，我是一个 TCP 服务器。\n"
     
     # 4-2. 字符串接收
     #     (如果 5 秒内没有接收到，跳转到 *TimeOut 标签)
     svr.recv 5000,*TimeOut
     var msg=result() # 接收到的字符串
     print msg
     delay 1.0
     # --------------------------------
     
     # 5. 关闭以太网套接字
     svr.close
     print svr.state() # 如果为 0，则正常。
     delay 1.5
     end

     *TimeOut
     print "超时！"
     svr.close
     end
```

[__SOURCE](7-enet-module/2-exam-server/2-enet-server-bin.md)
# 7.2.2 ethernet TCP server 示例 - 二进制数据的收发

二进制收发是使用 `BBuf` (二进制缓冲区) 对象进行的。  
(仅收发部分不同，其余与收发字符串数据相同。)

发送

1. 创建 `enet.BBuf` 对象。
2. 使用 `BBuf.append()` 函数将所需的二进制数据附加到 `BBuf` 对象。
3. 将 BBuf 对象作为 `ENET.send_bbuf()` 函数发送。


接收

1. 创建 `enet.BBuf` 对象。
2. 使用 `ENET.recv_bbuf()` 函数将二进制数据接收到 BBuf 对象中。
3. 使用 `BBuf.read_nums()` 函数从 `BBuf` 对象中读取所需的二进制数据。


```python
     # 1. 导入 enet 模块后，使用构造函数创建 ENet 对象
     import enet
     var svr=enet.ENet("tcp")
     
     # 2. 设置 IP 地址和端口号
     svr.ip_addr="192.168.1.172" # 远程 (对方) IP 地址
     svr.lport=51001 # 本地 (自己) 端口
     # (端口号 49152-65535（不包括 50000-50005）包含动态或私有端口)
     
     # 3. 打开以太网套接字
     svr.open
     var ret
     ret=svr.listen()
     ret=svr.accept() # 等待客户端连接
     print svr.state() # 如果是 1，则表示正常。

     # 发送 --------------------------------
     # 4-1. 创建 BBuf 对象
     var bbuf=enet.BBuf()

     # (示例二进制数据)
     var arr=[ -3, 0, 1 ]
     
     # 4-2. 将二进制数据附加到 BBuf 对象
     bbuf.clear()
     bbuf.append("s4", arr) # 附加小端符号-4字节数据

     # 4-3. 发送 BBuf 对象
     ret=svr.send_bbuf(bbuf)

     # 接收 --------------------------------
     # 4-1. 创建 BBuf 对象
     var bbuf2=enet.BBuf()
     
     # 4-2. 将二进制数据接收到 BBuf 对象
     #     (如果 3 秒内没有响应，则跳转到 *TimeOut 标签)
     svr.recv_bbuf bbuf2,3000,*TimeOut

     # 4-3. 从 BBuf 对象中读取二进制数据。
     var nums=bbuf2.read_nums("U2", 0, 3) # 读取 3 个大端无符号-2字节数据
     print nums
     # --------------------------------

     # 5. 关闭以太网套接字
     svr.close
     print svr.state() # 如果是 0，则表示正常。
     delay 1.5
     end

     *TimeOut
     print "超时！"
     svr.close
     end
```
* 字符串参数如 "s4" 和 "U2" 确定二进制数据格式，例如字节序、符号/无符号和字节数。有关更多信息，请参见 [7.4.2 supported format](../4-bbuf/2-format.md)。
[__SOURCE](7-enet-module/3-enet/README.md)
# 7.3 ENet 对象

The `ENet` object provides a socket interface for Ethernet communication.  
See the examples in the previous section for instructions on how to use them.
[__SOURCE](7-enet-module/3-enet/1-enet-creator.md)
# 7.3.1 `ENet` 创建者

### 描述

创建一个以太网对象。返回所创建对象的引用。

### 语法

`ENet({protocol})`

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">名称</th>
      <th style="text-align:left">含义</th>
      <th style="text-align:left">其他</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>protocol</td>
      <td>
        "tcp" : TCP 通信。<br>
        "udp" : UDP 通信。<br>
        如果省略，则识别为 "udp"。</td>
    </tr>
  </tbody>
</table>

### 返回值

所创建对象的引用。

### 示例

```python
enet0 = ENet()
var tcp = ENet("tcp")
```
[__SOURCE](7-enet-module/3-enet/2-enet-member-var.md)
# 7.3.2 `ENet` 成员变量

<table>
  <thead>
    <tr>
      <th style="text-align:left">变量名称</th>
      <th style="text-align:left">数据类型</th>
      <th style="text-align:left">描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">ip_addr</td>
      <td style="text-align:left">字符串</td>
      <td style="text-align:left">
        可读/可写<br>
        设置或获取通信对手（远程）的 IP 地址。<br>
        仅在调用 open 语句时应用。
      </td>
    </tr>
    <tr>
      <td style="text-align:left">rport</td>
      <td style="text-align:left">数字</td>
      <td style="text-align:left">
        可读/可写<br>
        设置或获取通信对手（远程）的端口号。<br>
        仅在调用 open 语句时应用。
      </td>
    </tr>
    <tr>
      <td style="text-align:left">lport</td>
      <td style="text-align:left">数字</td>
      <td style="text-align:left">
        可读/可写<br>
        仅在 UDP 点对点和 TCP 服务器中使用，在 TCP 客户端中被忽略。<br>
        设置或获取控制器的自身（本地）端口号。<br>
        默认值为 0（如果未指定），在这种情况下该端口号会被自动生成。<br>
        仅在调用 open 语句时应用。<br>
        控制器上的端口 50000-50005 是预分配的 lports，无法使用。
      </td>
    </tr>
  </tbody>
</table>
[__SOURCE](7-enet-module/3-enet/3-enet-member-func/README.md)
# 7.3.3 `ENet` 成员函数

* 当从成员函数获取返回值时，请确保将参数放在括号中。
  
  ```python
  var nitem=obj.func(param1,param2) # (O) ; 必须使用括号
  var nitem=obj.func param1,param2 # (X) ; 语法错误
  ```

* 可以省略括号，但不获取返回值。

  ```python
  obj.func(param1,param2) # (O)
  obj.func param1,param2 # (O) ; 省略了括号
  ```
[__SOURCE](7-enet-module/4-bbuf/README.md)
# 7.4 `BBuf` 对象

一个 `BBuf (二进制缓冲区)` 对象封装了通过以太网通信发送和接收的二进制数据。
有关用法，请参见二进制通信示例。

[7.1.2 点对点、客户端示例 - 二进制传输](7-enet-module/1-exam-client/2-enet-client-bin.md)

[7.2.2 以太网 TCP 服务器 - 二进制传输](7-enet-module/2-exam-server/2-enet-server-bin.md)
[__SOURCE](7-enet-module/4-bbuf/1-bbuf-creator.md)
# 7.4.1 `BBuf` 创建者

### 描述

创建二进制缓冲区对象。返回创建对象的引用。

### 语法

`BBuf()`

### 返回值

创建对象的引用。

### 示例

```python
var bbuf = BBuf()
```
[__SOURCE](7-enet-module/4-bbuf/2-format.md)
# 7.4.2 支持的格式

成员函数 `append()` 或 `read_num()` 需要指定一个类型作为参数。

格式由 1 个字母表示有符号/无符号/浮点数和 1 个数字表示字节数。<br>
如果字母是大写则为大端模式，小写则为小端模式。

<table>
  <thead>
    <tr>
      <th>格式</th>
      <th>字节顺序</th>
      <th>类型</th>
      <th>字节数</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>"S1"</td>
      <td>大端模式<br>
      <td>有符号整数<br>
      <td>1字节<br>
    </tr>
    <tr>
      <td>"S2"</td>
      <td>大端模式<br>
      <td>有符号整数<br>
      <td>2字节<br>
    </tr>
    <tr>
      <td>"S4"</td>
      <td>大端模式<br>
      <td>有符号整数<br>
      <td>4字节<br>
    </tr>
    <tr>
      <td>"U1"</td>
      <td>大端模式<br>
      <td>无符号整数<br>
      <td>1字节<br>
    </tr>
    <tr>
      <td>"U2"</td>
      <td>大端模式<br>
      <td>无符号整数<br>
      <td>2字节<br>
    </tr>
    <tr>
      <td>"U4"</td>
      <td>大端模式<br>
<td>无符号整数<br>
      <td>4字节<br>
    </tr>
    <tr>
      <td>"F4"</td>
      <td>大端<br>
      <td>单精度实数<br>
      <td>4字节<br>
    </tr>
    <tr>
      <td>"F8"</td>
      <td>大端<br>
      <td>双精度实数<br>
      <td>8字节<br>
    </tr>
    <tr>
      <td>"s1"</td>
      <td>小端<br>
      <td>带符号整数<br>
      <td>1字节<br>
    </tr>
    <tr>
      <td>"s2"</td>
      <td>小端<br>
      <td>带符号整数<br>
      <td>2字节<br>
    </tr>
    <tr>
      <td>"s4"</td>
      <td>小端<br>
      <td>带符号整数<br>
      <td>4字节<br>
    </tr>
    <tr>
      <td>"u1"</td>
      <td>小端<br>
      <td>无符号整数<br>
      <td>1字节<br>
    </tr>
    <tr>
      <td>"u2"</td>
      <td>小端<br>
      <td>无符号整数<br>
      <td>2字节<br>
    </tr>
    <tr>
      <td>"u4"</td>
      <td>小端<br>
      <td>无符号整数<br>
      <td>4字节<br>
    </tr>
    <tr>
      <td>"f4"</td>
      <td>小端<br>
      <td>单精度实数<br>
      <td>4字节<br>
    </tr>
    <tr>
      <td>"f8"</td>
      <td>小端<br>
      <td>双精度实数<br>
      <td>8字节<br>
    </tr>
	 <tr>

  </tbody>
</table>
[__SOURCE](7-enet-module/4-bbuf/3-bbuf-member-func/README.md)
# 7.4.2 `BBuf` 成员函数
[__SOURCE](8-alias.md)
# 8. 别名

别名是可以作为变量或对象属性表示法的替代名称。

别名是可以用来表示变量或对象的替代名称。您可以使用简洁的名称替换过长的属性表示法，或用更易读的名称替换特定索引的IO变量。

别名通过 `alias` 语句定义，语法几乎与 `var` 或 `global` 相同。

别名的作用域与全局相同。也就是说，在执行 `alias` 语句后，它可以在任何后续作业中使用，即使主程序通过 `end` 语句或 `R0 - [ENTER]` 操作重置程序周期，别名也不会被销毁。

```python
global myval=3, yourname="Jane"
val i=0,msg="hello"
val profile = { name: "Paul", age: 43, role: [ "CTO", "engineer" ] }

alias grip=fb3.do4, work_no=fb1.diw2 # (1)
alias role=profile.role # (2)
alias tool0=project.robot.tools.t_0 # (3)

# 使用
grip=1
print work_no
print role[1]
tool0.mass=12
```

在上面的例子中，(1) 的输出变量 `fb3.do4` 被定义为名为 `grip` 的别名，而输入变量 `fb1.diw2` 被定义为别名 `work_no`。  
在 (2) 中，作为 `profile` 属性的角色数组被定义为别名 `role`。  
在 (3) 中，内置对象 `project.robot.tools.t_0` 被定义为别名 `tool0`，指向工具数据 \#0。

对于引用数组的别名，其元素可以用 [ ] 操作符指定，如 `role[1]`。  
对于引用对象的别名，其属性可以用 . 操作符指定，如 `tool0.mass`。

常量不能定义为别名。使用 `global` 或 `var` 定义它。  
表达式也不能定义为别名。请注意，这可能导致故障。

```python
#alias pie=3.141592 # (X)
#alias unit="mm/s" # (X)
global pie=3.141592 # (O)
global unit="mm/s" # (O)

#alias pie_2 = pie*pie # (X)
```
[__SOURCE](9-file/README.md)
# 9. 文件
[__SOURCE](9-file/1-file-system/README.md)
# 9.1 文件系统

在${cont_model}控制器的MAIN模块文件系统中，描述了创建、复制和删除目录和文件的指令。
[__SOURCE](9-file/1-file-system/1-mkdir.md)
# 9.1.1 `mkdir`

`mkdir` 是创建目录的过程。

### 描述

在MAIN模块中为指定路径创建一个目录。

- 您不能在教学挂件或USB内存上创建目录。
- 如果中间路径的目录不存在，则会创建中间路径。

### 语法

```python
mkdir <path>
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">path</td>
      <td style="text-align:left">
        要创建的目录路径。<br>
        开头不要加 /。
      </td>
      <td style="text-align:left">字符串表达式</td>
    </tr>
  </tbody>
</table>

### 示例

```python
mkdir "work/data1"
```

![](../../_assets/mkdir.png)
[__SOURCE](9-file/1-file-system/2-copyfile.md)
# 9.1.2 `copyfile`

一个 `copyfile` 是请求复制目录或文件的过程。

### 描述

将指定源路径的目录或文件复制到指定目标路径名。

- 只能在 MAIN 模块中执行，不能在 Teach Pendant 或 USB 存储器中执行。
- 如果目标路径名的中间路径目录不存在，将创建中间路径。
- 如果目标目录已存在，将其删除并复制源目录。
- 如果目标文件已经存在，将覆盖。
- 目录中的所有子目录也会被复制。
- 路径名还支持通配符 ('*', '?')。

- 由于可能复制大文件或整个目录，因此以异步方式在后台执行，以避免因等待复制而导致的节拍时间丢失。换句话说，当执行 `copyfile` 语句时，启动后台任务中的复制，立即继续执行下一个语句。例如，您可以请求复制并执行移动语句。通过读取结果变量的值可以确定复制是否成功完成。(即，在复制失败时不会生成错误或警告。)

- 在一个复制或删除完成之前，您无法请求另一个复制或删除。

### 语法

```python
copyfile <result-variable>,<source pathname>,<destination pathname>
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">result-variable</td>
      <td style="text-align:left">
        后台执行结果<br>
        <ul>
        <li>1: 成功完成。</li>
        <li>0: 正在复制。</li>
        <li>-1: 源路径名无效。</li>
        <li>-2: 目标路径名无效。</li>
        <li>-3: 复制失败。</li>
        <li>-6: 在复制通配符时全部失败。</li>
        <li>-7: 在复制通配符时部分失败。</li>
        <li>-11: 创建临时路径失败。</li>
<li>-12: 复制到临时路径失败。</li>
<li>-13: 清除现有目标路径失败。</li>
<li>-14: 目标路径创建失败。</li>
<li>-15: 从临时路径移动到目标路径失败。</li>
</ul>
</td>
<td style="text-align:left">变量</td>
</tr>
<tr>
<td style="text-align:left">源路径名</td>
<td style="text-align:left">
要复制的目录路径,<br>
或要复制的文件路径名
</td>
<td style="text-align:left">字符串表达式</td>
</tr>
<tr>
<td style="text-align:left">字符串表达式</td>
<td style="text-align:left">
- 以 '/' 结尾：要复制的路径。<br>
- 不以 '/' 结尾：通过复制将创建的路径名。
</td>
<td style="text-align:left">字符串表达式</td>
</tr>
</tbody>
</table>

### 示例

   var res
   copyfile res,"project/vars","work/vars_1" # vars_1/ 文件夹被创建。
   wait res==1,8,*timeout
   copyfile res,"project/vars","work/vars_1/" # vars_1/vars/ 文件夹被创建。
   wait res==1,8,*timeout
   copyfile res,"work/clear.job","project/jobs/0005_clear.job"
   wait res==1,4,*timeout
   copyfile res,"work/*_sub.job","project/jobs/" # 通配符
   wait res==1,4,*timeout
   call 5
   end
   *timeout
   print "copyfile 失败"
   end
![](../../_assets/copyfile.png)
[__SOURCE](9-file/1-file-system/3-delfile.md)
# 9.1.3 `delfile`

`delfile` 是一个请求删除目录或文件的过程。

### 描述

在指定路径中删除目录或文件。

- 仅能在 MAIN 模块内执行，而不能在 Teach Pendant 或 USB 存储器中执行。
- 目录中的所有子目录也会被删除。
- 如果指定的路径名不存在，则以成功结束。
- 路径名也支持通配符 ('*', '?')。

- 由于可能会删除大的文件或整个目录，因此它在后台异步执行，以避免因等待删除而导致的节拍时间损失。可以通过读取结果变量的值来确定删除是否成功完成。（也就是说，当删除失败时，不会生成错误或警告。）

- 在一份复制或删除完成之前，您不能请求另一个复制或删除。

### 语法

```python
delfile <result-variable>,<pathname>
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">result-variable</td>
      <td style="text-align:left">
        背景执行的结果<br>
        <ul>
        <li>1: 成功完成。</li>
        <li>0: 删除正在进行中。</li>
        <li>-41: 删除目录失败。</li>
        <li>-42: 删除文件失败。</li>
        </ul>
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">pathname</td>
<td style="text-align:left">
        要删除的目录路径,<br>
        或要删除的文件路径
      </td>
      <td style="text-align:left">字符串表达式</td>
    </tr>
  </tbody>
</table>

### 示例

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
# 9.2 加载/保存

解释将文件加载/保存到 ${cont_model} 控制器的 MAIN 模块内存的语句。
[__SOURCE](9-file/2-load-save/1-load_job.md)
# 9.2.1 `load_job`

读取 MAIN 模块的 project/jobs/ 文件夹更改以更新内存的语句。


### 描述

将 MAIN 模块的 project/jobs/ 文件夹中的作业加载到新的内存中。

如果您通过 FTP 或 copyfile 命令将 .job 文件复制或覆盖到 jobs/ 文件夹中，则必须执行该语句以反映内存，以便能够选择或调用作业。

- 注意：内存中不存在于 jobs/ 文件夹的作业将被删除。
- 如果文件的修改时间不同，则会加载该文件。
- 内存中不存在的文件将被加载。

- 由于可以加载大容量的 .jobs，因此在后台异步进行，以避免因加载而导致的节拍时间损失。可以通过读取结果变量的值来确定加载的成功完成。
- 在当前加载完成之前，无法请求另一个加载。


### 语法

```python
load_job <result-variable>,"*"
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">result-variable</td>
      <td style="text-align:left">
        背景执行的结果<br>
        <ul>
        <li>1：成功完成。</li>
        <li>0：加载中。</li>
        </ul>
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">job filename</td>
      <td style="text-align:left">
      您只能使用“*”参数，这意味着所有文件。
      </td>
      <td style="text-align:left">字符串表达式</td>
    </tr>
  </tbody>
</table>

### 示例

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
# 9.2.2 `load_csv`

支持版本：V60.28-00。

声明将 .csv 文件（根全局数组）中的更改读取到 MAIN 模块的 `project/vars/` 文件夹的内存中。

### 描述

HRScript 的全局根数组存储在 `vars/` 文件夹中，作为 CSV 标准格式的文件。（‘根’意味着它不是另一个数组或对象的属性。）

有关变量文件的信息，请参阅下面的操作手册链接。

[全局变量/变量文件](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/6-monitoring/3-job/3-global-variable/3-var-files?cont_model=${cont_model})

您可以使用 PC 上的文本编辑器轻松编辑 .csv 文件。
复制到 `vars/` 文件夹的编辑文件不会立即在内存中反映，只有在教学挂件的全局变量窗口中使用 `[load all]` 功能或执行 `load_csv` 语句时才会反映。

- 由于大型 .csv 可以被加载，它们在后台异步执行以避免因加载而导致的失去节拍时间。成功加载可以通过读取结果变量的值来确定。
- 当前加载完成之前，您无法请求另一个加载。

### 语法

```python
load_csv <result-variable>,"*"
load_csv <result-variable>,"<variable name>"
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">result-variable</td>
      <td style="text-align:left">
        背景执行的结果<br>
        <ul>
        <li>1: 完成。</li>
        <li>0: 加载中。</li>
        </ul>
      </td>
      <td style="text-align:left">变量</td>
    </tr>
<tr>
      <td style="text-align:left">.csv 文件标题</td>
      <td style="text-align:left">
        <ul>
        <li>"*": 加载所有文件。</li>
        <li>"&lt;variable name&gt;": 加载 &lt;variable name&gt;.csv 文件。</li>
        </ul>
      </td>
      <td style="text-align:left">字符串表达式</td>
    </tr>
  </tbody>
</table>

{% hint style="warning" %}
如果您使用 "*" 加载所有 .csv 文件，则在 `vars/` 文件夹中没有 .csv 的根数组将被删除。
{% endhint %}

### 示例

```python
     var res
     copyfile res,"work/arrs/locs1.csv","project/vars/locs.csv"
     wait res==1,4,*timeout
     load_csv res,"locs"
     wait res==1,4,*timeout
     call 5
     end
     *timeout
     print "加载新位置失败。"
     end
```
[__SOURCE](9-file/2-load-save/3-save_csv.md)
# 9.2.3 `save_csv`

支持版本 V60.28-00。

将全局根数组变量存储为 .csv 文件，存放在 MAIN 模块的 `project/vars/` 文件夹中。

### 描述

HRScript 的全局根数组被存储在 `vars/` 文件夹中，作为 CSV 标准格式的文件。（“根”意味着它不是另一个数组或对象的属性。）

有关变量文件的信息，请参阅以下操作手册链接。

[全局变量/变量文件](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/6-monitoring/3-job/3-global-variable/3-var-files?cont_model=${cont_model})

全局根数组不会在值更改时立即存储到 .csv 文件中。
当您按 `Ctrl+[F7: 保存]` 或关闭电源时，它将作为文件保存，您可以通过执行 `save_csv` 命令立即将其保存为文件。

- 因为可以保存大的 .csv，所以它们在后台异步执行，以避免由于保存而导致的节拍时间损失。成功保存的结果可以通过读取结果变量的值来确定。
- 在当前保存完成之前，您无法请求另一个保存。

### 语法

```python
save_csv <result-variable>,"*"
save_csv <result-variable>,"<variable name>"
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">result-variable</td>
      <td style="text-align:left">
        后台执行的结果<br>
        <ul>
        <li>1: 完成。</li>
        <li>0: 保存进行中。</li>
        </ul>
      </td>
      <td style="text-align:left">变量</td>
    </tr>
<tr>
      <td style="text-align:left">.csv 文件标题</td>
      <td style="text-align:left">
        <ul>
        <li>"*": 保存所有变量。</li>
        <li>"&lt;variable name&gt;": 保存 &lt;variable name&gt;.csv 文件。</li>
        </ul>
      </td>
      <td style="text-align:left">字符串表达式</td>
    </tr>
  </tbody>
</table>

{% hint style="warning" %}
如果您通过指定 "*" 来保存所有 .csv 文件，它不会删除 `vars/` 文件夹中的 .csv 文件，因为对应名称的根变量不存在。
{% endhint %}

### 示例

```python
     var res
     save_csv res,"locs"
     wait res==1,4,*timeout
     copyfile res,"project/vars/locs.csv","work/arrs/locs2.csv"
     wait res==1,4,*timeout
     call 5
     end
     *timeout
     print "无法保存新位置。"
     end
```
[__SOURCE](10-etc/README.md)
# 10. 其他事项
[__SOURCE](10-etc/1-proc/README.md)
# 10.1 其他程序
[__SOURCE](10-etc/1-proc/1-gather.md)
# 10.1.1 `gather`

`gather` 是指定使用数据收集功能时收集开始和结束的过程。

### 描述

使用 `gather` 指定收集的开始和结束。收集结果文件保存在以下位置：
- 存储路径：MAIN/project
- 文件名：0001.GDT 到 0030.GDT

最多保存 30 个收集结果文件，如果超过此数量，之前的收集结果文件将被覆盖。

`gather_state()` 函数返回数据收集操作的当前状态。
  - 0 : 不在收集中。
  - 1 : 在收集中。 (gather 1 ~ gather 0)
  - 2 : 将收集结果保存为文件。 (gather 0~)

### 语法

```python
gather <start/end>
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">start/end</td>
      <td style="text-align:left">
        <ul>
        <li>1: 数据收集开始</li>
        <li>0: 数据收集结束</li>
        </ul>
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
  </tbody>
</table>

### 示例

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
# 10.1.2 `tonl`

`tonl` 语句是执行开始和结束之间步骤位置校正的过程。

### 描述

如果您知道坐标变换关系，当您在不计算单独坐标变换关系的情况下输入变换关系时，将应用此过程。

```python
R=[x,y,z,rx,ry,rz]
```

![](../../_assets/tonl2.png)

对于旋转矩阵，按 Rot_z.Rot_y.Rot_x 的顺序应用。

### 语法

```python
tonl <start/end>,<shift>
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">start/end</td>
      <td style="text-align:left">
        在线变换开始/结束<br>
        <ul>
        <li>on：开始</li>
        <li>off：结束</li>
        </ul>
      </td>
      <td style="text-align:left">开/关</td>
    </tr>
    <tr>
      <td style="text-align:left">shift</td>
      <td style="text-align:left">
        移动的量
      </td>
      <td style="text-align:left">移动表达式</td>
    </tr>
  </tbody>
</table>

### 示例

```python
   global sft
   enet1.recv msg # 通过以太网接收移位量
   sft=Shift(msg)
   tonl on,sft
   move L,spd=50mm/s,accu=0,tool=1
   move L,spd=10mm/s,accu=0,tool=1
   move L,spd=50mm/s,accu=0,tool=1
   tonl off
```

![](../../_assets/tonl.png)
[__SOURCE](10-etc/1-proc/3-seltool.md)
# 10.1.3 `seltool`

`seltool` 是一个用于更改工具编号的过程。

### 描述

工具分为连接到机器人法兰的机器人工具和与机器人单独安装的站工具，而 `seltool` 更改每种类型的工具编号。

### 语法

```python
seltool <tool number>,<tool type>
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">工具编号</td>
      <td style="text-align:left">
        工具编号<br>
        <ul>
        <li>机器人工具: 0 ~ 31</li>
        <li>站工具: 0 ~ 3</li>
        </ul>
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">工具类型</td>
      <td style="text-align:left">
        用于更改工具编号的工具类型<br>
        <ul>
        <li>机器人工具: robot</li>
        <li>站工具: station</li>
        </ul>
      </td>
      <td style="text-align:left">机器人/站</td>
    </tr>
  </tbody>
</table>
### 示例

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
# 10.1.4 `triggout`

`triggout` 是一个过程，允许您调整信号输出时间点为提前输出 (-) 或延迟输出 (+)。

### 描述

在 contpath 1 或 2 的命令连续处理间隔中，当命令位置到达目标位置（精度 OK）时，您可以调整信号输出时间点为提前 (-) 或延迟 (+)。

### 语法

```python
triggout <output variable>,val=<output value>,time=<ahead/behind time>
triggout <output variable>,val=<output value>,dist=<ahead/behind distance>,x=<X-direction absolute position>
triggout <output variable>,val=<output value>,dist=<ahead/behind distance>,y=<Y-direction absolute position>
triggout <output variable>,val=<output value>,dist=<ahead/behind distance>,z=<Z-direction absolute position>
triggout <output variable>,val=<output value>,dist=<ahead/behind distance>,j=<tcp or axis-direction relative distance>
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">output variable</td>
      <td style="text-align:left">
        与输出信号对应的变量<br>
        <ul>
        <li>用户输出变量；do, dob, dow, dol, dof</li>
        <li>系统输出变量；so, sob, sow, sol, sof</li>
        </ul>
      </td>
      <td style="text-align:left">output variable</td>
    </tr>
    <tr>
      <td style="text-align:left">output value</td>
      <td style="text-align:left">
        当为位输出（do, so）时，0 为关闭，非 0 为开启
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">ahead/behind time</td>
<td style="text-align:left">
        -10.00 ~ 2.00 [s]<br>
        如果是(-)，信号在目标位置到达之前输出；如果是(+) ，在到达之后输出。
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">前/后距离</td>
      <td style="text-align:left">
        -3000 ~ 3000 [mm]<br>
        如果是(-)，信号在目标位置到达之前输出；如果是(+) ，在到达之后输出。
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">绝对位置 x, y, z 方向</td>
      <td style="text-align:left">
        -3000 ~ 3000 [mm]
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">tcp 或轴向相对距离<br>
      tcp : 如果 j=0 则<br>
      轴向方向 : 如果 j=1 以上则<br>
      </td>
      <td style="text-align:left">
        tcp : -3000 ~ 3000 [mm]，轴向方向 : -3000 ~ 3000 [mm] 或 [deg]<br>
        如果是(-)，信号在相对距离达到之前输出；如果是(+) ，在达到之后输出。
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
  </tbody>
</table>

### 示例

   move L,spd=300mm/s,accu=3,tool=1
   triggout do1,val=1,time=-0.5 #在到达步骤前0.5秒打开 do1
   triggout do1,val=1,dist=-100.0,j=0 #当 tcp 到达步骤位置和相对距离 -100mm 时打开 do1
   triggout do1,val=1,dist=-3.0,j=1 #当轴 1 到达步骤位置和相对距离 -100mm 时打开 do1
   triggout do1,val=1,x=-100.0 #当 X 坐标值达到 -100mm 时打开 do1
   triggout do1,val=1,x=-100.0,y=-100.0 #当 X, Y 坐标值达到 -100mm 时打开 do1
   move L,spd=30%,accu=2,tool=1
   end

{% hint style="warning" %}
* **包含 `triggout` 命令的步骤** 用作参考点，系统检查信号是否输出 **直到下一步结束的那一刻**。 
* 如果 **在该时间范围内没有输出信号**，将显示以下警告：  
  **W0241: _"触发输出信号在步骤范围内未输出。"_**

{% endhint %}
[__SOURCE](10-etc/1-proc/5-intr_def.md)
# 10.1.5 `intr_def`

`intr_def` 是一个指定中断条件、观察间隔和发生中断时运行的程序的过程。

### 语法

中断函数是一种程序调用。当机器人在中断观察间隔内工作时，它会在满足预定义的中断条件时调用指定的作业。当被调用的程序运行完成后，它会返回到先前运行程序的位置并继续运行。

![](../../_assets/intr_def_1.png)

### 简要说明

- 仅在中断观察间隔中操作。
- 支持算术表达式作为中断条件表达式。
- 允许在执行中断程序时处理另一个中断（多个中断）。

### 中断被清除的时间点

如果发生以下操作，所有定义的中断会自动清除。

- 执行 'R0: 任务重置' 时
- 程序第一次运行时
- 更改程序计数器（步骤/功能 #）后开始时

### 示例

```python
intr_def <on/off>,no=<interrupt number>,var=<interrupt condition>,val=<condition matching value>,job=<call program number>,[once]
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">on/off</td>
      <td style="text-align:left">
        定义中断或删除已定义的中断<br>
        <ul>
        <li>打开：定义一个新的中断。</li>
        <li>关闭：删除已定义的中断。 （第三个及后续参数将被忽略。）</li>
        </ul>
      </td>
      <td style="text-align:left">打开/关闭</td>
    </tr>
    <tr>
      <td style="text-align:left">中断号码</td>
      <td style="text-align:left">
        要定义或删除的中断号码。<br>
      </td>
      <td style="text-align:left">算式表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">中断条件</td>
      <td style="text-align:left">
        将导致中断的条件表达式。
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">条件匹配值</td>
      <td style="text-align:left">
        生成中断的条件表达式的值。
      </td>
      <td style="text-align:left">算式表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">调用程序号码</td>
      <td style="text-align:left">
        当发生中断时要调用的程序号码。
      </td>
      <td style="text-align:left">算式表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">[一次]</td>
      <td style="text-align:left">
        在中断监视间隔内只处理一个中断，而不处理额外的中断。
      </td>
      <td style="text-align:left">一次</td>
    </tr>
  </tbody>
</table>


### 错误

- E1351 : 在不删除的情况下重新定义已定义的中断号码时发生。 请检查已创建的程序。
### 示例

```python
   intr_def on,no=1,var=di5,val=1,job=24,once # 定义中断
   move P,spd=30%,accu=3,tool=1
   move L,spd=30mm/s,accu=3,tool=1
   ...
   move L,spd=30mm/s,accu=3,tool=1
   move P,spd=30%,accu=3,tool=1
   intr_def off,no=1 # 删除中断
   move P,spd=30%,accu=3,tool=1
   end
```
[__SOURCE](10-etc/1-proc/6-typeof.md)
# 10.1.6 `typeof`

`typeof` 是获取变量或表达式类型的过程。结果从 `result()` 函数返回。


### 语法

```python
typeof <expression>
```


### 示例

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
# 10.1.7 `gasp_check`

`gasp_check`语句估计安装在机器人上的气体弹簧的压力，并检查其是否正常。

### 描述

![](../../_assets/gasp_check.png)

- 为了估计压力，配备气体弹簧的轴从其当前位置往回移动-20度。（建议在H轴140度位置执行）
- 通过将估计压力保存为变量来监测压力。
- 用户可以输入正常压力和容差。如果估计压力超过范围，设置的错误输出信号将开启。

### 语法

```python
gasp_check pres=<estimated pressure>,ref=<reference pressure>,tol=<tolerance>
gasp_check pres=<estimated pressure>,ref=<reference pressure>,tol=<tolerance>,os=<error output signal>
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">estimated pressure</td>
      <td style="text-align:left">
         存储估计气体弹簧压力的变量[bar]
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">normal pressure</td>
      <td style="text-align:left">
        作为错误发生的参考值的正常压力[bar]
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">tolerance</td>
      <td style="text-align:left">
        估计压力误差容差[bar]
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">错误输出信号</td>
      <td style="text-align:left">
        当发生错误时的信号输出
      </td>
      <td style="text-align:left">输出信号变量</td>
    </tr>
  </tbody>
</table>

### 错误
- E21011 : 当估计的气弹簧压力低于最低错误标准时发生。
- E21012 : 当估计的气弹簧压力高于最高错误参考时发生。
- E21013 : 在不支持气弹簧压力检查的机器人上发生。


### 示例

   var v0
   move P,spd=50%,accu=3,tool=1
   gasp_check pres=v0,ref=120,tol=20,os=do50    # 如果估计压力在100到140 bar之间，则为正常
   end

{% hint style="warning" %}
* 产品运行时，请勿进入操作区域或触摸机器人。 有受伤的风险。
{% endhint %}

{% hint style="info" %}
* 仅在配备气弹簧的机器人上支持
* 为了准确估计，必须在使用该功能之前进行[轴添加重量设置](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/7-system/4-robot-parameter/7-axis-add-weight/README?cont_model=${cont_model})和[负载估计功能](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/7-system/7-auto-calibration/3-load-estimation?cont_model=${cont_model})。
* 有关气弹簧压力检查监控功能的详细说明，请参阅以下链接。
[](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/6-monitoring/4-system/2-system-diagnosis/2-gas-pressure-check?cont_model=${cont_model})
* 估计的气弹簧压力可能会因测量开始时的初始姿势而有所变化。在机器人的初始设置期间，请根据每个参考姿势进行的测量管理压力值，并定期在同一姿势下测量压力，以便将其与初始值进行比较。如果在测量值中观察到显著差异，请检查设备的状态。

{% endhint %}
[__SOURCE](10-etc/1-proc/8-optime.md)
# 10.1.8 `optime`

`optime`语句是一种用于启动或更新操作时间测量的程序。

### 描述

通常，当按下启动按钮时，操作时间测量开始，操作时间在程序执行`end`时自动更新。  
然而，如果程序在未执行`end`的情况下使用`goto`语句跳回开始，操作时间会继续增加。在这种情况下，监控的操作时间值变得毫无意义。

为了解决这种情况，`optime`语句允许用户明确指定操作时间测量开始和更新的点。

### 语法
```python
optime <parameter>
```
### 参数
| 项目      | 描述                                                               | 备注   |
| --------- | ------------------------------------------------------------------ | ------ |
| 参数      | - cycle_start: 开始测量<br>- cycle_end: 更新测量                 |        |

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
# 10.1.9 `count_up`

`count_up` 声明是一个过程，它将指定变量的值增加 1，并在超过预设值时将其重置为初始值。

### 描述

此声明每次执行时将指定变量的值增加 1。  
如果变量值超过预设值所指定的值，则该变量将重置为初始值所指定的值。

执行  
```python
count_up cnt, init=0, preset=100`  
```
产生的结果与执行以下四行相同：

```python
cnt = cnt + 1
if cnt > 100
    cnt = 0
endif
```

### 语法
```python
count_up <variable>, init=<initial value>, preset=<final value>
```

### 参数
| 项目     | 描述                                                              | 备注 |
| -------- | ------------------------------------------------------------------------ | ------- |
| Variable | 将作为计数器的变量，其值将被增加                                    |         |
| init     | 当变量超过预设值时要分配的初始值                                     |         |
| preset   | 变量的最大值                                                         |         |

### 示例
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
# 10.1.10 `count_dn` 语句

`count_dn` 语句是一个过程，它将指定变量的值减 1，当该值小于预设值时，将其重置为初始值。

### 描述

该语句每次执行时将指定变量的值减少 1。  
如果变量值小于预设值指定的值，则变量将重置为初始值指定的值。

执行  
```python
count_dn cnt, init=100, preset=0
```
产生的结果与以下四行代码执行的结果相同：

```python
cnt = cnt - 1
if cnt < 0
    cnt = 100
endif
```

### 语法
```python
count_dn <variable>, init=<initial value>, preset=<final value>
```

### 参数
| 项目     | 描述                                                                          | 备注     |
| -------- | ------------------------------------------------------------------------------- | -------- |
| 变量     | 将作为计数器递减的变量                                                       |          |
| init     | 当变量小于 `preset` 值时要分配的初始值                                       |          |
| preset   | 变量的最小值                                                                  |          |


### 示例
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
# 10.1.11 `cycle_end`

`cycle_end` 语句是一个过程，它清除因执行 `call` 语句而管理的所有调用堆栈。

### 描述

当程序在存在调用堆栈的情况下执行 `end` 语句时，程序执行返回到执行 `call` 语句的位置并继续运行。  
然而，当执行 `cycle_end` 语句时，所有管理的调用堆栈都会被清除。因此，程序不会返回到 `call` 语句的位置，而是停止执行。

### 语法

```python
cycle_end
```

### 示例

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
# 10.1.12 `speed_out` 声明

`speed_out` 声明是一个计算与机器人当前运动速度成比例的值并将结果分配给指定变量的过程。  
它仅在执行插值设置为 `左 (L)` 或 `C` 的 `移动 (move)` 声明时起作用。

### 描述

该声明计算与机器人当前移动速度成比例的值，并将计算结果存储在指定变量中。  

如果执行以下命令，如图所示，计算出与当前机器人速度 `x` 相对应的值 `y` 并分配给 dow10。
...  
```python
speed_out on,min_spd=100,max_spd=2000,min_val=10,max_val=100,var=dow10
```

![](../../_assets/speed_out.png)

### 语法
```python
speed_out <on/off>, min_spd=<最低速度>, max_spd=<最高速度>, min_val=<最低值>, max_val=<最高值>, var=<数字变量>
```

### 参数
| 项目    | 描述                                                      | 备注              |
| ------- | ---------------------------------------------------------- | ---------------- |
| on/off  | 指定函数启用的部分                                       |                  |
| min_spd | 指定最低机器人移动速度 [mm/s]                           |                  |
| max_spd | 指定最高机器人移动速度 [mm/s]                           |                  |
| min_val | 指定与最低机器人速度相对应的值                         |                  |
| max_val | 指定与最高机器人速度相对应的值                         |                  |
| var     | 指定存储计算值的变量                                    | 数字变量         |

### 示例

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
# 10.1.13 `任务 (task)` 语句

`任务 (task)` 语句是用于执行多任务功能的过程。  
有关 `任务 (task)` 语句的详细信息，请参阅以下链接：  
[${cont_model} 控制器功能手册 - 多任务处理](https://hrbook-hrc.web.app/#/view/doc-multi-task/zh/README?cont_model=${cont_model})  

### 语法

```python
task start, sub=<subtask number>, job=<program number>
task wait,  sub=<subtask number>
task sync,  id=<identifier>, no=<number of executions with the same id>
task stop,  sub=<subtask number>
task reset, sub=<subtask number>
```
[__SOURCE](10-etc/1-proc/14-toolchng.md)
# 10.1.14 `toolchng`

`toolchng`语句是用于更改分配给附加轴的伺服工具的程序。  
有关`toolchng`语句的详细信息，请参阅以下链接：  
[${cont_model} 机器人控制器功能手册 - 伺服工具更换](https://hrbook-hrc.web.app/#/view/doc-svtool-change/zh/README?cont_model=${cont_model})

### 语法

```python
toolchng on/off, tg=<change target>, di=<connection complete signal>, wait=<waiting time>
```
[__SOURCE](10-etc/1-proc/15-json_parse.md)
# 10.1.15 `json_parse`

支持版本：V60.32-00

`json_parse` 过程解析 JSON 字符串以构建对象、数组或值。

### 语法

在过程开始后，`result()` 函数返回一个结果对象，用于检查状态和存储结果数据。
```python
    json_parse <json string literal/value>
    var r = result()
```

您必须等待此过程完成。
```python
    wait r.status == "finished"
```

解析的结果将存储在 `r.data` 中。如果在访问结果之前不允许程序完成，则可能会发生错误。

##### 状态

<table>
  <thread>
    <th style="text-align:left">状态</th>
    <th style="text-align:left">详细信息</th>
  </thread>
  <tbody>
  <tr>
    <td style="text-align:left">解析中</td>
    <td style="text-align:left">JSON 字符串仍在解析中。数据尚不可用。</td>
  </tr>
  <tr>
    <td style="text-align:left">已完成</td>
    <td style="text-align:left">JSON 字符串解析已完成。数据现在可用。</td>
  </tr>
  </tbody>
</table>

### 示例
```python
    json_parse "[1, 2, 3, 4]"
    var r = result()
    wait r.status == "finished", 10 # 等待进程完成，最长超时 10 秒。
    var jr = r.data   # r.data 的类型是数组
    print jr          # 打印 [1, 2, 3, 4]
```
    json_parse "3.141592"
    var r = result()
    wait r.status == "finished", 10 # 等待进程完成，最大超时为10秒。
    var jr = r.data    # r.data 的类型为 double
    print jr           # 打印出 3.141592
```
```python
    json_parse "{\"test\": \"value\"}" # JSON 字符串内部的双引号必须被转义。
    var r = result()
    wait r.status == "finished", 10 # 等待进程完成，最大超时为10秒。
    var jr = r.data    # r.data 的类型为 JObject
    print jr           # 打印出 { _type: "JObject", _sub_file: "", _desc: "", test: "value" } 
```
[__SOURCE](10-etc/1-proc/16-brake_check.md)
# 10.1.16 `brake_check`

`brake_check`语句是一个程序，通过对每个轴电机施加扭矩来诊断制动器是否正常工作。

### 描述

![](../../_assets/brake_check.png)

* **保持测试**  
  在制动器保持锁定的情况下，对每个轴施加3秒的扭矩，并检查电机角度的变化是否低于阈值。

* **释放测试**  
  在制动器释放的情况下，对每个轴施加3秒的扭矩，并检查电机角度的变化是否高于阈值。

### 语法

```python
brake_check  
brake_check os=<error output signal> 
brake_check job=<return program>
brake_check os=<error output signal>,job=<return program>
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">错误输出信号</td>
      <td style="text-align:left">
         当角度变化超过阈值时输出的信号<br>
         - 如果指定，将触发警告并输出信号。<br>
         - 如果未指定，将发生错误。
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">返回程序</td>
      <td style="text-align:left">
        当角度变化超过阈值时要执行的程序号。
      </td>
      <td style="text-align:left">变量</td>
    </tr>
</tbody>
</table>

### 设置
当您在 brake_check 命令中触摸 [属性] 按钮时，将进入刹车诊断设置屏幕。  
![](../../_assets/brake_check_setting.png)

- **模式**  
  设置是运行阈值设置模式还是诊断模式。

- **刹车测试项目**  
  设置是否对每个轴执行保持和释放测试。

- **扭矩比 (%)**  
  设置每个轴施加多少扭矩。

- **错误检测阈值**  
  在诊断模式下运行时，设置每个轴的错误检测阈值角度。  
  在阈值设置模式下，值会自动设置。  
  仅可由工程师级别或更高权限编辑。

### 错误代码
- E1509：当刹车测试在 6 秒内未完成时发生。
- E1510：当刹车未释放时发生。
- E1525 ~ E1527：当返回程序缺失或其配置不同时发生。
- E1529：当机器人正在移动、独立运行等时，无法执行刹车测试。
- E1530：当刹车测试执行延迟时发生。
- E21005/W21005：当保持测试期间的角度变化大于释放测试期间的角度变化时发生。

### 示例

```python
   var v0
   move P,spd=50%,accu=3,tool=1
   brake_check os=do50,job=9000    # 在错误时，输出 do50 并执行作业程序编号 9000
   end
```

{% hint style="warning" %}
* 在产品操作时，请勿进入操作区域或触摸机器人。存在受伤风险。
{% endhint %}

{% hint style="info" %}
* 仅支持配备气弹簧的机器人
* 为了准确估计，必须在使用该功能之前进行 [轴添加重量设置](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/7-system/4-robot-parameter/7-axis-add-weight/README?cont_model=${cont_model}) 和 [负载估计功能](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/7-system/7-auto-calibration/3-load-estimation?cont_model=${cont_model})。
* 有关刹车检查监控功能的详细说明，请参阅以下链接。
[](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/6-monitoring/4-system/2-system-diagnosis/1-brake-check?cont_model=${cont_model})
{% endhint %}
[__SOURCE](10-etc/2-func/README.md)
# 10.2 其他功能
[__SOURCE](10-etc/2-func/1-rducs.md)
# 10.2.1 `rducs` - 用户坐标系

### 描述

读取生成的用户坐标系作为姿态的函数。

- 将创建的用户坐标系的位置/方向复制到其姿态值中。
- 如果没有创建或参数无效，则作业执行将以错误中断。

### 语法

```python
<result variable> = rducs(<user coord. system number>,<pose variable>)
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">result variable</td>
      <td style="text-align:left">
        后台执行的结果<br>
        <ul>
        <li>0: 成功完成。</li>
        </ul>
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">user coord. system number</td>
      <td style="text-align:left">
        要读取的用户坐标系的编号
      </td>
      <td style="text-align:left">[1~20]</td>
    </tr>
    <tr>
      <td style="text-align:left">pose variable</td>
      <td style="text-align:left">
        获取位置/方向的变量
      </td>
      <td style="text-align:left">姿态变量</td>
</tr>
  </tbody>
</table>

### 返回值


<table>
  <thead>
    <tr>
      <th style="text-align:left">值</th>
      <th style="text-align:left">含义</th>
      <th style="text-align:left">其他</th>
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


### 错误

- E14613 : 当实际参数与形式参数不匹配时发生。请检查实际参数。
- E14614 : 当用户坐标号不是数字时发生。请重新指定用户坐标号。
- E14615 : 当用户坐标号不是1到20之间的数字时发生。请更改用户坐标号。
- E1336 : 当它是未注册的用户坐标号时发生。请更改用户坐标号。


### 示例

```python
   var p_uc2=Pose(0,0,0,0,0,0,"base")
   var res=rducs(2,p_uc2)
   end
```

![](../../_assets/rducs.png)
[__SOURCE](10-etc/2-func/2-segment.md)
# 10.2.2 `segment`

`segment` 是将起始位置和结束位置之间的距离均匀划分的函数。


### 描述

将函数因子之间的起始位置和结束位置的距离均匀划分，并根据指定计数器存储考虑到位置和姿态的姿态值。
![](../../_assets/image_segment_1.png)

例如，如果 `P3=segment(P1,P2,3,2)`，则将 `P1` 起始位置与 `P2` 目标位置之间的距离划分为 3 个相等部分，并将第二个姿态的位置和旋转的姿态值存储在 `P3` 姿态变量中。

当您将经过位置作为函数的参数添加时，组成起始位置、经过点和目标位置的弧上的距离被均匀划分，位置和旋转的姿态值存储在姿态变量中。

![](../../_assets/image_segment_2.png)

例如，如果 `P10=segment(P1,P2,P3,4,2)`，
则组成 `P1` 起始姿态和 `P2` 经过姿态 `P3` 目标姿态的弧上的距离被划分为 4 个相等部分，指定第二个姿态的位置和旋转的姿态值存储在 `P10` 姿态变量中。

<br>

### 语法

```python
result=segment(<start pose>,<end pose>,<division number>,<counter>)
```

```python
result=segment(<start pose>,<via pose>,<end pose>,<division number>,<counter>)
```

### 返回值

结果姿态。

### 参数
<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">start pose</td>
      <td style="text-align:left">
        start pose
      </td>
```html
<td style="text-align:left">姿态表达</td>
    </tr>
    <tr>
      <td style="text-align:left">经过姿态</td>
      <td style="text-align:left">
        经过姿态
      <td style="text-align:left">姿态表达</td>
    </tr>
    <tr>
      <td style="text-align:left">结束姿态</td>
      <td style="text-align:left">
        结束姿态
      </td>
      <td style="text-align:left">姿态表达</td>
    </tr>
    <tr>
      <td style="text-align:left">分割数</td>
      <td style="text-align:left">
        分割数<br>
        (1 ~ 30000)
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">计数器</td>
      <td style="text-align:left">
        要存储的姿态计数器编号<br>
        (0 ~ 300000, 0: 起始姿态)
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
  </tbody>
</table>

### 示例
```python
     var po1,po2,po3
     po1=Pose(1000.000,0.000,1938.000,0.000,0.000,0.000) # 起始姿态
     po2=Pose(2000.000,0.000,1938.000,0.000,0.000,0.000) # 结束姿态
     po3=segment(po1,po2,4,2)
     end
```

```python
     var po1,po2,po3,po10
     po1=Pose(1000.000,0.000,1938.000,0.000,0.000,0.000) # 起始姿态
     po2=Pose(1500.000,500.000,1938.000,0.000,0.000,0.000) # 经过姿态
     po3=Pose(2000.000,0.000,1938.000,0.000,0.000,0.000) # 结束姿态
     po10=segment(po1,po2,po3,5,3)
     end
```

[__SOURCE](10-etc/2-func/3-intersection.md)
# 10.2.3 `intersection`

您可以使用 `intersection` 函数找到与直线相交的点，该点与直线的最短距离为一个点，或者找到与直线相交的最短距离。

### 描述

如果您指定两个形成直线的点和另一个点作为参数，您将获得一条连接直线和一个点的交叉位置，该交叉位置为最短距离。

![](../../_assets/image_intersection_1.png)

如果您指定两个形成直线的点和两个形成另一条直线的点作为参数，您可以找到两条直线之间的最短距离的交点。交点是您指定的第一条直线的交点。

![](../../_assets/image_intersection_2.png)


### 语法

```python
result=intersection(<straight-line ref.pose 1>,<straight-line ref.pose 2>,<position ref.pose>)
```

```python
result=intersection(<straight-line ref.pose 1>,<straight-line ref.pose 2>,<straight-line ref.pose 3>,<straight-line ref.pose 4>)
```

### 返回值

结果姿态。


### 参数
<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">straight-line ref.pose 1</td>
      <td style="text-align:left">
        第一条直线的第一个参考姿态
      </td>
      <td style="text-align:left">姿态表达</td>
    </tr>
    <tr>
      <td style="text-align:left">straight-line ref.pose 2</td>
      <td style="text-align:left">
2nd reference pose of 1st straight-line  
      <td style="text-align:left">位姿表达</td>  
    </tr>  
    <tr>  
      <td style="text-align:left">位置参考位姿</td>  
      <td style="text-align:left">  
        引用位姿以找到一条直线和最短距离位置  
      </td>  
      <td style="text-align:left">位姿表达</td>  
    </tr>  
    <tr>  
      <td style="text-align:left">直线参考位姿 3</td>  
      <td style="text-align:left">  
        2nd 直线的第 1 个参考位姿  
      </td>  
      <td style="text-align:left">位姿表达</td>  
    </tr>  
    <tr>  
      <td style="text-align:left">直线参考位姿 4</td>  
      <td style="text-align:left">  
        2nd 直线的第 2 个参考位姿  
      </td>  
      <td style="text-align:left">位姿表达</td>  
    </tr>  
  </tbody>  
</table>  

### 示例  
[__SOURCE](10-etc/2-func/4-rand.md)
# 10.2.4 `rand`

您可以使用 `rand` 函数生成随机数。

### 描述
根据函数的参数，它生成一个介于 0 和 1 之间的随机实数，或者在指定范围内生成随机整数。

### 语法
```python
# 介于 0 和 1 之间的随机实数
v0=rand() 
```

```python
# 在指定范围内的随机整数
v1=rand(<minimum value>,<maximum value>) 
```

### 参数
<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">minimum value</td>
      <td style="text-align:left">
        要生成的最小随机整数
      </td>
      <td style="text-align:left">整数常量</td>
    </tr>
    <tr>
      <td style="text-align:left">maximum value</td>
      <td style="text-align:left">
        要生成的最大随机整数
      <td style="text-align:left">整数常量</td>
    </tr>
  </tbody>
</table>

### 示例

```python
     var v0, v1
     var min=1
     var max=100
     v0=rand()          # 生成介于 0 和 1 之间的随机实数
     v1=rand(min,max)   # 生成介于 1 和 100 之间的随机整数
     end
```

[__SOURCE](10-etc/2-func/5-sig2int.md)
# 10.2.5 `sig2int`

使用 `sig2int` 函数，可以将特定范围的输入/输出信号表示为 `int` 类型值。

### 描述
- 输入要表示为 `int` 类型的输入/输出信号名称。
- 设置从输入/输出信号中读取多少位。

### 语法

```python
result=sig2int(<input/output signal>,<number of bits>)
```

### 参数
<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">输入/输出信号</td>
      <td style="text-align:left">
        输入/输出信号变量名称
      </td>
      <td style="text-align:left">输入/输出信号变量</td>
    </tr>
    <tr>
      <td style="text-align:left">位数</td>
      <td style="text-align:left">
        从输入/输出信号中读取的位数
      <td style="text-align:left">变量</td>
    </tr>
  </tbody>
</table>

### 示例

```python
     var result1,result2,result3
     result1=sig2int(di4,4)
     result2=sig2int(fb2.do0,1)
     result3=sig2int(fn1.di24,8)
     end
```

[__SOURCE](10-etc/3-sysvar/README.md)
# 10.3 系统变量
[__SOURCE](10-etc/3-sysvar/_acc_rate.md)
# `_acc_rate`

获取或设置速度曲线中的加速度。

### 描述

- 单位 : %
- 范围 : 1 到 100
- 默认值 : 100

### 语法

```python
var res
res = _acc_rate
```

### 示例

```python
   ...
   # 打印当前加速度，并设置为70%。
   print _acc_rate
   _acc_rate=70
   ...
   end
```
[__SOURCE](10-etc/3-sysvar/_dec_rate.md)
# `_dec_rate`

获取或设置速度曲线中的减速率。

### 描述

- 单位 : %
- 范围 : 1 到 100
- 默认值 : 100

### 语法

```python
var res
res = _dec_rate
```

### 示例

```python
   ...
   # 打印当前减速率，并设置为 70%。
   print _dec_rate
   _dec_rate=70
   ...
   end
```
[__SOURCE](10-etc/3-sysvar/_intr_no.md)
# `_intr.no`

`_intr.no` 系统变量是发生的中断号。

### 描述

当因为 `intr_def` 程序中的条件表达式被满足而发生中断时，您可以使用 `_intr.no` 来确定程序是由哪个中断号调用的。


### 语法

```python
var res
res = _intr.no
```


### 示例

```python
   ...
   if _intr.no==1  # 如果发生中断号 1 
   print "通过传感器 1 的激活，发生中断。"
   else if _intr.no==2 # 如果发生中断号 2 
   print "通过传感器 2 的激活，发生中断。"
   stop # 机器人停止
   endif
   ...
   end
```
[__SOURCE](10-etc/3-sysvar/_intr_target.md)
# `_intr.target`

`_intr.target` 系统变量调整机器人的目标位置达成状态。

### 描述

在移动语句中，当发生中断并在调用程序执行结束后返回到上一个程序的位置时，用于调整位置。

### 语法

```python
_intr_target=1
```

### 示例

```python
- _intr.target=-1
```

![](../../_assets/intr_target_1.png)


```python
- _intr.target=1 or 0
```
![](../../_assets/intr_target_2.png)
[__SOURCE](10-etc/3-sysvar/_spd_rate.md)
# `_spd_rate`

获取或设置播放速度。

### 描述

与 cond.set 相同的设置 - 播放速度。

- 单位 : %
- 范围 : 1 到 100
- 默认值 : 100

### 语法

```python
var res
res = _spd_rate
```

### 示例

```python
   ...
   # 如果播放速度低于 50%，则将其提高到 100%。
   if _spd_rate<50
     _spd_rate=100
   ...
   end
```
[__SOURCE](10-etc/3-sysvar/_task_enable.md)
# `_task.enable`

### 描述

一个系统变量，用于确定子任务是否处于活动状态。


### 语法

```python
var res
res = _task[1].enable
```


### 示例

```python
   ...
   if _task[1].enable==1  # 如果子任务 1 处于活动状态
   print "Subtask 1 is active"
   endif
   ...
   end
```
[__SOURCE](10-etc/3-sysvar/_tool.md)
# `_tool`

`_tool` 是一个用于读取或更改工具数据的系统变量。

### 描述

- 读取注册的工具数据（重量/质心/惯性）或更改工具数据。
- 如果工具数据未注册或成员无效，将会发生错误，并且作业执行将被中断。

### 语法

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

### 错误

- E14550 : 当工具数据的成员无效时发生。确保设置的工具数据的成员为质量、cx、cy、cz、ixx、iyy、izz。
- E14286 : 当赋值语句的右侧不是移位类型或工具变量的成员无效时发生。请正确指定右侧。

### 示例

```python
   var sft=Shift(100,20,30,0,0,0,"tool")
   _tool3=sft
   move L,spd=30%,accu=1,tool=3
   end
```
[__SOURCE](10-etc/3-sysvar/_vel_rpm_cmd.md)
# `_vel_rpm_cmd`

读取或设置电机旋转时控制附加轴速度的速度。

### 描述

附加轴必须在工装轴上设置为速度控制模式。<br>
单位为 rpm。您可以设置 -10000 到 10000 之间的值，默认值为 0。<br>
如果指定为 -，电机将反向旋转。

### 语法

```python
var res
_vel_rpm_cmd[6] = 1000 # 以 1000 rpm 的速度旋转 7 轴电机 
res = _vel_rpm_cmd[6] # 赋值 7 轴电机的旋转速度 
```

### 示例

```python
   ...
   # 打印当前 7 轴电机旋转速度后，将其设置为 1000 rpm。
   print _vel_rpm_cmd[6]
   _vel_rpm_cmd[6]=1000
   ...
   end
```
[__SOURCE](10-etc/3-sysvar/_weaving.md)
# `_weaving`

### 描述

`_weaving` 用于更改当前选定的编织条件。

### 语法

```python
_weaving.frequency=2
_weaving.angle=5
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">项目</th>
      <th style="text-align:left">含义</th>
      <th style="text-align:left">其他</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">编织</td>
      <td style="text-align:left">
         编织类型 (0=单次振动, 1=三角形, 2=L形, 3=圆形)
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">频率</td>
      <td style="text-align:left">
        频率[Hz]
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">左距离</td>
      <td style="text-align:left">
        向左的距离[mm]
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">右距离</td>
      <td style="text-align:left">
        向右的距离[mm]
      </td>
<td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">角度</td>
      <td style="text-align:left">
        角度[度]
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">偏移角度</td>
      <td style="text-align:left">
        偏移角度[度]
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">墙面方向</td>
      <td style="text-align:left">
        墙面方向 (0=垂直, 1=水平, 2=火炬方向)
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">前向角度</td>
      <td style="text-align:left">
        前向角度[度]
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">边界限制</td>
      <td style="text-align:left">
        边界限制 (0=有效, 1=无效)
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">段时间_1</td>
      <td style="text-align:left">
        段 (1~4) 移动时间[s]
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">段延迟_1</td>
      <td style="text-align:left">
        段 (1~4) 计时器（编织停止）[s]
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">height_sensing_mode</td>
      <td style="text-align:left">
        高度感应模式 (0=当前变化, 1=左固定, 2=右固定)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">side_sensing_mode</td>
      <td style="text-align:left">
        左/右感应模式 (0=中心, 1=左, 2=右)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">asymetric_sensing_ratio</td>
      <td style="text-align:left">
        非对称感应比例 (-50~50) [%]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">side_sensing_sensitivity</td>
      <td style="text-align:left">
        左右感应灵敏度 (0~10)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">height_sensing_sensitivity</td>
      <td style="text-align:left">
        高度感应灵敏度 (0~10)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
  </tbody>
</table>




### 示例

   weaving on,cnd=1
   move P,spd=50%,accu=3,tool=1
   _weaving.frequency=5    # 将编织频率更改为5Hz
   move P,spd=50%,accu=3,tool=1
   weaving off
   end


[__SOURCE](10-etc/3-sysvar/_pc.md)
# `_pc`

### 描述

`_pc` 用于获取当前程序计数器信息。 <br>
程序计数器由程序编号、步骤编号和功能编号组成。

### 语法

```python
var sno=_pc.cur_sno  # 分配当前步骤编号
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">项</th>
      <th style="text-align:left">含义</th>
      <th style="text-align:left">其他</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">cur_sno</td>
      <td style="text-align:left">
         光标当前所在的步骤编号
      </td>
      <td style="text-align:left">变量</td>
    </tr>
  </tbody>
</table>




### `cur_sno` 示例：如果未满足条件，则移动到上一个步骤。

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
