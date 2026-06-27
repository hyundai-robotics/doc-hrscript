
[__SOURCE](README.md)
# ${cont_model} 控制器功能手册 - 机器人语言 HRScript
[__SOURCE](0-about-this-manual/README.md)
# 关于手册
[__SOURCE](0-about-this-manual/precautions.md)
# 注意事项

{% include file="zh/precautions.md" %}
[__SOURCE](0-about-this-manual/safety-notice.md)
# 安全注意事项

{% include file="zh/safety-notice.md" %}

{% hint style="danger" %}
在用户脚本执行期间，逻辑错误或未满足的执行条件可能导致机器人行为异常，从而可能导致严重伤害或死亡。
{% endhint %}
[__SOURCE](1-intro/README.md)
# 1. 概述
[__SOURCE](1-intro/1-hrscript.md)
# 1.1 HRScript 的介绍

HD Hyundai Robotics 的 ${cont_model} 控制器允许用户使用一种称为 HRScript 的机器人语言编程机器人的任务。创建的程序可以保存为扩展名为 .job 的多个文件。

HRScript 是一种脚本语言，将由解释器逐行解释和执行，无需编译过程。它类似于 Python 或 JavaScript 语言，但具有更简单的语法。
[__SOURCE](2-basic-syntax/README.md)
# 2. 基本语法

描述本节的是 HRScript 的基本术语。作业程序的基本概念可以通过以下方法理解：定义变量的方法、使用运算符构造简单表达式以及将结果值赋给变量。
[__SOURCE](2-basic-syntax/1-statements.md)
# 2.1 声明

声明指的是成为作业程序执行单元的每个命令字符串。HRScript 每行只允许一个声明。请注意下面四个声明的写法，特别是它们的外观。

```python
     move P,po3,spd=80%,accu=1,tool=3 until do33
10   z_pos = (base_height+offset)*1.05
     # 机器人必须等待 sensor2 输入
     *err_handle
```

对于除了步骤声明（如移动声明等）之外的声明，您可以选择在行的开头添加行号（1 到 9999）。第二行中的数字 10 就是行号的示例。

声明前后有任意数量的空格或制表符都没有关系。

建议在声明中进行适当的缩进以提高可读性。缩进允许使用空格和制表符，并且在执行时不会影响操作。
[__SOURCE](2-basic-syntax/2-identifier.md)
# 2.2 标识符

命令、变量、函数和描述的标签必须赋予名称。这些名称统称为 `标识符`。在决定标识符时，必须遵守 HRScript 标识符的以下规则。

* 它只能由大写字母、小写字母、数字和下划线组成。
* 它区分大小写。（全局变量中的顶级数组名称除外）
* 第一个字符只能是小写字母、大写字母或下划线，而不能是数字。
* 它不应包含空格或制表符。
* 系统中已定义的标识符，例如 `如果 (if)` 和 `for` 不能使用。
* 长度没有限制。

以下显示了标识符的正确和不正确示例：

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

例外情况下，全球变量中的顶级数组名称不区分大小写。
（这是因为顶级全局数组以 .csv 文件保存，文件名不区分大小写。）

例如，以下两个变量不能一起使用：

    global MyArr = Array(10)
    global myarr = Array(10)

{% endhint %}
[__SOURCE](2-basic-syntax/3-statement-type/README.md)
# 2.3 声明的类型

HRScript 的四种声明类型如下：

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

三种类型的程序参数如下所示：

| 类型 | 语法 | 示例 |
| :--- | :--- | :--- |
| 位置参数 | &lt;value&gt; | P, po3 |
| 关键字参数 | &lt;keyword&gt; = &lt;value&gt; | spd=80%, accu=1, tool=3 |
| 介词参数 | &lt;preposition&gt; &lt;value&gt; | until do33 |

位置参数的角色由其位置决定，因此不应移动，并且必须始终位于程序的前面。

关键字参数应放在位置参数之后。然而，关键字参数之间的顺序不影响操作。

介词参数应放在最后。
[__SOURCE](2-basic-syntax/3-statement-type/2-assignment.md)
# 2.3.2 赋值语句

赋值语句由左侧、赋值运算符 \(=\) 和右侧组成。左侧 \(lvalue\) 必须是一个可以存储值的变量。常量或表达式不允许出现。

另一方面，右侧 \(rvalue\) 可以包含常量、变量和表达式。

```python
height=(500+margin)/2
```
[__SOURCE](2-basic-syntax/3-statement-type/3-comment.md)
# 2.3.3 注释语句

注释语句用于以易于理解的方式描述作业程序的内容。即使执行注释语句，也不会执行任何操作。如下面所示，描述附加在井号 \(\#\) 后面。它可以作为单独的语句使用或附加在另一个语句后面。

```python
# robot has to wait sensor2 input
var work_w,work_h  # width and height of a workpiece
```
[__SOURCE](2-basic-syntax/3-statement-type/4-label.md)
# 2.3.4 标签

一个标签用于标记根据goto语句要移动到的目标点。它由一个星号 \(\*\) 和一个标识符组成。
[__SOURCE](2-basic-syntax/4-hello-world.md)
# 2.4 第一个程序 - 你好，世界！

让我们创建一个简单的作业程序，在教学挂件屏幕上打印字符串。创建新作业后，记录如下的打印语句，并附上字符串参数 "你好，世界！"

```python
print "Hello, World !"
```

打印语句用于在教学挂件的作业面板底部打印值。现在，当你运行程序时，可以在作业面板的底部看到文本 "你好，世界！" 被打印出来。
[__SOURCE](2-basic-syntax/5-type/README.md)
# 2.5 数据类型
[__SOURCE](2-basic-syntax/5-type/1-type-string.md)
# 2.5.1 字符串数据类型

上一段中的第一个程序使用数据 "Hello, World!" 作为打印语句的参数，即字符串数据类型。字符串数据类型的值以双引号开始和结束。字符串的长度没有限制。

```python
print "Welcome to the Robot World."
```

以反斜杠 \(\\) 开头的序列表示字符串中的双引号或特殊字符。这个序列称为“转义字符”。

支持的转义字符如下面的表格所示。



|  |  |
| :--- | :--- |
| \" | 双引号 |
| \\ | 反斜杠 |
| \t | 制表符 |
| \n | 换行符 |

```python
print "Message:\nPlease, press \"OK\" button."

# Result of print
Message:
Please, press "OK" button.
```
[__SOURCE](2-basic-syntax/5-type/2-number-type.md)
# 2.5.2 数字数据类型

数字数据类型存储整数或实数。让我们使用打印语句进行打印。如果在打印语句中用逗号 \(,\) 分隔多个值，如下面的示例所示，每个值将用空格分隔显示。

```python
280
3.141592
-99
print 280, -99
```

在系统内部，整数和实数是分别处理的。每种数据大小如下：

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

# 结果输出
false
true
false
```
[__SOURCE](2-basic-syntax/5-type/4-array-object-type.md)
# 2.5.4 数组类型和对象类型

此外，还有数组类型和对象类型。将在第 4.1 节和第 4.2 节中进一步讨论这些内容。
[__SOURCE](2-basic-syntax/6-variable.md)
# 2.6 变量

变量可以存储值并具有标识符名称。变量分为全局变量和局部变量，二者之间的区别将在后面描述。局部变量的例子在这里首先描述。

变量可以使用 var 命令创建，如下所示。这被称为定义变量。可以通过在 var 命令后列举多个标识符一次性创建多个标识符。

```python
var myvar
var width, height, depth
```

将值存储到变量中称为“赋值”。赋值可以在定义变量时或在定义之后进行。如果在定义时没有进行赋值，则变量的默认数字值为 0。

```python
var myvar=0
var message, width=200
message="无效的输入值"
```

在 HRScript 中，\(=\) 并不意味着相等。它用作赋值运算符，意味着运算符右侧的值被赋给左侧的变量。存储在变量中的值可以通过 print 语句打印出来。

```python
var myvar=0
var message, width=200
message="无效的输入值"
print width, message
```

可以将不同的值赋给已经赋值的变量。之所以称为变量，是因为它的值可以改变。

```python
var width=200
width=300
```
[__SOURCE](2-basic-syntax/7-binary-hex-number.md)
# 2.7 二进制和十六进制

All the number type values previously described as examples are interpreted as decimal numbers. It can represent binary or hexadecimal values just by adding 0b or 0x prefixes, respectively, as shown in the following.

```python
var binary = 0b10010011
var hexadecimal = 0xFF4A38C0
```
[__SOURCE](2-basic-syntax/8-operator-expression.md)
# 2.8 运算符和表达式

在以下示例中，变量 margin 被添加到数字值 500，然后结果值除以 2。因此，计算得出的值被分配给一个名为“height”的变量。

```python
var height, margin=10
height=(500+margin)/2
print height
```

通过 print 语句，可以检查到表达式的结果 255 被分配给“height”。

通过将操作数（即值或变量）用各种运算符连接，可以创建一个表达式，并将结果分配给一个变量或用作语句的参数。

如果在没有分组的情况下使用加号和乘号，首先执行的操作会是什么？因为使用了一种称为“运算符优先级”的运算顺序，乘法和除法将优先于加法和减法执行。由于乘法的运算符优先级高于加法，即使乘号位于后面，乘法也会首先执行。

print 10+10\*2

当对字符串使用 \(+\) 运算符时，字符串将被连接。

```python
var name="axis1", type="rotational"
print name + ":" + type
```

HRScript 支持的运算符如下。数值越高，运算符优先级越高。也就是说，优先级高的运算符会先执行。

<table>
  <thead>
    <tr>
      <th style="text-align:left">运算符</th>
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
      <td style="text-align:left">乘法、除法、余数</td>
      <td style="text-align:left">300/3 ; 100, 8 mod 3 ; 2</td>
    </tr>
    <tr>
      <td style="text-align:left">+, -</td>
      <td style="text-align:left">加法、减法</td>
      <td style="text-align:left">300-100 ; 200</td>
    </tr>
    <tr>
      <td style="text-align:left">~</td>
      <td style="text-align:left">按位取反</td>
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
        <p>比较运算</p>
        <p>(!=) 表示不同，(==) 表示相等。</p>
      </td>
      <td style="text-align:left">
        <p>30 &lt;= 29 ; false</p>
        <p>response != &quot;ok&quot;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">not x</td>
      <td style="text-align:left">逻辑运算 NOT</td>
      <td style="text-align:left">not error_state</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>and</p>
        <p>or</p>
      </td>
      <td style="text-align:left">
        <p>逻辑运算 AND</p>
        <p>逻辑运算 OR</p>
      </td>
      <td style="text-align:left">
        <p>height&gt;100 and invert==false</p>
        <p>timeout or work_count&gt;3</p>
      </td>
    </tr>
  </tbody>
</table>

当操作数为数字或布尔值时，比较和逻辑运算的结果是布尔数据类型，其他运算的结果类型是数字数据类型。

在没有比较运算符的情况下使用布尔类型的操作数，意味着它的值是否等于 true。例如，下面这两行具有相同的含义。

```python
var result= timeout
var result= (timeout==true)
```

可以用于字符串的运算符是加法 \(+\)、比较 \(!=, ==\) 和赋值 \(=\)。字符串加法使得可以连接操作数字符串，如上所示。

比较运算确定一个字符串是否不同或相等。

```python
var response="ok"
print response=="ok"
print response=="ng"
```

有时，操作数的数据类型可能在运算过程中自动改变。

当使用比较运算符比较数字与字符串时，它们会作为字符串进行比较。

```python
print 123=="123" # true
```

当数字作为逻辑运算符的操作数时，0 将被视为 false，而非 0 将被视为 true。

```python
var count_a=1, count_b=0, height=100
print count_a and height>99
print count_b and height>99
```

“按位取反”和“左移/右移”是基于 32 位长度计算的。
[__SOURCE](2-basic-syntax/9-function/README.md)
# 2.9 函数

将角度60°转换为弧度值的过程是什么，或者找到变量mystr包含的字符串的长度？

HRScript提供了各种函数，通过参数接收输入，执行一些处理，并返回结果值。

函数可以作为表达式的一部分使用，如下所示。

```python
var dg=60, rd
rd=deg2rad(dg)

var limit=40, message="Input your code number"
var validity= len(message) < limit
```

HRScript提供的函数列表如下。 \(表格按名称的升序排列。\)
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
      <td>返回 <b>a</b> 的绝对值
      </td>
      <td>abs(-300)</td>
      <td>300</td>
    </tr>
    <tr>
      <td>acos(<b>a</b>)</td>
      <td>返回 <b>a</b> 的反余弦值，单位为弧度</td>
      <td>acos(0.5)</td>
      <td>1.0472</td>
    </tr>
    <tr>
      <td>asin(<b>a</b>)</td>
      <td>返回 <b>a</b> 的反正弦值，单位为弧度</td>
      <td>asin(0.5)</td>
      <td>0.5236</td>
    </tr>
    <tr>
      <td>atan(<b>a</b>)</td>
      <td>返回 <b>a</b> 的反正切值，单位为弧度</td>
      <td>atan(0.5)</td>
      <td>0.4636</td>
    </tr>
    <tr>
      <td>atan2(<b>a</b>, <b>b</b>)</td>
      <td>返回以 <b>a</b> 为 y 值，<b>b</b> 为 x 值的三角形的反正切值，单位为弧度</td>
      <td>atan2(2,1)</td>
      <td>1.1071</td>
    </tr>
		<tr>
			<td>ceil(x)</td>
			<td>返回 <b>x</b> 的向上舍入值。</td>
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
      <td>返回 <b>r</b> 的余弦值，单位为弧度</td>
      <td>cos(3.1415)</td>
      <td>-1</td>
    </tr>
    <tr>
      <td>deg2rad(<b>d</b>)</td>
      <td>返回 <b>d</b> 的弧度值，单位为度</td>
      <td>deg2rad(-90)</td>
      <td>-1.570796</td>
    </tr>
    <tr>
      <td>dist(<b>x</b>, <b>y</b>)</td>
      <td>返回从原点到 (<b>x</b>, <b>y</b>) 坐标的欧几里德距离</td>
      <td>dist(3.5,10)</td>
      <td>10.59481</td>
    </tr>
		<tr>
			<td>floor(x)</td>
			<td>返回 <b>x</b> 的向下舍入值。</td>
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
      <td>返回 <b>a</b> 和 <b>b</b> 之间的较大值
      </td>
      <td>max(-1.23, -3)</td>
      <td>-1.23</td>
    </tr>
    <tr>
      <td>min(<b>a</b>, <b>b</b>)</td>
      <td>返回 <b>a</b> 和 <b>b</b> 之间的较小值
      </td>
      <td>max(-1.23, -3)</td>
      <td>-3</td>
    </tr>
    <tr>
      <td>near(<b>a</b>, <b>b</b> [,<b>e</b>])</td>
      <td>如果 <b>a</b> 和 <b>b</b> 之间的实数值的差小于或等于 <b>e</b>，则返回 1；如果差大于 <b>e</b>，则返回 0
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
      <td>返回 <b>r</b> 的度值，单位为弧度</td>
      <td>rad2deg(1.570796)</td>
      <td>90</td>
    </tr>
		<tr>
			<td>round(x)</td>
			<td>返回 <b>x</b> 的四舍五入值。</td>
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
      <td>返回 <b>r</b> 的正弦值，单位为弧度</td>
      <td>sin(1.5*3.1415)</td>
      <td>-1</td>
    </tr>
    <tr>
      <td>sqr(<b>a</b>)</td>
      <td>返回 <b>a</b> 的平方根
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
      <td>返回 <b>r</b> 的正切值，单位为弧度</td>
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
      返回由格式重新解释的 v 值的二进制数据。<br>
			有关支持的格式，请参阅下面的 [Table 1]。
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
		<tr><td rowspan="7">小<br>端</td>
		     <td>u1</td><td>无符号 1 字节</td></tr>
		<tr><td>u2</td><td>无符号 2 字节</td></tr>
		<tr><td>s1</td><td>有符号 1 字节</td></tr>
		<tr><td>s2</td><td>有符号 2 字节</td></tr>
		<tr><td>s4</td><td>有符号 4 字节</td></tr>
		<tr><td>f4</td><td>浮点数 4 字节</td></tr>
		<tr><td>f8</td><td>双精度浮点数 8 字节</td></tr>
		<tr><td rowspan="7">大<br>端</td>
		     <td>U1</td><td>无符号 1 字节</td></tr>
		<tr><td>U2</td><td>无符号 2 字节</td></tr>
		<tr><td>S1</td><td>有符号 1 字节</td></tr>
		<tr><td>S2</td><td>有符号 2 字节</td></tr>
		<tr><td>S4</td><td>有符号 4 字节</td></tr>
		<tr><td>F4</td><td>浮点数 4 字节</td></tr>
		<tr><td>F8</td><td>双精度浮点数 8 字节</td></tr>
	</tbody>
</table>
[__SOURCE](2-basic-syntax/9-function/2-func-string.md)
# 2.9.2 字符串函数

Examples with var str="hello, world" executed;

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
      <td style="text-align:left">返回数字 <b>a</b> 的二进制表示的字符串</td>
      <td style="text-align:left">bin(0b0010)</td>
      <td style="text-align:left">&quot;10&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">chr(<b>a</b>)</td>
      <td style="text-align:left">返回字符串类型的ASCII代码为 <b>a</b> 的字符</td>
      <td
      style="text-align:left">chr(65)</td>
        <td style="text-align:left">&quot;A&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">double(<b>s</b>)</td>
      <td style="text-align:left">返回实数字符串 <b>s</b> 的实数类型值（只解释到能解释的位置，并丢弃其余部分。）</td>
      <td style="text-align:left">double(&quot;29.38E-2&quot;)</td>
      <td style="text-align:left">0.2938</td>
    </tr>
    <tr>
      <td style="text-align:left">hex(<b>a</b>)</td>
      <td style="text-align:left">返回数字 <b>a</b> 的十六进制表示的字符串</td>
      <td
      style="text-align:left">hex(0x7A2F)</td>
        <td style="text-align:left">&quot;7A2F&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">int(<b>s</b>)</td>
      <td style="text-align:left">返回整数字符串 <b>s</b> 的整数类型值（只解释到能解释的位置，并丢弃其余部分。）</td>
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
      <td style="text-align:left">返回字符串 <b>s</b> 的前 <b>n</b> 个字符的字符串</td>
      <td style="text-align:left">left(str, 3)</td>
      <td style="text-align:left">&quot;hel&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">len(<b>s</b>)</td>
      <td style="text-align:left">如果 <b>s</b> 是字符串，则返回字符串的长度，如果 <b>s</b> 是数组，则返回数组中的元素数量</td>
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
      <td style="text-align:left">返回从字符串 <b>s</b> 的第 <b>i</b> 个字符开始的 <b>n</b> 个字符的字符串（第一个字符的位置是0。）</td>
      <td
      style="text-align:left">mid(str, 3, 5)</td>
        <td style="text-align:left">&quot;lo, w&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">mirror(<b>s</b>)</td>
      <td style="text-align:left">返回字符串 <b>s</b> 的反向字符串</td>
      <td style="text-align:left">mirror(&quot;HELLO&quot;)</td>
      <td style="text-align:left">&quot;OLLEH&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">right(<b>s</b>, <b>n</b>)</td>
      <td style="text-align:left">返回字符串 <b>s</b> 的最后 <b>n</b> 个字符的字符串</td>
      <td style="text-align:left">right(str, 3)</td>
      <td style="text-align:left">&quot;rld&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">str(<b>a</b>)</td>
      <td style="text-align:left">返回数字 <b>a</b> 的十进制表示的字符串</td>
      <td style="text-align:left">str(13.25)</td>
      <td style="text-align:left">13.250000</td>
    </tr>
    <tr>
      <td style="text-align:left">strpos(<b>s</b>, <b>p</b>)</td>
      <td style="text-align:left">返回字符串 <b>s</b> 中与字符串 <b>p</b> 匹配的第一个位置（如果没有匹配的，则第一个字符的位置将为0或-1。）</td>
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
      <th style="text-align:left">用法示例</th>
      <th style="text-align:left">结果</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:right">date( )</td>
      <td style="text-align:left">
        <p>以字符串类型返回当前日期</p>
        <p>(YYYY-MM-DD 格式)</p>
      </td>
      <td style="text-align:left">date( )</td>
      <td style="text-align:left">&quot;2019-04-17&quot;</td>
    </tr>
    <tr>
      <td style="text-align:right">time( )</td>
      <td style="text-align:left">
        <p>以字符串类型返回当前时间</p>
        <p>(HH:MM:SS 格式)</p>
      </td>
      <td style="text-align:left">time( )</td>
      <td style="text-align:left">&quot;08:48:14&quot;</td>
    </tr>
    <tr>
      <td style="text-align:right">time("hh:mm:ss.00")</td>
      <td style="text-align:left">
        <p>以字符串类型返回当前时间及其小数秒</p>
        <p>(HH:MM:SS.00 格式)</p>
      </td>
      <td style="text-align:left">time("hh:mm:ss.000")</td>
      <td style="text-align:left">&quot;08:48:14.187&quot;</td>
    </tr>
    <tr>
      <td style="text-align:right">timer( )</td>
      <td style="text-align:left">返回从开机时起经过的时间，以秒为单位 (sec)</td>
      <td style="text-align:left">timer( )</td>
      <td style="text-align:left">2796.37</td>
    </tr>
  </tbody>
</table>
[__SOURCE](2-basic-syntax/9-function/4-func-creator.md)
# 2.9.4 构造函数

这些函数接收一个参数的输入，然后创建并返回一个对象。

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
        <p>如果指定两个或更多元素，则会创建多维数组。</p>
        <p>请参阅 &quot;<a href="../../4-array-object/1-array/3-array-creator">4.1.3 数组构造函数 - Array()</a>&quot;。</p>
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
        <p>请参阅 &quot;<a href="../../5-moving-robot/1-pose.md">5.1 姿态</a>&quot;。</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">姿态对象</td>
    </tr>
    <tr>
      <td style="text-align:left">Shift(element)</td>
      <td style="text-align:left">
        <p>创建并返回一个移动对象</p>
        <p>请参阅 &quot;<a href="../../5-moving-robot/2-shift.md">5.2 移动</a>&quot;。</p>
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
        <p>返回机器人当前姿势到 "crd" 坐标系统</p>
        <p>有关可用作 "crd" 元素的值，请参见 "<a href="../../5-moving-robot/1-pose.md">5.1 姿势</a>" 下的表。</p>
        <p>如果模式为 "cmd"，则为命令值；如果模式为 "cur"，则为当前值。</p>
        <p>"crd" 和 "mode" 参数可以省略，默认值分别为 "base" 和 "cur"。</p>
      </td>
      <td style="text-align:left">cpo("joint", "cmd")</td>
      <td style="text-align:left">存储机器人到轴坐标系统的命令值的姿势*</td>
    </tr>
    <tr>
      <td style="text-align:left">gather_state()</td>
      <td style="text-align:left">通过执行 <a href="../../10-etc/1-proc/1-gather.md">gather</a> 语句返回当前数据收集状态</td>
      <td style="text-align:left">gather_state()</td>
      <td style="text-align:left">
        0 : 不在收集中。<br>
        1 : 在收集中。<br>
        2 : 正在将收集的结果保存为文件。
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>mkucs(n,po)</p>
        <p>mkucs(n,po1,po2,po3)</p>
        <p>mkucs(n,"OXY",po1,po2,po3)</p>
      </td>
      <td style="text-align:left">
        <p>创建并注册第 n 个用户坐标系统对象</p>
        <p>请参阅 "<a href="../../5-moving-robot/5-mkucs.md">5.5 用户坐标系统 (UCS)</a>"。</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>0: 成功</p>
        <p>&lt;0: 错误代码</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">result()</td>
      <td style="text-align:left">对于一些过程，检查结果可能是必要的。如果在执行过程后立刻调用 result() 函数，可以返回执行结果。</td>
      <td style="text-align:left">result()</td>
      <td style="text-align:left"></td>
    </tr>
   <tr>
      <td style="text-align:left">mkshift(3,ref_po,mea_po,2.0) <br>
      mkshift(5,ref_po,mea_sft)
      </td>
      <td style="text-align:left">优化的移动值是根据多个参考姿势的测量姿势或移动数据计算并返回的。<br>
      如果第四个参数对应的容差被指定为大于 0，并且计算的移动值大于此值，则会停止并显示错误。<br>
      # 注意 <br>
      ref_po（参考姿势）和 mea_po（测量姿势）是姿势变量的数组类型，而 mea_sft（测量移动）是移动变量的数组类型。<br>
      如果没有对应于容差的第四个参数，则不会检测到错误。<br>
      我们目前支持最多 100 个位置。
      </td>
      <td style="text-align:left">sft1=mkshift(4,ref_po,mea_po,3.0)</td>
      <td style="text-align:left">移动</td>
    </tr> 
    <tr>
      <td style="text-align:left">calshift(po1,po2) <br>
      calshift(po1,po2,"TV")
      </td>
      <td style="text-align:left">返回两个姿势之间的差异作为移动值。<br>
      如果存在 "TV" 参数，则工具的垂直方向作为移动值返回。
      </td>
      <td style="text-align:left">sft1=calshift(po1,po2)</td>
      <td style="text-align:left">移动</td>
    </tr> 
    <tr>
      <td style="text-align:left">po.valid()
      </td>
      <td style="text-align:left">
        返回关于姿势对象的信息，以确定其是否在机器人的运动范围内。<br>
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
        返回关于姿势对象的信息，作为数组格式的字符串。<br>
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
        返回关于移动对象的信息，作为数组格式的字符串。<br>
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
        <p>执行 move ~ until 语句时，当满足 until 条件时，将返回当前姿势在 crd 坐标系统中的值。</p>
        <p>有关可用作 "crd" 元素的值，请参见 "<a href="../../5-moving-robot/1-pose.md">5.1 姿势</a>" 下的表。</p>
         <p>"crd" 参数可以省略，默认值为 "base"。</p>
      </td>
      <td style="text-align:left">upo(&quot;joint&quot;)
      </td>
      <td style="text-align:left">姿势*</td>
    </tr>

  </tbody>
</table>

\* 姿势是表示机器人姿态或工具尖端位置的数据类型。详细信息将在 "[5.1 姿势](../../5-moving-robot/1-pose.md)" 中描述。
[__SOURCE](2-basic-syntax/10-import.md)
# 2.10 `import`

### 描述

一些功能并不是 hrspace 的内置功能，但也以插件模块的形式提供支持。

某些模块作为默认选项预装，而其他模块则需要您安装它们。  
该模块必须在机器人语言中通过 `import` 语句加载到控制器中，才能使用。

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

例如，若要在机器人语言中进行以太网 TCP 或 UDP 通信，必须 `import` 名为 `enet` 的默认选项模块。

执行 `import` 后，在全局范围内创建一个名为 `enet` 的模块对象。如下面的示例 `enet.ENet()`，您可以访问模块对象的成员变量或调用成员函数，特别是通过调用成员函数中的 `creator`，您可以创建新对象。

### 示例

在下面的示例中，  
(1) `enet` 模块对象已被 `import`。  
(2) 调用 `enet.ENet()` 创建一个新的以太网套接字对象，并将其分配给名为 `cli` 的局部变量。  
(3) 将一个字符串分配给对象 `cli` 的成员变量 `ip_addr`。

```python
import enet # (1)
var cli=enet.ENet() # (2)
cli.ip_addr="192.168.1.172" # (3)
```

以如下方式编写代码时，效果也是一样的。

```python
import enet as enet_module # (1)
var cli=enet_module.ENet() # (2)
cli.ip_addr="192.168.1.172" # (3)
```

* 本节仅涵盖了 `import` 语句的粗略语法。您将在后面的章节中看到 `import` 的使用示例，这些章节描述模块功能。
[__SOURCE](3-flowcontrol-subprogram/README.md)
# 3. 流程控制语句和子程序

作业程序中的语句按从上到下的顺序逐行执行。然而，根据某些条件，语句可以在不被执行的情况下被跳过，或者某些语句可以被重复执行。让我们来看看可以以这种方式控制程序流程的控制语句。
[__SOURCE](3-flowcontrol-subprogram/1-address.md)
# 3.1 地址

在程序中不按顺序执行下一行而跳转到另一个位置称为“分支”。
地址是分支的目标。

定义地址有三种方式：

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
        介于 1~9999 之间的整数。可以附加在语句的左侧，而不是步骤上。
      </td>
      <td style="text-align:left">99</td>
    </tr>
    <tr>
      <td style="text-align:left">标签</td>
      <td style="text-align:left">
        标签不是你附加在语句上的语法，而是它本身就是一条语句。<br>
        形式为 * 后跟 <a href="../2-basic-syntax/2-identifier">标识符</a>。但是，标识符不能超过 128 个字符。
      </td>
      <td style="text-align:left">*timeout</td>
    </tr>
    <tr>
      <td style="text-align:left">步骤号</td>
      <td style="text-align:left">
        步骤号会自动附加在递增一步的步骤上。<br>
        形式为 S 后跟步骤的数字。你可以指定 S1~S999。
      </td>
      <td style="text-align:left">S15</td>
    </tr>
  </tbody>
</table>


在下面的示例中，` (10)` 在第二条语句中是行号，`*err_handle` 是标签，`S12` 是步骤号。

```python
     move P,po3,spd=80%,accu=1,tool=3 until do33
  10 z_pos = (base_height+offset)*1.05
     # 机器人必须等待传感器2的输入
     *err_handle
S12  move P,spd=80%,accu=1,tool=3
```
[__SOURCE](3-flowcontrol-subprogram/2-stop-wait/README.md)
# 3.2 停止或等待语句

此语句可以停止程序的执行，或使其等待一定时间，直到条件满足。
[__SOURCE](3-flowcontrol-subprogram/2-stop-wait/1-stop.md)
# 3.2.1 ` (stop)`

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

这将停止程序。当处于连续播放模式或重启模式时，执行将从主程序的开始重新启动。

### 语法

end

### 示例

```python
move p,spd=70%,accu=1,tool=0
move p,spd=70%,accu=1,tool=0
end
```
[__SOURCE](3-flowcontrol-subprogram/2-stop-wait/3-delay.md)
# 3.2.3 `时间延迟 (delay)`

### 描述

在等待指定时间后，可以进展到下一个命令语句。

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
      <td style="text-align:left">等待时间</td>
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
# 3.2.4 `等待 (wait)`

### 描述

在指定条件变为真之前，等待后使其能够移动到下一个命令语句。

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
      <td style="text-align:left">超时超过时将跳转到的地址。</td>
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

使能够在没有条件的情况下转到不同的地址。
[__SOURCE](3-flowcontrol-subprogram/3-branch/1-goto.md)
# 3.3.1 `goto`

### Description

使能够跳转到指定地址。

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
        分支地址<br/>
        在行号的情况下，允许使用算术表达式。
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
# 3.3.2 `gosub`~`retsub`

### 描述

当遇到 `gosub` 语句时，它会分支到指定的地址。
当遇到 `retsub` 语句时，它会返回到 gosub 语句之后的下一个位置。
`gosub` 可以嵌套多层，且嵌套的数量没有限制。

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
        <p>分支到的地址</p>
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

这些语句允许根据某些条件执行或不执行某个操作。
[__SOURCE](3-flowcontrol-subprogram/4-conditional/1-simple-if.md)
# 3.4.1 单行 `如果 (if)`

### 描述

单行 `如果 (if)` 语句的形式如下：如果 &lt;布尔表达式&gt; 为真，则将发生跳转到 &lt;地址&gt;。如果为假，则将移动到下一个语句。

### 语法

```python
if <bool expression> then <address>
```

### 示例

以下是单行 if 语句的示例。如果压力大于限制的条件为真，则将发生跳转到标签地址 "\*err"，从而可以打印出压力过高的警告。如果条件为假，则将一个接一个地执行下一个语句，因此将打印 "正常运行中 "，结束程序。

```python
var pressure=95, limit=90
if pressure > limit then *err
print "normal operation."
end
*err
print "warning: pressure is too high."
```
[__SOURCE](3-flowcontrol-subprogram/4-conditional/2-if-endif.md)
# 3.4.2 `如果 (if)`-`endif`

### 说明

如果单行 `如果 (if)` 语句为真，则仅会执行分支到特定地址的操作。如果需要执行其他操作或多个语句，则应使用 `如果 (if)`-`endif` 块。

格式如下：如果 &lt;布尔表达式&gt; 为真，则 `如果 (if)` 和 `endif` 之间的多个&lt;语句&gt;将按顺序执行。如果 &lt;布尔表达式&gt; 为假，将跳过到 `endif` 后的位置，而不执行 &lt;语句&gt;。

### 语法

```python
if <bool expression>
	<statement>
	...
endif
```

### 示例

在以下示例中，如果压力大于限制，将执行以下赋值和打印语句。否则，将跳转到末尾而不执行这些语句。

```python
var pressure=95, limit=90, exceed
if pressure > limit
	exceed = pressure - limit
	print "warning: pressure is too high."
endif
end
```

在示例程序中，`如果 (if)` 和 `endif` 之间的语句缩进两个空格。这些语句的缩进使其更容易识别它们是嵌套在 `如果 (if)` 和 `endif` 之间的代码块。
[__SOURCE](3-flowcontrol-subprogram/4-conditional/3-if-else-endif.md)
# 3.4.3 `如果 (if)`-`else`-`endif` 语句

### 描述

如果表达式为假，并且 `如果 (if)` 有要执行的语句，则使用以下形式：

如果表达式为真，将执行语句 A。如果为假，将执行语句 B。

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
	print "警告: 压力过高."
else
	print "处于正常运行中."
endif
end
```
[__SOURCE](3-flowcontrol-subprogram/4-conditional/4-if-elseif-else-endif.md)
# 3.4.4. `如果 (if)`-`elseif`-`else`-`endif`

### Description

在多个条件的情况下，可以使用以下形式的 `elseif` 语句。

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
	print "警告：压力过高。"
elseif pressure > limit_m
	print "通知：压力偏高。"
else
	print "处于正常运行状态。"
endif
end
```
[__SOURCE](3-flowcontrol-subprogram/4-conditional/5-switch-case-break-end_switch.md)
# 3.4.5 `切换 (switch)`-`case`-`break`-`end_switch`

### Description

A `切换 (switch)` statement evaluates a numeric expression and compares it with the resulting value of the numeric expression designated by a `case` statement. It is executed from the `case` statement of equal value until a `break` statement is encountered.

In the following example, if the resulting value of Expression `X` is equal to the resulting value of Expression `B1` or `B2`, \(1\) through \(3\) will be executed, and it will move to the point of the `end_switch` statement \(note that there is no `break` below the command statement B\). Meanwhile, if the resulting value of Expression `X` is equal to that of Expression `C按钮 (C)`, \(2\) through \(3\) will be executed.

{% hint style="warning" %}
If the `break` statement is omitted, the statements in the following `case` will also be executed. Users familiar with the `CASE` statement in Hi5a HR-BASIC should take note of this behavior.
{% endhint %}

If the resulting value of Expression `X` is not equal to that of any `case` statement, it will be moved to the `默认值 (default)`, and \(4\) through \(5\) will be executed. Then, the `默认值 (default)` section may be omitted.

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
# 3.5. 嵌套控制流语句

### 描述

在控制语句块中，可以放置另一个控制语句块，如以下示例所示。在以下格式中，显示了两个嵌套级别，但可以根据需要进行多个嵌套级别。

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
		print "警告: 压力过高。"
	else
		print "在正常操作中。"
	endif
endif
end
```
[__SOURCE](3-flowcontrol-subprogram/6-loop/README.md)
# 3.6 循环语句

循环语句可用于需要多次重复相同操作的情况。
[__SOURCE](3-flowcontrol-subprogram/6-loop/1-for-next.md)
# 3.6.1 `for`-`next`

### 描述

`for`~`next` 语句的格式，用于重复相同的操作，如下所示。

首先，初始值将分配给索引变量。当在执行 `for` 语句下的语句时遇到 `next` 语句时，索引变量将增加/减少值，并从 `for` 语句的点开始重复。当索引变量超过结束值时，重复将结束。

如果未指定步骤，将应用 1。

### 语法

```python
for <index variable>=<initial value> to <end value> [step <increment/decrement value>]
	<statement>
	...
next
```

### 示例

以下显示了一个例程的示例，该例程使用 `for`-`next` 语句将 1 累加到 10。当重复结束时，将在屏幕上打印 11 和 55。

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

`break` 和 `continue` 用于前一部分中解释的 `for`~`next` 语句之间。

- 当在 `for`~`next` 块中遇到 `break` 时，循环停止其重复并转向 `next` 语句。
- 当在 `for`~`next` 块中遇到 `continue` 时，它不会继续到下一个语句，而是对索引变量进行增量/减量，并转向 `for` 语句。

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

这是一个使用 `for`~`next` 语句输出数组中所有名称的示例，除了字符超过 5 的名称，但在遇到空字符串时停止。

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

结果

```python
Anna
James
Tom
```
[__SOURCE](3-flowcontrol-subprogram/7-call-jump/README.md)
# 3.7 `call`, `jump` 语句和子程序

如果将整个大规模机器人操作创建为一个作业程序，则程序会变得庞大和复杂，这使得添加功能或查找和解决问题变得困难。

为了程序的可维护性，最好将构成整个程序的单元操作划分为子程序。例如，当例程，如与传感器通信的例程、利用接收的数据计算工具尖端目标位置的例程，以及在发生错误时生成适当消息的例程，变为单独的子程序并允许主程序调用它们时，将更容易掌握程序的整体结构。这在其他项目中重用划分的子程序时也会很有帮助。
[__SOURCE](3-flowcontrol-subprogram/7-call-jump/1-call.md)
# 3.7.1 `call`

### 描述

在 HRScript 中，主程序和子程序之间在格式上没有显著区别。通过启动按钮或信号执行的第一个作业是主程序，所有通过 `call` 语句调用的其他作业都是子程序。

### 语法

```python
call <作业编号, 文件名, 或用户函数名> [,参数 1,参数 2,...]
```

在 `call` 语句之后指定作业文件名的作业编号（不包括扩展名）。然后，当程序 ` (A)` 正在执行时，如果遇到 `call (B)`，将停止执行 ` (A)`，并继续执行子程序 ` (B)` 的第一条语句。如果在执行 ` (B)` 时遇到 `end` 或 `return` 语句，程序 ` (A)` 将在返回到之前调用的程序 ` (A)` 的 `call` 语句的下一条语句的位置继续执行。

### 示例

以下显示了通过 `call` 语句调用的子程序的示例及结果。将程序划分为两个部分似乎毫无意义，因为子程序必须处理仅一个打印语句。然而，稍后将显示一个更实际的示例。

* 请参阅 [3.7.3 def](./3-def.md) 以获取调用用户函数的示例。

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
# 3.7.2 参数和 `param`, `return`

在作业程序中，正式参数作为输入和输出传递的通道。`param` 语句将在作业程序的开头定义正式参数。

在以下示例中，作业编号 105 被命名为 "dist2d"，因为它是一个子作业，获取从原点到坐标值 \(x, y\) 的欧几里得距离并返回给 len。

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

在作业编号 1 中，dist2d 子程序通过 `call` 语句被调用，并传递了 "x, y"，这些是局部变量。在 dist2d 子程序中，使用 `param` 语句定义的 "dx" 和 "dy" 被称为 "正式参数"，而传递给 `call` 语句的 "x, y" 被称为 "实际参数"。

dist2d 程序通过 `return` 语句将结果值传输到外部目的地。返回值可以通过在被调用程序中调用 result\(\) 函数来获取。

(一个 `return` 语句和一个 `end` 语句的作用相同，因为它们结束一个被调用的程序并返回到主程序。然而，`return` 语句与 `end` 语句不同，因为前者可以指定作为元素的结果值)。
[__SOURCE](3-flowcontrol-subprogram/7-call-jump/3-def.md)
# 3.7.3 `def` (定义用户函数)

since V60.05-06

### 描述

您可以在作业中使用 `def` 语句定义用户函数，并使用 `call` 语句调用它。与 `param` 语句类似，`def` 语句可以指定一个正式参数列表。`call` 语句的实际参数值会传递给正式参数。
由 `def` 语句定义的函数在执行 `return` 语句或 `end` 语句时返回到 `call` 语句后的下一个语句。

用户函数是通过名称而不是数字进行调用的，因此其可读性优于子程序。您可以将多个相关函数分组到一个子程序中，以改善项目结构。

### 语法

```python
def <用户函数名称> [,parameter1[=默认值],parameter2[=默认值],...]
```

在 `def` 后指定用户函数名称。函数名称必须遵循 [2.2 标识符](../../2-basic-syntax/2-identifier.md) 部分中定义的规则。此外，它应该是唯一的全局名称。请注意不要与其他函数名称或其他变量名称重复。
之后，指定正式参数。您还可以为每个参数指定默认值。如果您在 `call` 语句中省略实际参数，则正式参数将初始化为默认值。如果您开始为特定正式参数指定默认值，则必须为最后一个参数之前的所有参数指定默认值。

```python
# 正式参数默认值的示例
def set_work,mass,cx=0,cy=0,cz=0 # 合法示例
def set_work,mass,cx=0,cy,cz     # 非法示例
```

### 示例

以下是使用 `call` 语句调用用户函数的示例及其结果。我们在前面章节中展示了欧几里得距离的示例来描述子程序。现在让我们定义欧几里得距离和曼哈顿距离的用户函数，并分别调用它们。

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

结果
```python
euclid= 13.7419
manhattan= 17.8
end
```
[__SOURCE](3-flowcontrol-subprogram/7-call-jump/4-jump.md)
# 3.7.4 `jump`

### 描述

此格式与 `call` 语句的格式完全相同，其执行动作也类似于 `call` 语句。

唯一的区别是，虽然 `call` 语句使用 `end` 语句返回到主程序，`jump` 语句则不返回。

### 语法

```python
jump <工作编号或文件名> [,参数 1,参数 2,???]
```



### 示例

如果将本示例程序的 `jump` 语句替换为 `call` 语句，替换后的程序结果将如下所示。当遇到子程序 \(0102\_err\) 的 `end` 时，动作周期将结束。如果执行下一个动作周期，主程序 \(0001\) 将从头开始执行。


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

例子仅使用通过 var 语句定义的局部变量的例子来描述。局部变量是在一个作业程序中通过 var 语句创建的，当程序在遇到结束语句后结束时，它们会被自动销毁。此外，其他程序无法读取或写入它们的值。

### 例子

"main\_v" 是一个仅在 0001.job 内部可访问的局部变量，而 "sub\_v" 是一个仅在 0107.job 内部可访问的局部变量。从另一个程序访问它将导致错误。

局部变量 "x" 在 0001.job 和 0107.job 中都被定义。分别在两个程序中定义的局部变量 "x" 名称相同但不同。因此，在子程序 0107 中为变量 "x" 设置的值 5 返回到主程序 0001 后将打印 3，而不是 5。

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
# 3.8.2 全局变量

### 描述

另一方面，定义为全局的全局变量可以始终从所有作业程序中访问。如果全局变量已经定义，即使通过结束语句或主程序的 R0 \[Enter\] 操作重置程序循环，也不会被清除。

### 示例

如果首先执行全局 x，将创建一个变量 x，并将其值初始化为默认值 0。然后，它将在下一行增加到 1。如果在下一个程序循环中再次执行全局 x，则不会再次定义，而是保留值 1，因为 x 已经被定义。另一方面，全局 y=10 将进行定义和赋值，因此当在下一个程序循环中执行时，变量 y 的值将重置为 10。

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
        <p>end
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

因此，如果要将全局变量用作程序循环次数的计数器，则不应在定义时赋值。

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
        <p>end
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
# 3.8.3 优先级

当存在同名的局部变量和全局变量时，将优先访问局部变量。例如，当执行 0005.job 时，如下所示，全局变量 x 和局部变量 x 将同时存在。此时，如果读取 x 值，将会读取局部变量的值。在 0005.job 返回到 0001.job 后，如果读取 x 值，将会读取全局变量，因为此时只存在全局变量。

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

数组是一种变量类型，可以在单个名称下收集和存储多个值，并通过索引号访问。

数组被定义为 `var` 或 `global`，与其他变量一样。

{% hint style="warning" %}
[全局变量中顶级数组的名称对大小写不敏感，因此请注意。](../../2-basic-syntax/2-identifier.md)
{% endhint %}


数组的定义和访问格式如下。

|  |  |
| :--- | :--- |
| 定义 | var array name = \[ Value, Value, ...\] |
| 访问 | Array name \[Index\] |

构成数组的值称为 `elements.` 距离，在以下示例中，数组总共有五个元素。索引从0开始。`distances` 的元素0和元素1分别是10和10.5。



使用 \[ \] 操作符读写数组特定元素的值。以下是定义和访问对象的示例。

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



可以通过使用 `len`\(\) 函数获得数组中的元素数量。之前，`len`\(\) 函数被引入为获取字符串长度的函数。如果将数组作为 `len`\( \) 的参数，将返回数组中的元素数量。

<table>
  <thead>
    <tr>
      <th style="text-align:left">函数名称</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">用法示例</th>
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



`for-next` 语句主要用于对数组的所有元素执行某些处理。

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



数组中存储的值可以是不同类型的，这并不重要。

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
</table>
[__SOURCE](4-array-object/1-array/2-md-array.md)
# 4.1.2 多维数组

数组也可以作为数组的元素嵌套。当访问多维数组的元素时，可以连续使用`[ ]`运算符。在以下示例中，`arr_y`是一个二维数组。\(1\)

`arr_y[1]`是索引1的元素数组，即`["abc", "jqk", "xyz"]`，并将其分配给新变量`arr_x`。\(2\)

因此，`arr_x[1]`是`jqk`，而`arr_y[1][2]`是`xyz`，因为它指向`arr_y[1]`的`[2]`。

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

仅用`[ ]`表示法创建一个包含数百个元素的数组是困难的。通过调用构造函数可以创建任意数量的数组。每个元素将被初始化为 0。

```python
var name = Array(900)	# 创建一个包含 900 个元素的数组
```

如果指定两个或更多元素，可以创建多维数组。在以下的三维数组示例中，`[4]`是最低维度。

```python
var name = Array(3,2,4)	# 创建 [3][2][4] 个三维数组
# [ [[0,0,0,0], [0,0,0,0]], [[0,0,0,0], [0,0,0,0]], [[0,0,0,0], [0,0,0,0]] ]
```
[__SOURCE](4-array-object/1-array/4-array-append.md)
# 4.1.4 `append_arr` 过程用于向数组添加元素

支持版本 V60.32-00

`append_arr` 过程可用于向数组添加元素

```python
var arr = [1, 2]
append_arr arr, 3   # 将 3 添加为 arr 的一个元素
print arr       # [1, 2, 3]
```

任何值，包括另一个数组，都可以作为元素附加，因为数组可以包含不同类型的元素。

```python
var arr = [1, 2]
append_arr arr, [3, 4]  # 将 [3, 4] 作为 arr 的一个元素附加
print arr           # [1, 2, [3, 4]]
```
[__SOURCE](4-array-object/1-array/5-array-extend.md)
# 4.1.5 `extend_arr` 过程用于将一个数组的所有元素添加到另一个数组

支持版本 V60.32-00

`extend_arr` 过程可用于将一个数组的所有元素添加到另一个数组。

```python
var arr = [1, 2]
var brr = [3, 4]
extend_arr arr, brr
print arr   # [1, 2, 3, 4]
```

可以如下使用。

```python
var arr = [1, 2]
extend_arr arr, [3, 4, 5]
print arr   # [1, 2, 3, 4, 5]
```
[__SOURCE](4-array-object/2-object.md)
# 4.2 对象

如之前所见，发现数组可以存储多个元素值，并通过索引访问。

对象与数组类似，都是用来存储多个元素值。不同之处在于，通过键来访问对象，而不是通过索引。此外，键是字符串，而不是数字。

对象的定义方式与其他变量一样，是 `var` 或 `global`。对象的定义和访问格式如下。

|  |  |
| :--- | :--- |
| 定义 | var object name = { key : value, key : value, ...} |
| 访问 | Object name key |




以下是定义和访问对象的示例。

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



对象的键必须符合标识符的格式，但元素的值可以是任何类型，也可以是不同类型。

对象可以包含其他对象或数组作为其元素。同样，数组也可以包含其他数组或对象作为其元素。在以下示例中，“work”是一个对象，包含“size”，它是一个对象，以及“heights”，它是一个数组。

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
      <td style="text-align:left">结果</td>
      <td style="text-align:left">false, 80, 87.600000</td>
    </tr>
  </tbody>
</table>
[__SOURCE](4-array-object/3-array-object-assignment.md)
# 4.3 数组和对象的复制赋值

如果赋值语句的右侧包含对象变量，则右侧变量的整个值将被复制到左侧的变量。 当数组或对象以复杂的方式将子数组和子对象包含为元素值时，这种包含结构将被复制，这称为深复制。

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
# 4.4 引用调用和值调用

在第 3.4 节中给出的 `call` 语句和 `jump` 语句的描述中，解释了形式参数和实际参数的概念。当实际参数被传送到子程序时，如果子程序在更改参数的值后结束，这些更改会反映到主程序中吗？

例如，假设有一个子程序 `0005_pow3.job` 将一个值提升到立方，如下所示：

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

虽然我们预计输出应该是 8，因为 2x2x2 等于 8，但结果却是 2。这是因为，当一个数值类型的实际参数被传送到子程序时，值是作为参数被复制的。换句话说，在 \(1\) 中，由于立方的值被赋值给了复制版本，因此没有影响原参数 x 的值。

因此，教学程序应进行修正，以便通过返回语句传送结果值。

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
      <td style="text-align:left">结果</td>
      <td style="text-align:left">8</td>
    </tr>
  </tbody>
</table>

另一方面，在数组或对象的情况下，传送的是实际参数的引用，而不是复制版本。引用指的是参数的位置。

在下面的例子中，子程序 0006\_pow3.job 将数组的每个元素的立方值提升，实际参数数组的元素值被更改。

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
      <td style="text-align:left">结果</td>
      <td style="text-align:left">[27, 8, 64]</td>
    </tr>
  </tbody>
</table>

当调用子程序时，如果传送的是实际参数值的复制版本，则称为值调用；如果传送的是引用，则称为引用调用。是否为值调用或引用调用由以下值的类型决定：

|  |  |
| :--- | :--- |
| 值调用 | 布尔、数值和字符串类型 |
| 引用调用 | 数组和对象类型 |

![](../_assets/image_3.png)
[__SOURCE](5-moving-robot/README.md)
# 5. 使用机器人语言移动机器人

在理解表达机器人目标位置的姿态后，让我们学习移动机器人的指令。
[__SOURCE](5-moving-robot/1-pose.md)
# 5.1 位姿

位姿是嵌入在 ${cont_model} 控制器中的对象类型，表示机器人每个轴或工具尖端的笛卡尔坐标和方向。

通过调用构造函数 `Pose()` 来创建位姿。所有函数参数都是位置参数。第一个字符串元素被识别为 `format`，第二个字符串元素为 `config`。其余元素均为数值类型。

### format
多个子元素，包括坐标系，用分号 (;) 分隔列出。每个子元素都是可选的，可以按任何顺序出现。

<table>
  <tr>
    <th>子元素名称</th>
    <th>类型</th>
    <th>描述</th>
  </tr>
  <tr>
    <td>crd</td>
    <td>字符串</td>
    <td>坐标系。<br>如果省略，则使用关节坐标系。<br>请参见下表。</td>
  </tr>
  <tr>
    <td>sync(p1,p2)</td>
    <td>p1, p2 : 实数</td>
    <td>传感器同步 (1 或 2 个位置值)</td>
  </tr>
  <tr>
    <td>mi(mech#[, ...])</td>
    <td>每个机械数字 : 整数 0~7</td>
    <td>机械配置。<br>(mi 代表 mech.info.)<br>如果省略，则包含所有机械。</td>
  </tr>
</table>

格式示例；
```python
"base,mi(0,2)" # 基坐标，包含机械 0 和 2
"" # 坐标省略（关节），无传感器同步，机械信息省略（所有机械）
"sync(20.5,-12.0),robot" # 传感器同步（pos.1=20.5, pos.2=-12.0），机器人坐标
```

{% hint style="info" %}
cfg 元素指定机器人配置。有关更多信息，请参阅 ${cont_model} 控制器操作手册中的 "[2.3.2.2 基础和机器人记录坐标](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/2-operation/3-step/2-step-pose-modify/2-base-robot-crd-sys?cont_model=${cont_model})"。
{% endhint %}

```python
var <pose 变量名称> = Pose(j1, j2, j3, ...)		# 轴坐标
var <pose 变量名称> = Pose(x, y, z, rx, ry, rz, j7, j8,..., crd, cfg)		# 基坐标
```

请参考以下创建 6 轴 + 1 个附加轴和笛卡尔 + 1 个附加轴的位姿示例。

```python
var po1 = Pose(10, 90, 0, 0, -30, 0, -1240.8)				# 轴坐标
var po2 = Pose(1850, 0, 2010.5, 0, -90, 0, -1240.8, "base", "fl;r2")	# 基坐标
var po3 = Pose(-1140.8, "mi(2)")	# 关节坐标，机械 2
```

或者，可以使用单个数组或字符串参数调用位姿构造函数。通过这种方式，可以将文件或数据转换为位姿，通过远程通信获取并使用。

```python
var <pose 变量名称> = Pose(array)
var <pose 变量名称> = Pose(string)
```

请参考以下示例。

```python
var arr = [10, 90, 0, 0, -30, 0, -1240.8]
var str = "[1850, 0, 2010.5, 0, -90, 0, -1240.8, \"base\", \"fl;r2\"]"
var po3 = Pose(arr)
var po4 = Pose(str)
```

位姿对象的元素可以使用以下键访问。



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
    <td>轴数</td>
    <td> </td>
  </tr>
   </tr>
    <tr>
    <td>j1~j32</td>
    <td>实数</td>
    <td>8 字节实数</td>
    <td>轴值</td>
    <td>毫米，度</td>
  </tr>
   </tr>
    <tr>
    <td>x, y, z</td>
    <td>实数</td>
    <td>8 字节实数</td>
    <td>工具在笛卡尔坐标中的位置</td>
    <td>毫米</td>
  </tr>
   </tr>
    <tr>
    <td>rx, ry, rz</td>
    <td>实数</td>
    <td>8 字节实数</td>
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
    <td>基</td>
    <td>基坐标</td>
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
    <td rowspan="7">可以通过用“;”分隔进行组合。</td>
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
    <td>自动</td>
    <td>自动（自动决策）</td>
    <td></td>
  </tr>
  <tr>
    <td>mechinfo</td>
    <td>整数</td>
    <td>-1 ~ 255</td>
    <td>位字段<br>(bit0:M0, bit1:M1, .... bit7:M7)<br>-1表示所有机械。</td>
    <td>仅设置与包含的机械对应的位为 1。</td>
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

1. 对于 V60.06-06 或更早版本，`fl` 是 `non-fl`。

位姿元素值可以如下示例所示进行访问。

```python
po1.j2 = po1.j2 + 5
print po2.z, po2.cfg
```
[__SOURCE](5-moving-robot/2-shift.md)
# 5.2 Shift

Shift 是嵌入在 ${cont_model} 控制器中的对象类型，表示姿态的变化值。

Shift 通过调用构造函数 `Shift()` 创建。所有函数参数均为位置参数。同时，`crd` 和 `cfg` 为字符串类型，其余为数字类型。

```python
var <shift variable name> = Shift(j1, j2, j3, ...)				# 轴坐标
var <shift variable name> = Shift(x, y, z, rx, ry, rz, j7, j8,..., crd)		# 基坐标
```

参考以下创建 6 轴 + 1 额外轴和笛卡尔 + 1 额外轴的 Shift 示例。

```python
var sft1 = Shift(30, 0, 0, 0, -5.8, 0, -120)				# 轴坐标
var sft2 = Shift(0, 0, 55.2, 0, -5, 0, -120, "base")			# 基坐标
```

或者，可以使用单个数组或字符串参数调用构造函数 Shift。通过此方式，可以将文件或数据转换为 Shift，通过远程通信获取并使用。

```python
var <shift variable name> = Shift(array)
var <shift variable name> = Shift(string)
```

参考以下示例。

```python
var arr = [30, 0, 0, 0, -5.8, 0, -120]
var str = "[0, 0, 55.2, 0, -5, 0, -120, \"base\"]"
var sft3 = Shift(arr)
var sft4 = Shift(str)
```

可以使用以下键访问 Shift 对象的元素。

![](../_assets/image_7.png)
[__SOURCE](5-moving-robot/3-pose-expression.md)
# 5.3 姿态表达

结果值成为姿态的表达式称为 `姿态表达式`。

以下所有形式都被识别为姿态。

```python
Pose
Pose+Shift
Pose-Shift
Pose+Shift+Shift+...
```

请参考以下将姿态表达式的结果分配给另一个姿态变量的示例。

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

The `移动 (move)` statement is a procedure for moving the robot. The format is as follows.

### Description

机器人的工具提示移动到位姿位置。

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
        <p>P: 轴插补;</p>
        <p>L: 线性插补;</p>
        <p>C: 圆形插补,</p>
        <p>SP: 静止轴插补,</p>
        <p>SL: 静止工具线性插补,</p>
        <p>SC: 静止工具圆形插补</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Pose/Shift</td>
      <td style="text-align:left">
        <p>目标姿态（位姿）移动到</p>
        <p>如果有隐藏位姿，则将被省略。</p>
        <p>如果指定了带有+或-符号的移位表达式，（隐藏位姿+移位表达式）将作为目标姿态。</p>
      </td>
      <td style="text-align:left">位姿表达式或签名移位表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">Speed</td>
      <td style="text-align:left">
        <p>工具提示的移动速度</p>
        <p>应添加单位（mm/sec, cm/min, sec, %）。</p>
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">Accuracy</td>
      <td style="text-align:left">
        <p>算术表达式</p>
        <p>值越低，越准确。如果为0，操作将不连续地发生。</p>
      </td>
      <td style="text-align:left">0~7</td>
    </tr>
    <tr>
      <td style="text-align:left">Tool number</td>
      <td style="text-align:left">机器人操作时使用的工具的编号</td>
      <td
      style="text-align:left">0~31</td>
    </tr>
      <tr>
      <td style="text-align:left">Assignment statement</td>
      <td style="text-align:left">
        <p>当移动开始时，将从左到右顺序执行要执行的赋值语句。</p>
      </td>
      <td style="text-align:left">True if not 0 False if 0
      <p>"&lt;assignment statement1;assignment statement2;...&gt;"<\p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Conditional expression</td>
      <td style="text-align:left">
        <p>一旦条件表达式为真，机器人操作将结束，指定的姿态被认为已达到。</p>
        <p>条件表达式的结果可以通过result()函数获得。</p>
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

If the `[Record]` button of the teach pendant is pressed, a `移动 (move)` statement in hidden pose type will be recorded as the current robot position. The hidden pose value can be checked or edited by placing the cursor on the `移动 (move)` statement and pressing the `[Property]` button. 

When the `[Command]` button is pressed and the `[Motion]` group is opened, select the move menu. As a result, a pose-type `移动 (move)` statement is recorded.
[__SOURCE](5-moving-robot/5-mkucs.md)
# 5.5 `mkucs` - 制作用户坐标系

### 描述

一个用来创建具有三个姿态或一个姿态的用户坐标系的命令。

- 当您用三个姿态创建时，它会根据指定的步骤顺序创建原点姿态、轴姿态和平面姿态。
- 如果未指定步骤顺序，它将使用原点姿态、X轴姿态和XY平面姿态创建。
- 当您用一个姿态创建时，它将使用原点姿态，并且位置/方向基于姿态值。
- 如果无法计算，作业执行将因错误中断。

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
        <li>-1: 创建用户坐标系统失败。</li>
        </ul>
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">user coord. system number</td>
      <td style="text-align:left">
        要创建的用户坐标系统的编号
      </td>
      <td style="text-align:left">[1~20]</td>
    </tr>
    <tr>
      <td style="text-align:left">step order</td>
      <td style="text-align:left">
        三个姿态的顺序，如果未指定，将为"OXY" <br>
        (示例) <br>
        "OXY" : 原点姿态，X轴姿态，XY平面姿态 <br>
        "OYZ" : 原点姿态，Y轴姿态，YZ平面姿态 <br>
      </td>
      <td style="text-align:left">字符串变量</td>
    </tr>
    <tr>
      <td style="text-align:left">origin pose</td>
      <td style="text-align:left">
        原点处的姿态
      </td>
      <td style="text-align:left">姿态变量</td>
    </tr>
    <tr>
      <td style="text-align:left">axis pose</td>
      <td style="text-align:left">
        位于X、Y、Z轴上的姿态
      </td>
      <td style="text-align:left">姿态变量</td>
    </tr>
    <tr>
      <td style="text-align:left">plane pose</td>
      <td style="text-align:left">
        位于XY、YZ、ZX平面上的姿态
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

- E14613 : 当实际参数与形式参数不匹配时发生。检查实际参数。
- E14614 : 当用户坐标号不是一个数字时发生。请重新指定用户坐标号。
- E14615 : 当用户坐标号不是1到20之间的数字时发生。请更改用户坐标号。
- E1011 : 当教授的姿态之间的距离过近时发生。当每个点之间的距离小于1mm时发生。请更正姿态之间的距离值。
- E1012 : 当三个调用的姿态在一条直线上时发生。

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

![](../_assets/mkucs.png)
[__SOURCE](5-moving-robot/6-selucrd.md)
# 5.6 `selucrd` - 选择用户坐标系统

`selucrd` 语句是用于更改在条件设置中指定的用户坐标系统编号的过程。

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
        <li>0: 取消指定用户坐标系统</li>
        <li>1~20: 指定一个用户坐标系统</li>
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

请参见下面的链接以获取 CONTPATH 的描述。
[操作手册：8.15 R360 手动设置 CONTPATH](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/8-r-code/15-r360?cont_model=${cont_model})

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

- 如果未明确执行 `contpath` 语句，则默认应用 `contpath 1`。即使明确指定，在周期开始时也会初始化为 `contpath 1`。

- 可以通过标题栏上的 `CP0` / `CP1` / `CP2` 标志检查更改的状态。

{% endhint %}
[__SOURCE](5-moving-robot/8-coldet.md)
# 5.8 `coldet`

机器人语言 `coldet` 用于在功能被激活时设置每个轴的碰撞检测级别。

用户应该在 TP 菜单中设置功能的开/关和碰撞级别。 `[F2: 系统] - 3: robot parameter - 14: impact detection - 2: set the collision detection (of each axis) ([F2: System] - 3: robot parameter - 14: impact detection - 2: set the collision detection (of each axis))`

菜单可以在设置为检测碰撞的机器人中显示。

如果功能被激活，默认检测级别为 1。

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
* 步骤 1 和步骤 2 的检测级别值为 1。
* 步骤 3 的检测级别值为 2，步骤 4 和步骤 5 的级别值为 3。
* 在步骤 6 和步骤 7 中，碰撞检测功能被关闭。
---
[__SOURCE](5-moving-robot/9-colsense.md)
# 5.9 `colsense` 

机器人语言 `colsense` 用于在功能激活时设置检测灵敏度。

用户应在 TP 菜单中设置功能激活开/关和检测灵敏度。`[F2: 系统] - 3: robot parameter - 14: impact detection - 1: Model-based collision detection ([F2: System] - 3: robot parameter - 14: impact detection - 1: Model-based collision detection)`。

---

### 描述
* 可以设置一般的碰撞检测灵敏度
* 每个轴的碰撞检测灵敏度可以设置

### 语法 
```python
colsense general,sensitivity=<general sensitivity>  
colsense axis,id=<joint number>,criteria=<each axis sensitivity> 
```

### 参数 
* 一般阈值可以设置从 0 到 200，值越大灵敏度越高。(0:0ff,1~200)
* 参数 "id" 设置为关节编号。(1~6)  
* 轴阈值可以设置从 0 到 100，值越低灵敏度越高。(0:0ff,1~100)"

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
* 第 1 步和第 2 步中的检测灵敏度值基于菜单设置 `[F2: 系统] - 3: robot parameter - 14: impact detection - 1: Model-based collision detection ([F2: System] - 3: robot parameter - 14: impact detection - 1: Model-based collision detection)`。
* 第 3 步中的一般灵敏度为 150，第 4 步和第 5 步时值更改为 200。
* 第 1 关节和第 2 关节的碰撞感应被禁用，其他关节的碰撞根据一般灵敏度 200 被检测。

--- 
{% hint style="info" %}

每个轴的最终灵敏度值与各轴的灵敏度值成正比，与一般灵敏度值成反比。
{% endhint %}
[__SOURCE](5-moving-robot/10-softxyz.md)
# 5.10 `softxyz`

`softxyz` 函数是一种无传感器的力控制特性，允许机器人在用户定义的条件下对外部力量在笛卡尔空间中进行灵活移动。

为了确保正常操作，`工具数据和额外的负载信息必须正确配置`。

{% hint style="warning" %}

由于 `softxyz` 函数是 `无传感器` 的并且不使用力传感器，  
实现完全平滑和自然运动存在 `固有的限制`。

然而，通过为应用环境适当地调整 `softxyz_lim` 值，  
您可以在功能限制内实现可能的最平滑运动。

因为 `softxyz_lim (pos / xnr / vel / thr)` 直接决定机器人对外部力量的反应，  
需要根据环境、装配过程和工具刚度进行 `微调`。

{% endhint %}

### 描述
* 一种允许机器人在不使用力传感器的情况下，通过外部力量在笛卡尔坐标系中被位移的功能。

---

### 语法
```python
softxyz on, crd=<reference_coordinate>
softxyz set, dpr=<stiffness>
softxyz off
```

### 参数
- ` (on)` : 启动 softxyz 功能  
- ` (off)` : 停止 softxyz 功能  
- `set` : 修改 softxyz 设置  

- `crd` : 外部力位移的参考坐标系统  
  - 可用选项: `基座 (base)`, `机器人 (robot)`, `工具 (tool)`, `user_x`

- `dpr` : 刚度值  
  - 范围: `0.0 ~ 2.0`  
  - 较高的值 = `更刚性`，在外部力量下位移更小  
  - 默认: `1.0`

```python
softxyz on,  crd="base"     # 基于基座坐标系统
softxyz on,  crd="robot"    # 基于机器人坐标系统
softxyz on,  crd="tool"     # 基于工具坐标系统
softxyz on,  crd="user_1"   # 用户定义的坐标系统 #1

softxyz set, dpr=1.0        # 设置刚度 (0.0~2.0, 较高 = 更刚性)
softxyz off                 # 禁用 softxyz 功能
```


### 示例 
> 示例 1) 在允许 X、Y 和 Ry 方向位移的情况下沿 Z 方向装配
> * 坐标 : 机器人坐标 (crd="robot") <br>
> * 位置 (xnr) 限制 : X 和 Y 方向的范围 [-50,+50] (mm)，Ry 方向的范围 [-3,+3] (deg) <br>
> * 速度 (vel) 限制 : X 和 Y 方向的最大速度 5(mm/sec)，Ry 的最大速度 3(deg/sec)  <br>
> * 扭矩 (thr) 限制 : X 方向的阈值 3N，Y 方向的阈值 3N 和 Ry 方向的 1Nm 

```python
S1   move P,spd=100mm/sec,accu=0,tool=0
     delay 2.0   # 启用 softxyz 之前所需的时间
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
(mm) , -Y 方向的范围 [-200,0] (mm) <br>
> * 速度 (vel) 限制 : Y 方向的最大速度 150(mm/sec)<br>


```python
S1   move P,spd=100mm/sec,accu=0,tool=0
     delay 2.0   # 启用 softxyz 之前所需的时间
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
>   (`pos`, `xnr`, `vel`, `thr`) 以设置最大位移、速度，  
>   以及笛卡尔阈值。
>
> - 为了提高对外部力量的灵敏度，建议您  
>   `在执行 `softxyz on` 之前，使用 `delay` 指令输入保持机器人静止 1-2 秒 ( command)`  
>
> - 如果在 softxyz 操作过程中出现振动，建议进行以下调整：
>   1) *增加 `thr` 值*  
>   2) *增加 `dpr` 值*  
>   3) *降低 `vel` 值*
[__SOURCE](5-moving-robot/11-softxyz_lim.md)
# 5.11 `softxyz_lim`

在使用指令 `softxyz on` 之前，用户应设置 `softxyz_lim` 参数，例如位置限制(`pos`)、工作空间限制(`xnr`)、速度限制(`vel`)和力阈值限制(`thr`). <br>

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
* softxyz_lim pos : 基于笛卡尔空间的位置限制 [mm] <br>
* softxyz_lim vel : 基于笛卡尔空间的最大平移和旋转速度限制 [mm/sec] 或 [deg/sec] <br>
* softxyz_lim xnr : 基于笛卡尔空间的工作空间（位置/旋转）限制 [mm] 或 [deg] <br>
* softxyz_lim thr : 基于笛卡尔空间的力阈值限制 [N] 或 [Nm] <br>

### 示例
> * 设置位置限制：+X 方向为 200[mm]，-Y 方向为 100[mm]，+Z 方向为 300[mm]
```python
softxyz_lim pos, _x=200, y_=100, _z=300
```
> * 设置速度限制：Z 方向的最大速度为 40[mm/sec] 
```python
softxyz_lim vel, z=40
```
> * 设置工作空间限制：X 方向的最大位置为 [-200,200][mm]
```python
softxyz_lim xnr, x=200
```
> * 设置扭矩限制：扭矩阈值设置为 10[N]
```python
softxyz_lim thr, y=10
```
[__SOURCE](5-moving-robot/12-softjoint.md)
# 5.12 `softjoint`

`softjoint` 指令是无传感器的力控制，允许机器人在关节空间中相对于用户设定的环境中的外部力量以顺应方式移动。 <br>

用户应检查机器人工具和附加轴信息的有效性，以提高功能的准确性。 <br>

--- 

### 描述 
* 无需使用传感器，在关节空间中相对于用户设定的环境中的外部力量以顺应方式移动。 

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

* 在使用 `softjoint on` 之前，用户应设置 softjoint_lim 参数，例如关节编号(` (j)`)、柔软度(`sft`)、关节角度限制(`ang`)和扭矩阈值(`thr`)。

* 为了提升无传感器力控制性能，用户应在 `softjoint on` 之前将 `时间延迟 (delay)` 命令设置为 `delay 1.0`。  

{% endhint %}
[__SOURCE](5-moving-robot/13-softjoint_lim.md)
# 5.13 `softjoint_lim`

在使用指令 `softjoint on` 之前，用户应设置 `softjoint_lim` 参数，例如关节编号(` (j)`)、柔性(`sft`)、关节角度限制(`ang`)和扭矩阈值(`thr`)。 <br>

---

### 语法 
```python
softjoint_lim, j=<关节编号>, sft=<柔性>, ang=<关节角度限制>, thr=<扭矩阈值> 
```

### 参数
* j : 关节编号 [1~6]
* sft : 较大的值更容易移动 [0:off,0~100]
* ang : 关节角度限制 [度]
* thr : 扭矩阈值 [Nm]


### 示例 
> 示例1) 设置关节编号 3(J3) 的参数 
> * 在 J3 激活，柔性(50)，关节角度限制 [-30~30] (度) 和扭矩阈值 10(Nm)   
```python
softjoint_lim, j=3, sft=50, ang=30, thr=10
```

> 示例2) 设置关节编号 2 和 3(J2, J3) 的参数
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

* 使用 `softjoint` 功能时，应设置 ` (j)` 和 `sft` 上的参数，若不设置 `ang` 参数，机器人将在定义的软限制内移动。扭矩阈值 `thr` 的默认参数值为 0 [Nm]。 

{% endhint %}
[__SOURCE](5-moving-robot/14-external_control.md)
# 5.14 外部控制

### 描述  
* 机器人的运动位置命令生成由外部设备执行，这个生成的外部命令通过以太网或串行通信作为字符串数据传输到 ${cont_model} 控制器。 ${cont_model} 控制器接收该命令并控制机器人。

### 语法 
```python
     global onl_trj
     var msg # 位姿或位姿类型字符串

     onl_trj=online.Traject()
     onl_trj.time_from_start=-1.0
     onl_trj.look_ahead_time=1.0
     onl_trj.interval=0.1
     onl_trj.init
     onl_trj.buf_in msg
 
```

### 参数 
* `time_from_start` : 从起始位置到现在的经过时间 (-1: 禁用)  
* `look_head_time` : 机器人移动的时间延迟 (单位 : [s])  
* `interval` : 生成命令之间的时间间隔 (单位 : [s])  
* `init` : 在线轨迹初始化，清除命令缓冲区  
* `buf_in`  : 将位姿或位姿类型字符串添加到命令缓冲区


### 示例
> 机器人通过接收外部生成的命令来移动，采用enet通信。

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
       onl_trj.init # 缓冲区清除 (快速停止)
     else
       onl_trj.buf_in msg 
     endif    
     goto 10
     end 
```


--- 
{% hint style="info" %}

* 当前接收到的位姿或位姿类型字符串只能是轴-角坐标格式。
* 位姿字符串只能是数组格式的轴-角坐标 (例如 [0.000,90.000,0.000,0.000,-90.000,0.000])。    

{% endhint %}
[__SOURCE](5-moving-robot/15-convcrd.md)
# 5.15 `convcrd`

### Description 
* `convcrd` 命令是一个功能指令，用于转换姿态变量的坐标系统。

### Syntax 
>* poseA: 要转换的姿态变量。
>* poseB: 转换后的姿态变量。

```python
poseB = poseA.convcrd("base")      # 基准坐标
poseB = poseA.convcrd("robot")     # 机器人坐标
poseB = poseA.convcrd("tool")      # 工具坐标
poseB = poseA.convcrd("u1")        # 用户坐标 1
```

### Example 
```python
     var pose_A, pose_B
     
     # 关节坐标
     pose_A=Pose(0.00,60.00,0.00,0.00,-30.00,0.00)
     # 基准坐标
     pose_B=pose_A.convcrd("base")
```
[__SOURCE](5-moving-robot/16-pose_trans.md)
# 5.16 `pose_trans`

### Description 
* `pose_trans` 命令是一个函数指令，用于将两个姿态变量相乘以获得结果姿态值。

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


### Description

* `pose_inv` 指令是一个将对应于姿态变量的逆矩阵的姿态变量转换为函数。  


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

### Description
* `axisctrl` 命令指定在执行 `移动 (move)` 命令以移动每个轴时，是否应让额外的轴移动到其目标位置。
* 有关 `axisctrl` 语句的详细描述，请参阅下面的链接。  
[${cont_model} Controller Function Manual - Multitasking](https://hrbook-hrc.web.app/#/view/doc-multi-task/zh/README?cont_model=${cont_model})

### Syntax
```python
axisctrl <on/off>,a=<additional axis number>
axisctrl <on/off>,a=[additional axis number, additional axis number, ...]  # 允许多重指定（最多 4 个）
```
[__SOURCE](5-moving-robot/19-smov.md)
# 5.19 `smov`

### 描述
`smov` 语句是用于定位器同步的程序。  
有关 `smov` 语句的详细描述，请参见以下链接。  
[${cont_model} 控制器功能手册 - 定位器同步](https://hrbook-hrc.web.app/#/view/doc-positioner-sync/zh/README?cont_model=${cont_model})

<br><br>

### 语法
```python
smov S<station number>,<interpolation mode>,tg=<target position>,spd=<speed>,accu=<Accuracy>,tool=<tool number>
smov S<station number>,<interpolation mode>,tg=<target position>,spd=<speed>,accu=<Accuracy>,tool=<tool number> until <input signal>
```
[__SOURCE](5-moving-robot/20-shift.md)
# 5.20 `shift`

### 描述
`shift`语句在保持工具方向（工具角度）的情况下，转换XYZ坐标系中已教导的点。

### 语法
```python
shift crd=<参考坐标>,x=<X位移值>,y=<Y位移值>,z=<Z位移值>
```

### 参数
* crd : 参考坐标系
["base": 基底, "robot": 机器人, "tool": 工具, "joint": 关节, "u": 用户]
* x, y, z : X, Y, Z位移值 [0-3000, mm]

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

`shift_lim` 语句是一个通过设置机器人可允许的最大移动量来提高使用移动功能时安全性的函数。  
如果输入的移动值超过配置的限制，将产生错误。

### 语法
```python
shift_lim x=<X 移动限制>, y=<Y 移动限制>, z=<Z 移动限制>
```

### 参数
* x, y, z: X, Y, Z 移动限制值[0~3000,mm]<br><br>

### 错误指南
* E1196: 移动量超过配置的移动限制。减少移动量或重新调整移动限制值。

### 示例
```python
     var po1 = Pose(0.691, 99.293, 24.758, -6.528, -48.574, 15.774, 0.000)
S1   move P, tg=po1, spd=10%, accu=0, tool=0
     shift_lim x=120, x=200, z=100
     shift crd="base", x=-150, y=70, z=10  # 超过移动限制的错误发生
S2   move P, tg=po1, spd=10%, accu=0, tool=0
     end
```
[__SOURCE](5-moving-robot/22-s-curve.md)
# 5.22 scurve

S-曲线是一种运动轨迹规划方法，在机器人运动的加速和减速阶段，将速度变化视为平滑曲线。

- **默认方法**：在加速的开始和结束时，速度变化突然，这可能会导致机械冲击（冲击力）。
- **S-曲线方法**：使速度变化平滑，从而最小化设备振动，延长硬件寿命，并确保在高速操作期间路径的稳定准确性。

### 语法
```python
"scurve on, cnd=<condition number>
"scurve off
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">项目</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">其他</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">on/off</td>
      <td style="text-align:left">
        S-曲线功能是否启用
      </td>
      <td style="text-align:left">on(启用), off(禁用)</td>
    </tr>
    <tr>
      <td style="text-align:left">
        cnd (条件编号)
      </td>
      <td style="text-align:left">
        指定要使用的S-曲线条件的编号
      </td>
      <td style="text-align:left">1~16</td>
    </tr>
  </tbody>
</table>


### 使用示例
```python
     scurve on,cnd=1   # 应用S-曲线条件#1
S1   move P,tg=po1,spd=10%,accu=0,tool=0
     scurve off       # 禁用S-曲线
S2   move P,tg=po1,spd=10%,accu=0,tool=0
     end
```

{% hint style="info" %}
有关详细信息，请参见${cont_model}控制器操作手册的"[7.5.23 S-曲线条件](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/7-system/5-application-parameter/23-scurve-condition/README?cont_model=${cont_model})"部分。
{% endhint %}
[__SOURCE](6-external-comm/README.md)
# 6. 与外部设备通信
[__SOURCE](6-external-comm/1-fb-io/README.md)
# 6.1 `FB` 对象：数字输入/输出

数字输入/输出 \(I/O\) 可以通过 10 个 `FB` 对象执行，这些对象可以从 HRScript 访问。 `FB` 指的是现场总线块，每个 `FB` 对象被设置为映射到安装在机器人控制器中的 I/O 硬件，并包含输入和输出变量作为元素。
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
    <td>有符号 1字节 整数</td>
    <td>-128 ~ +127</td>
  </tr>
  <tr>
    <td>dow[0~118]</td>
    <td>有符号 2字节 整数</td>
    <td>-32768 ~ +32767</td>
  </tr>
  <tr>
    <td>dol[0~116]</td>
    <td>有符号 4字节 整数</td>
    <td>-2147483648 ~ +2147483647</td>
  </tr>
  <tr>
    <td>dof[0~116]</td>
    <td>有符号 4字节 实数</td>
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
    <td>有符号 1字节 整数</td>
    <td>-128 ~ +127</td>
  </tr>
  <tr>
    <td>diw[0~118]</td>
    <td>有符号 2字节 整数</td>
    <td>-32768 ~ +32767</td>
  </tr>
  <tr>
    <td>dil[0~116]</td>
    <td>有符号 4字节 整数</td>
    <td>-2147483648 ~ +2147483647</td>
  </tr>
  <tr>
    <td>dif[0~116]</td>
    <td>有符号 4字节 实数</td>
    <td>3.4E+/-38 (7 位有效数字)</td>
  </tr>
</tbody>
</table>

<br><br>

In `do`, `dob`, `dow`, `dol`, and `dof`, the suffixes ` (b)`, ` (w)`, ` (l)`, and ` (f)` mean `byte`, `word`, `long`, and ` (float)`, respectively, and all are signed values. These are not separate memory spaces and represent the same 960-byte space just with different data types. For example, `do[1~16]`, `dob[1~2]`, and `dow[1]` are all the same output signals.

![](../../_assets/image_2.png)

If a value is assigned to an output variable that starts with `do`, I/O signal output will be performed. The I/O signal currently being inputted can be acquired by reading the input variable value that starts with `di`. The do variable can be read and written, but the di variable can only be read.

The `FB` object name can be omitted as follows.

| **对象名称** | **do 表示法** | fb.do 表示法 |
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

请参阅以下用法示例。

```python
do2=1		# 打开 fb0 的编号 0 的位输出值
fb2.dob3=0b00001111  	# 将 fb2 的第 3 个字节输出值指定为二进制位字符串
fb[4].dob1=0x0F  	# 打开 fb4 的第 1 个字节输出值的低 4 位，并关闭高 4 位
var work_no=fb9.dib3    # 将 fb9 的第 3 个字节输入值分配给 work_no 变量
if fb5.di43 then *err  	# 当 fb5.di42 被打开时分支到 *err 标签
for idx=21 to 29
  fb3.do[idx]=1  	# 打开 fb3 的所有输出信号 do21 ~ do29 
next
fb2.do3=fb2.do7=fb2.do11=1   # 同时打开 fb2 的第 3、第 7 和第 11 个输出信号
```
[__SOURCE](6-external-comm/1-fb-io/3-fn-io.md)
# 6.1.3 `fn` 对象

您可以通过指定 `fb` 对象的特定区域来定义 `fn` 对象。
如果 ${cont_model} 控制器是现场总线主设备，并且有多个现场总线从设备，您可以将每个从设备的区域设置到每个 `fn` 对象，以便直观地处理这些从设备。

![](../../_assets/io/io_fn.png)

请查看以下链接获取有关如何设置 `fn` 区域的说明。

[操作手册：fn 块分配](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/7-system/3-control-parameter/2-io-signal-setting/12-fn-block?cont_model=${cont_model})

&nbsp;

`fn` 的语法与 `fb` 的格式相同。
`fn` 索引为 0 到 63，位索引为 0 到 959，和 `fb` 一样。
也就是说，最大可配置索引为 fn0.do0 到 fn63.do959。

当访问未配置的不存在的 `fn` 对象或访问超出 `fn` 设置范围的 do/di 时，会发生错误。

请参阅下面的使用案例；

```python
fn2.dob3=0b00001111  	# 将 fn2 的输出字节 3 设置为二进制位
fn[4].dob1=0x0F  	# 打开 fn4 的输出字节 1 的低 4 位，并关闭高 4 位。
var work_no=fn63.dib3    # 将 fn63 的输入字节 3 赋值给 work_no 变量
if fn5.di43 then *err  	# 当 fn5.di42 打开时，跳转到 *err 标签。
for idx=21 to 29
  fn3.do[idx]=1  	# 打开 fn3 的所有输出信号 do21 ~ do29。
next
fn2.do3=fn2.do7=fn2.do11=1   # 一次打开 fn2 的输出信号 3、7 和 11。
```
[__SOURCE](6-external-comm/1-fb-io/4-pulse.md)
# 6.1.4 `pulse`

`pulse` 语句是脉冲类型信号输出的过程。

### 描述

在 tlag 时间经过后，以 cnt 次作为高电平（On）持续 ton 时间，低电平（Off）持续 toff 时间输出。

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
      <td style="text-align:left">Signal</td>
      <td style="text-align:left">
        以脉冲形式输出的信号名称<br>
        (仅支持 fb.do 信号。)
      </td>
      <td style="text-align:left">输出信号</td>
    </tr>
    <tr>
      <td style="text-align:left">Lag time</td>
      <td style="text-align:left">
        执行过程后直到脉冲信号开始前的等待时间<br>
        (0.0 ~ 100.0[秒])
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">On time</td>
      <td style="text-align:left">
        输出信号为高电平（On）状态的时间<br>
        (0.0 ~ 100.0[秒])
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">Off time</td>
      <td style="text-align:left">
        输出信号为低电平（Off）状态的时间<br>
        (0.0 ~ 100.0[秒])
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">Number of outputs</td>
      <td style="text-align:left">
        重复脉冲周期的次数
        (0 ~ 1000)
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
# 6.2 `http_cli` 模块：HTTP 客户端

使用 ${cont_model} 控制器的通用以太网端口，可以访问远程 Web 服务并使用 HTTP 服务。  
要使用此功能，请导入 `http_cli` 模块并创建一个 `HttpCli` 对象，如下所示。

```python
import http_cli
var cli = http_cli.HttpCli()
```

创建 `HttpCli` 对象后，可以通过调用 `get`、`put`、`post` 和 `删除 (delete)` 成员过程来发起服务请求。<br>  
`HttpCli` 对象提供一个名为 `body` 的属性。<br>  
- 当发起 `GET` 请求并成功接收到响应时，远程服务器返回的数据存储在 `body` 属性中。<br> `body` 值的类型可以是字符串、数字、数组或对象。  
- 在发起 `PUT` 请求时，待传输的数据必须提前分配给 `body` 属性。  
- 在发起 `POST` 请求时，待传输的数据也必须提前分配给 `body` 属性，并且远程服务器在响应中返回的数据存储在 `body` 属性中。  
- `DELETE` 服务不使用 `body` 属性。  
提供的 HTTP 客户端通信以同步模式操作。
[__SOURCE](6-external-comm/2-http_cli/1-http_cli-creator.md)
# 6.2.1 构造函数 

### 描述

创建一个 `HttpCli` 对象并返回对它的引用。

### 语法


HttpCli\(\)

### 返回值

对新创建对象的引用。

### 使用示例

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
      <td style="text-align:left">Any</td>
      <td style="text-align:left">
        <p>要传输的数据必须在PUT和POST请求之前分配。<br><br>如果给`body`分配了一个对象以外的值，执行时URL的最后路径段将被视为键。<br><br>GET和POST请求的响应数据存储在`body`中。<br><br>在HRScript中，不支持直接访问`body`的成员变量。要修改或使用数据，必须先将其分配给另一个变量。</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">query</td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">
        用于需要查询参数的GET服务。<br>与GET请求一起发送的数据必须预先分配。
      </td>
    </tr>
    <tr>
      <td style="text-align:left">status</td>
      <td style="text-align:left">int</td>
      <td style="text-align:left">
        <p>
            返回HTTP响应代码和错误代码。(请参阅[6.2.4节, HTTP通信代码](./4-http_cli-code.md))
          <br/>
        </p>
      </td>
    </tr>
  </tbody>
</table>

<br/>

`body`和`query`都使用对象数据类型。

对象类型支持`{ key: value }`格式。

```python
cli.body = { name: "WORK #32", color: "green", state: "OK" }
cli.query = { axis: 3 }
```
[__SOURCE](6-external-comm/2-http_cli/3-http_cli-member-proc/README.md)
# 6.2.3 成员过程
[__SOURCE](6-external-comm/2-http_cli/3-http_cli-member-proc/1-http_cli-get.md)
# `get`

### Description

请求HTTP GET服务。

服务器检索与请求的URL相关的信息并在响应中返回。

响应数据存储在`body`属性中。

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
        请求的URL。
      </td>
      <td></td>
    </tr>
    <tr>
      <td>Timeout</td>
      <td>
        （可选）超时时间。如果超时到期，则执行将继续进入下一条语句或备用地址。<br>如果没有指定，请求将无限期等待。<br>超时必须设置在5 ms到15 ms（包含）之间。否则，将发生播放超时错误。<br>如果值超出此范围，`-9 (InvalidTimeout)`将存储在`状态 (status)`中。
      </td>
      <td>毫秒</td>
    </tr>
    <tr>
      <td>timeout fallback address</td>
      <td>
        （可选）超时发生时分支的地址。<br>如果没有指定，执行将继续进入下一个地址。
      </td>
      <td>地址</td>
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
# `put`

### Description

请求一个 HTTP PUT 服务。

更新指定的资源。

要传输的数据必须事先分配给 `body` 属性。

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
        请求的 URL。
      </td>
      <td></td>
    </tr>
    <tr>
      <td>Timeout</td>
      <td>
        （可选）超时时间。 如果超时到期，执行将继续到下一个语句或备用地址。<br>如果未指定，请求将无限期等待。<br>超时时间必须设定在 5 ms 到 15 ms 之间（包括）。 否则，将发生播放超时错误。<br>如果值超出此范围，则 `-9 (InvalidTimeout)` 被存储在 `状态 (status)` 中。
      </td>
      <td>毫秒</td>
    </tr>
    <tr>
      <td>timeout fallback address</td>
      <td>
        （可选）在发生超时时跳转的地址。<br>如果未指定，执行将继续到下一个地址。
      </td>
      <td>地址</td>
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
# `post`

### Description

请求 HTTP POST 服务。

创建指定的资源。

要传输的数据必须提前分配给 `body` 属性。

远程服务器返回的响应数据存储在 `body` 属性中。

### Syntax

&lt;HttpCli object&gt;.post &lt;URL string, timeout, timeout fallback address&gt;

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">项目</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>URL string</td>
      <td>
      请求 URL。
      </td>
      <td></td>
    </tr>
    <tr>
      <td>Timeout</td>
      <td>
        （可选）超时时间。如果超时到期，执行将继续到下一个语句或后备地址。<br>如果未指定，请求将无限期等待。<br>超时必须设置在 5 ms 和 15 ms（包括）之间。否则，将发生播放超时错误。<br>如果值超出此范围，`-9 (InvalidTimeout)` 将存储在 `状态 (status)` 中。
      </td>
      <td>毫秒</td>
    </tr>
    <tr>
      <td>timeout fallback address</td>
      <td>
        （可选）发生超时时的分支地址。<br>如果未指定，执行将继续到下一个地址。
      </td>
      <td>地址</td>
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
# `删除 (delete)`

### 描述

请求 HTTP DELETE 服务。

删除指定的资源。

`body` 属性在此请求中不使用。

### 语法

&lt;HttpCli object&gt;.delete &lt;URL string, timeout, timeout fallback address&gt;

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">项目</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>URL string</td>
      <td>
        请求的 URL。
      </td>
      <td></td>
    </tr>
    <tr>
      <td>Timeout</td>
      <td>
        (可选) 超时持续时间。如果超时到期，执行将继续到下一条语句或转到后备地址。<br>如果未指定，请求将无限期等待。<br>超时必须设置在 5 ms 到 15 ms 之间（包括）。否则，将发生播放超时错误。<br>如果值超出此范围，`-9 (InvalidTimeout)` 将存储在 `状态 (status)` 中。
      </td>
      <td>毫秒</td>
    </tr>
    <tr>
      <td>Timeout fallback address</td>
      <td>
        (可选) 超时发生时分支到的地址。<br>如果未指定，执行将继续到下一个地址。
      </td>
      <td>地址</td>
    </tr>
  </tbody>
</table>

### 使用示例

```python
var domain="http://192.168.1.200:8888"
cli.delete domain+"/items"
```
[__SOURCE](6-external-comm/2-http_cli/4-http_cli-code.md)
# 6.2.4 HTTP 通信代码

* 主要 HTTP 响应代码 
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
      <td rowspan="2">信息性</td>
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
      好的
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
      非权威性信息
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
      暂时未移动
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
        400
      </td>
      <td>
      请求错误
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
      禁止 
      </td>
    </tr>
    <tr>
      <td>
        404
      </td>
      <td>
      找不到 
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
      已消失  
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
      请求-URI 过长
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
      <td>
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
      不支持 HTTP 版本
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
      在处理您的请求时发生了模糊的异常。
      </td>
    </tr>
    <tr>
      <td> ConnectionErr</td>
      <td>
        -2
      </td>
      <td>
      如果发生网络问题（例如 DNS 失败、拒绝连接等）
      </td>
    </tr>
    <tr>
    <td> HTTPError
      <td>
        -3
      </td>
      <td>
      如果 HTTP 请求返回不成功的状态代码，将会发生。
      </td>
    </tr>
    <tr>
    <td>URLRequired</td>
      <td>
        -4
      </td>
      <td>
      进行请求需要有效的 URL。
      </td>
    </tr>
    <tr>
    <td>TooManyRedirects</td>
      <td>-5</td>
      <td>
      如果请求超过配置的最大重定向次数，将引发 TooManyRedirects 异常。
      </td>
    </tr>
    <tr>
    <td>Timeout</td>
      <td>
        -6
      </td>
      <td>
      如果请求超时，将引发 Timeout 异常。
      </td>
    </tr>
    <td>SessionInvalid</td>
      <td>
        -7
      </td>
      <td>
        此错误表示会话无效，因为在处理会话请求时发生了运行时错误。 会话无效。 当在会话请求期间发生运行时错误时，将出现此错误。
      </td>
    </tr>
    <td>UnhandledException</td>
      <td>
        -8
      </td>
      <td>
        在 HTTP 请求或响应处理过程中（例如，会话创建、请求执行或响应解析）发生了意外错误，并且与任何明确处理的异常不匹配。因此，请求结果报告为 UnhandledException。
      </td>
    </tr>
    <td>InvalidTimeout</td>
      <td>
        -9
      </td>
      <td>
        当超时值超过 5 ms 到 15 ms 的范围时。
      </td>
    </tr>
  </tbody>
</table>
[__SOURCE](6-external-comm/2-http_cli/5-http_cli-example.md)
# 6.2.5 HTTP客户端使用示例

```python
     import http_cli
     var cli=http_cli.HttpCli()
     var url, body, query, status_code
     var domain="http://192.168.1.200:8888"

     # 获取
     cli.get domain+"/device/direction"
     body = cli.body

     #检查通信状态
     if cli.status>=400 or cli.status<0
        goto 99 		#http通信错误
     endif

     # 放置
     url = domain+"/device/direction"
     body.ry=90
     cli.body=body
     cli.put(url, 3000, *Timeout)

     # 发送
     cli.body={ name: "WORK #32", color: "green", state: "OK" }
     cli.post domain+"/display/update", 5000, *Timeout

     # 删除
     cli.delete(domain+"/items")

     end
     
  99 print "错误状态"
     
     *Timeout
     print "超时"
```
[__SOURCE](6-external-comm/3-tp-console-bar/README.md)
# 6.3 使用教导 pendant 控制台栏的输入/输出
[__SOURCE](6-external-comm/3-tp-console-bar/1-print.md)
# 6.3.1 `print`

### Description

`print` 语句将字符串打印到教导挂件的引导条上。除了字符串常量外，任何类型的表达式（包括常量和变量）结果都将转换为字符串并打印出来。如果指定多个表达式，则每个表达式之间用一个空格字符分隔打印。

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
        <p>要打印的表达式。<br>
        支持所有类型的布尔值、数字、字符串、数组、对象。
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
# 6.3.2 `input`

### Description

使用 `input` 语句将字符串作为 Teach Pendant 的按键输入，并将其存储在一个变量中。如果在超时之前没有输入，请继续执行以下语句或跳转到超时地址。

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
      <td style="text-align:left">超时后跳转的地址</td>
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
# 6.4 Modbus 模块 : Modbus 主站

Modbus 主站操作可以在 HRScript 中执行。有关 Modbus 通信功能的详细信息，请参阅单独的手册。 [${cont_model} 控制器功能手册 - Modbus](https://hrbook-hrc.web.app/#/view/doc-modbus/zh/README?cont_model=${cont_model})  
[__SOURCE](6-external-comm/5-sci/README.md)
# 6.5 Sci module : Serial communication

串行通信可以通过 ${cont_model} 控制器的 COM 端口进行。

要使用此功能，您必须创建一个 `Sci` 对象作为全局变量，如下所示。

另外，在使用之前，请务必检查 `[F2: 系统] - 2. Control Parameters - 3. Serial Port ([F2: System] - 2. Control Parameters - 3. Serial Port)` 中的设置规格。

```python
global sci2
sci2=com.Sci(2)
```

创建 `Sci` 对象后，只需调用 `send`、`recv`、`open` 和 `关闭 (close)` 成员过程。

调用 `send` 时，必须事先输入要发送的字符串。

调用 `recv` 时，成功接收后会分配给指定的字符串变量。

调用 open 时，端口会被打开。

调用 open 时，端口将关闭。
[__SOURCE](6-external-comm/5-sci/1-sci-creator.md)
# 6.5.1 构造函数

### 描述

为 `Sci` 对象创建全局变量。

### 语法

com.Sci(port number)

### 返回值

创建的对象的引用

### 示例

```python
global sci2
sci2=com.Sci(2)
```
[__SOURCE](6-external-comm/5-sci/2-sci-member-proc/README.md)
# 6.5.2 成员过程
[__SOURCE](6-external-comm/5-sci/2-sci-member-proc/1-sci-send.md)
# `send`

### 描述

通过调用 `Sci` 的 `send` 发送字符串。

### 语法

&lt;Sci object&gt;.send "string" <br>
&lt;Sci object&gt;.send string variable


### 示例

```python
sci2.send "test"
or
var msg="test"
sci2.send msg
```
[__SOURCE](6-external-comm/5-sci/2-sci-member-proc/2-sci-recv.md)
# recv

### Description

调用 `Sci` 的 `recv` 以接收字符串。

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
        成功接收到的字符串将会存储在此字符串变量中。<br>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>timeout</td>
      <td>
        当在指定时间内未接收到数据时，将跳转到 goto 地址，如果没有 goto 地址，则会发生错误。<br>
        如果未指定，将无限期等待。
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>goto address</td>
      <td>
        当发生超时时跳转的地址。<br>
        如果未指定，将以错误停止。
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
# `open`

### Description

执行 `Sci` 的 `open()` 函数以打开串口。

通过控制器设置以预设内容打开串口，除非之前关闭了端口，否则无需单独打开该端口。(默认：打开)

### Syntax

&lt;Sci object&gt;.open()

### Return Value
- 0: 成功
- <0: 失败

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
# `关闭 (close)`

### Description

执行 `Sci` 的 `关闭 (close)` 以关闭串行端口。

### Syntax

&lt;Sci object&gt;.close()

### Return Value
- 0: 成功
- -1: 失败

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
# `clr_rbuf`

### 描述

初始化 `Sci` 的接收缓冲区。


### 语法

&lt;Sci object&gt;.clr_rbuf()

### 返回值
- 0: 接收缓冲区初始化成功
- -1: 失败

### 示例

```python
var ret
ret=sci2.clr_rbuf()
if ret<0
  print "接收缓冲区清除错误"
  stop
endif
```
[__SOURCE](6-external-comm/5-sci/3-sci-example.md)
# 6.5.3 串行通信示例

``` python
Hyundai Robot Job File; { version: 1.6, mech_type: "", total_axis: -1, aux_axis: -1 }
     
     # 使用构造函数创建 Sci 对象并将其分配给全局变量 
     global sci2
     sci2=com.Sci(2)   #port no. (com2)
     
     # 清除接收缓冲区
     var ret
     ret=sci2.clr_rbuf()

     # 发送
     sci2.send "test"

     # 接收 (选项: 当超过 3000ms 时，转到 *timeout)
     var msg
     sci2.recv msg,3000,*timeout
     print msg

     end

     *timeout
     print "error"
     stop

```
[__SOURCE](6-external-comm/6-rsi/README.md)
# 6.6 RSI模块 : 传感器接口

支持自 V70.02-00。

"RSI" 代表 "远程传感器接口"。

机器人的位置信息等实时通过控制器的以太网通信传输到支持 RSI 的设备。 <br>
(机器人控制器 -> 远程传感器设备) <br>

以太网通信支持 UDP、TCP客户端和 TCP服务器。 <br>
有关以太网通信设置的信息，请参阅单独的 "[${cont_model} 控制器操作手册 - TP630](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/7-system/3-control-parameter/9-network-setting/2-service/4-enet-comm-setting?cont_model=${cont_model})"。

要使用此功能，您必须创建一个 RSI 对象作为全局变量，如下所示。

```python
global rsi
rsi=com.RSI(_enet0)  # _enet0 使用以太网通信设置中的 "enet0" 对象 
```

创建 RSI 对象后，您可以调用成员程序，例如 on、off 和 put。

执行 'on' 后，数据传输开始。

执行 off 后，数据传输停止。

您可以通过调用 put 来更改传输的值或添加新的标签。 

<br>

### 传输数据
通过执行 HRScript 语句，可以向基本标签添加选项标签。 <br>
标签的结构如下。 <br>

##### 基本标签 <br>

- cur_po : 这些是机器人的当前位置和方向的当前值。 (x, y, z, rx, ry, rz) 
- tsp : 这是从上一次数据传输到当前数据传输的时间经过时间。 (us) <br>
- index : 这是一个在执行 rsi.on 后初始化为 0 的值，每次传输数据时增加 1。 <br>
您可以通过它检查丢失的通信。
- trigger : 这是在运行 rsi.on 后自动生成的，值为 0 的标签。 <br>
您可以通过执行 rsi.put("trigger", 1) 将值更改为 1，并配置逻辑以从传感器设备读取和处理该值。  
##### 选项标签 <br>
- cpo_cmd : 这些是机器人的位置和方向的命令值。 (x, y, z, rx, ry, rz)  <br>
当您执行 rsi.put("cmd_po") 时，"cmd_po" 标签将以与 "cur_po" 标签相同的格式添加。
- 用户标签 : 您可以添加用户标签并通过执行 rsi.put("tag name", value) 来更改这些标签的值。 <br>
<br>
<br>

#### 传输的数据如下，具体取决于文档格式。
您可以通过执行 rsi.format="json" 或 rsi.format="xml" 来指定文档格式为 "JSON" 或 "XML"。 (默认 = "JSON")
<br>

JSON格式
```python
{
	"cur_po" : {
		"x" : 2407.675176,
		"y" : -38.666578,
		"z" : 2006.844781,
		"rx" : -158.004863,
		"ry" : 83.273921,
		"rz" : -159.598022
	},
	"tsp" : 3812,
	"index" : 186,
	"trigger" : 0
}
```
<br>

XML格式
```python
<Rob Type="HYUNDAI" tsp="3938">
    <cur_po x="2407.6" y="-37.7" z="2006.8" rx="-157.9988" ry="83.2761" rz="-159.5930"/>
    <index>167</index>
    <trigger>0</trigger>
</Rob>
```
[__SOURCE](6-external-comm/6-rsi/1-rsi-creator.md)
# 6.6.1 构造函数

### 描述

为 `RSI` 对象创建一个全局变量。

### 语法

com.RSI(enet 对象) <br>

指定用于以太网通信设置的对象。例如，如果使用的对象名称是 "enet0"，则指定 _enet0；如果是 "enet1"，则指定 _enet1。  

### 返回值

创建对象的引用

### 示例

```python
global rsi
rsi=com.RSI(_enet0)  # _enet0 在以太网通信设置中使用 "enet0" 对象 
```
[__SOURCE](6-external-comm/6-rsi/2-rsi-member-proc/README.md)
# 6.6.2 成员过程
[__SOURCE](6-external-comm/6-rsi/2-rsi-member-proc/1-rsi-on.md)
# 开启

### 描述

开始向外部传感器设备传输数据。
- 将“index”标签的值初始化为0。
- 初始化以便“cmd_po”标签不包含在输出中。
- 清除所有用户标签。
- 添加值为0的“trigger”标签。

### 语法

&lt;RSI object&gt;.on <br>


### 示例

```python
rsi.on

```
[__SOURCE](6-external-comm/6-rsi/2-rsi-member-proc/2-rsi-off.md)
# off

### 描述

停止与外部传感器设备的数据传输。

### 语法

&lt;RSI object&gt;.off <br>


### 示例

```python
rsi.off

```
[__SOURCE](6-external-comm/6-rsi/2-rsi-member-proc/3-rsi-put.md)
# put

### Description

您可以通过执行 RSI put() 函数更改现有标签的值或添加选项标签。


### Syntax

&lt;RSI object&gt;.put("cmd_po") <br>
&lt;RSI object&gt;.put("trigger", 1) <br>

### Return Value
- 1: 更改现有标签的值
- 0: 添加选项标签
- -1: 当函数只有一个参数时，输入参数不是系统标签

### Example

```python
var ret
ret=rsi.put("cmd_po")  # 包含 "cmd_po" 标签到输出中。
ret=rsi.put("trigger", 1)  # 将触发器标签的值更改为 1
ret=rsi.put("MyValue1", 789)  # 添加 MyValue1 标签以设置整数值 789
ret=rsi.put("MyValue2", 1.2345)  # 添加 MyValue2 标签以设置浮点值 1.2345
ret=rsi.put("MyValue3", "hello")  # 添加 MyValue3 标签以指定字符串 "hello"
```
[__SOURCE](6-external-comm/6-rsi/3-rsi-example.md)
# 6.6.3 传感器接口示例

``` python
Hyundai Robot Job File; { version: 1.6, mech_type: "", total_axis: -1, aux_axis: -1 }
     
     # 使用构造函数创建RSI对象并将其分配给全局变量 
     global rsi
     rsi=com.RSI(_enet0)  # 与enet0配置对象通信
     rsi.format="json" # 字符串格式 "json" 或 "xml"
     rsi.period=5  # 数据传输周期(ms)
     var ret

     # 发送开始
     ret=rsi.on
     ret=rsi.put("cmd_po")  # 包含 "cmd_po" 标签

     move L,spd=100mm/s,accu=1,tool=1
     ret=rsi.put("trigger", 1)  # 更改触发标签值
     move L,spd=100mm/s,accu=1,tool=1
     move L,spd=100mm/s,accu=1,tool=1
     ret=rsi.put("MyValue1", 789)  # 添加 MyValue1 标签
     move L,spd=100mm/s,accu=1,tool=1

     # 发送停止
     rsi.off

     end


```
[__SOURCE](7-enet-module/README.md)
# 7 `enet` module : 以太网 TCP/UDP 通信

使用 ${cont_model} 控制器的用户以太网端口，您可以通过以太网 TCP 或 UDP 通信与外部设备发送和接收字符串或二进制数据。

`enet` 模块可以创建两个对象，`ENet` 和 `BBuf`。`ENet` 提供以太网套接字接口，而 `BBuf` 用于通信二进制数据。

让我们按照客户端示例和服务器示例来理解如何使用它。每个对象的成员变量和函数的参考指南随之而来。
[__SOURCE](7-enet-module/1-exam-client/README.md)
# 7.1 对等网络，客户端示例

UDP 对等网络 (1:1 通信) 或 TCP 客户端示例程序用于字符串和二进制传输的说明。
[__SOURCE](7-enet-module/1-exam-client/1-enet-client-str.md)
# 7.1.1 peer-to-peer, client 示例 - 传输字符串数据

按照以下步骤进行：

1. 在导入 `enet` 模块后，通过构造函数创建一个 `ENet` 对象。
2. 使用成员变量设置 IP 地址和端口号。
   - `注意：控制器上的端口 50000-50005 是预分配的 lports，无法使用。`
3. 使用 `open` 成员过程打开以太网套接字，并使用 `state()` 成员变量检查状态。
\(对于 TCP 通信，在打开之后还必须调用 `连接 (connect)` 过程。\)
1. 使用 `send` 和 `recv` 成员过程进行传输。
2. 使用 `关闭 (close)` 成员过程关闭通信连接。

<br>

### UDP peer-to-peer
```python
     # 1. 在导入 enet 模块后，通过构造函数创建一个 ENet 对象
     import enet
     var cli=enet.ENet() # 默认 enet 模式是 "udp"

     # 2. 设置 IP 地址和端口号
     cli.ip_addr="192.168.1.172" # 远程（对手）IP 地址
     cli.lport=51001 # 本地（自己）端口
     cli.rport=51002 # 远程（对手）端口
     # (端口号 49152-65535（排除 50000-50005）包含动态或私有端口)

     # 3. 打开以太网套接字
     cli.open
     
     print cli.state() # 如果是 1，则正常。

     # --------------------------------
     # 4-1. 字符串传输
     cli.send "hello, peer.\n"

     # 4-2. 字符串接收
     #     (如果 5 秒内未接收到，跳转到 *TimeOut 标签)
     var msg
     cli.recv 5000, *TimeOut
     var msg=result() # 接收到的字符串
     print msg
     delay 1.0
     # --------------------------------

     # 5. 关闭以太网套接字
     cli.close
     print cli.state() # 如果是 0，则正常。
     delay 1.5
     end

     *TimeOut
     print "时间到了!"
     cli.close
     end
```
<br>

### TCP client
(仅 `lport` 和 `连接 (connect)` 部分与 peer-to-peer 不同。)
```python
     # 1. 在导入 enet 模块后，通过构造函数创建一个 ENet 对象
     import enet
     var cli=enet.ENet("tcp")

     # 2. 设置 IP 地址和端口号
     cli.ip_addr="192.168.1.172" # 远程（对手）IP 地址
     cli.lport=0 # 本地（自己）端口；随机
     cli.rport=51002 # 远程（对手）端口
     # (端口号 49152-65535 包含动态或私有端口)

     # 3. 打开以太网套接字
     cli.open
     cli.connect # 连接到服务器。
     print cli.state() # 如果是 1，则正常。

     # --------------------------------
     # 4-1. 字符串传输
     cli.send "hello, peer.\n"

     # 4-2. 字符串接收
     #     (如果 5 秒内未接收到，跳转到 *TimeOut 标签)
     var msg
     cli.recv 5000, *TimeOut
     var msg=result() # 接收到的字符串
     print msg
     delay 1.0
     # --------------------------------

     # 5. 关闭以太网套接字
     cli.close
     print cli.state() # 如果是 0，则正常。
     delay 1.5
     end

     *TimeOut
     print "时间到了!"
     cli.close
     end
```
[__SOURCE](7-enet-module/1-exam-client/2-enet-client-bin.md)
# 7.1.2 点对点，客户端示例 - 发送和接收二进制数据

二进制传输使用 `BBuf`（二进制缓冲区）对象进行。  
（只有传输部分不同，其余部分与字符串数据的传输相同。）

发送

1. 创建 `enet.BBuf` 对象。
2. 使用 `BBuf.append()` 函数将所需的二进制数据附加到 `BBuf` 对象中。
3. 通过 `ENET.send_bbuf()` 函数发送 BBuf 对象。


接收

1. 创建 `enet.BBuf` 对象。
2. 使用 `ENET.recv_bbuf()` 函数将二进制数据接收至 BBuf 对象中。
3. 使用 `BBuf.read_nums()` 函数从 `BBuf` 对象中读取所需的二进制数据。


<br>

### UDP 点对点
```python
     # 1. 导入 enet 模块后，使用构造函数创建一个 ENet 对象
     import enet
     var cli=enet.ENet()

     # 2. 设置 IP 地址和端口号
     cli.ip_addr="192.168.1.172" # 远程（对手）IP 地址
     cli.lport=51001 # 本地（自己）端口
     cli.rport=51002 # 远程（对手）端口
     # (端口号 49152-65535（除 50000-50005）包含动态或私有端口)

     # 3. 打开以太网套接字
     cli.open
     
     print cli.state() # 如果 1，表示正常。

     # 发送 --------------------------------
     # 4-1. 创建 BBuf 对象
     var bbuf=enet.BBuf()

     # (示例二进制数据)
     var arr=[ -3, 0, 1 ]
     
     # 4-2. 将二进制数据附加到 BBuf 对象
     bbuf.clear()
     bbuf.append("s4", arr) # 附加小端签名的4字节数据

     # 4-3. 发送 BBuf 对象
     var ret
     ret=cli.send_bbuf(bbuf)

     # 接收 --------------------------------
     # 4-1. 创建 BBuf 对象
     var bbuf2=enet.BBuf()
     
     # 4-2. 将二进制数据接收至 BBuf 对象
     #     (如果 3 秒内没有响应，则跳转到 *TimeOut 标签)
     cli.recv_bbuf bbuf2,3000,*TimeOut

     # 4-3. 从 BBuf 对象读取二进制数据。
     var nums=bbuf2.read_nums("U2", 0, 3) # 读取 3 个大端无符号2字节数据
     print nums
     # --------------------------------

     # 5. 关闭以太网套接字
     cli.close
     print cli.state() # 如果 0，表示正常。
     delay 1.5
     end

     *TimeOut
     print "超时！"
     cli.close
     end
```


### TCP 客户端
（仅 `lport` 和 `连接 (connect)` 部分与点对点不同。）
```python
     # 1. 导入 enet 模块后，使用构造函数创建一个 ENet 对象
     import enet
     var cli=enet.ENet("tcp")

     # 2. 设置 IP 地址和端口号
     cli.ip_addr="192.168.1.172" # 远程（对手）IP 地址
     cli.lport=0 # 本地（自己）端口；随机
     cli.rport=51002 # 远程（对手）端口
     # (端口号 49152-65535 包含动态或私有端口)

     # 3. 打开以太网套接字
     cli.open
     cli.connect # 连接到服务器。
     print cli.state() # 如果 1，表示正常。

     # 发送 --------------------------------
     # 4-1. 创建 BBuf 对象
     var bbuf=enet.BBuf()

     # (示例二进制数据)
     var arr=[ -3, 0, 1 ]
     
     # 4-2. 将二进制数据附加到 BBuf 对象
     bbuf.clear()
     bbuf.append("s4", arr) # 附加小端签名的4字节数据

     # 4-3. 发送 BBuf 对象
     var ret
     ret=cli.send_bbuf(bbuf)

     # 接收 --------------------------------
     # 4-1. 创建 BBuf 对象
     var bbuf2=enet.BBuf()
     
     # 4-2. 将二进制数据接收至 BBuf 对象
     #     (如果 3 秒内没有响应，则跳转到 *TimeOut 标签)
     cli.recv_bbuf bbuf2,3000,*TimeOut

     # 4-3. 从 BBuf 对象读取二进制数据。
     var nums=bbuf2.read_nums("U2", 0, 3) # 读取 3 个大端无符号2字节数据
     print nums
     # --------------------------------

     # 5. 关闭以太网套接字
     cli.close
     print cli.state() # 如果 0，表示正常。
     delay 1.5
     end

     *TimeOut
     print "超时！"
     cli.close
     end
```

* 字符串参数，如 "s4" 和 "U2" 决定了二进制数据格式，如字节序类型、有符号/无符号和字节数。有关更多信息，请参阅 [7.4.2 支持的格式](../4-bbuf/2-format.md)。
[__SOURCE](7-enet-module/2-exam-server/README.md)
# 7.2 TCP 服务器示例

TCP 服务器示例程序解释了传输字符串数据和二进制数据的情况。

当 TCP 客户端使用 `connect()` 函数连接到服务器时，TCP 服务器调用 `listen()` 函数并使用 `accept()` 函数等待客户端的连接。

* 只允许同时连接一个客户端。
* 不需要指定远程端口。

其余的操作与客户端相同。
[__SOURCE](7-enet-module/2-exam-server/1-enet-server-str.md)
# 7.2.1 ethernet TCP server - 传输字符串数据

Follow these steps:

1. 在导入 `enet` 模块后，使用构造函数创建 `ENet` 对象。
2. 用成员变量设置 IP 地址和端口号。 (不需要设置远程端口。)
   - `注意: 控制器上的端口 50000-50005 是预分配的 lports，不能使用。`
3. 使用 `open` 成员过程打开以太网套接字，并调用 `listen()`、`accept()` 函数。使用 `state()` 成员变量检查状态。
4. 使用 `send` 和 `recv` 成员过程进行传输。
5. 使用 `关闭 (close)` 成员过程关闭通信连接。


```python
     # 1. 在导入 enet 模块后，创建一个 ENet 对象
     import enet
     var svr=enet.ENet("tcp")
     
     # 2. 设置 IP 地址和端口号
     svr.ip_addr="192.168.1.172" # 远程（对手）IP 地址
     svr.lport=51001 # 本地（自己）端口
     # (端口号 49152-65535（除 50000-50005 外）包含动态或私人端口)
     
     # 3. 打开以太网套接字
     svr.open
     var ret
     ret=svr.listen()
     ret=svr.accept() # 等待客户端连接
     print svr.state() # 如果为 1，则正常。
     
     # --------------------------------
     # 4-1. 字符串传输
     svr.send "欢迎，我是一个 TCP 服务器。\n"
     
     # 4-2. 字符串接收
     #     （如果 5 秒内未接收，跳转到 *TimeOut 标签）
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
     print "超时!"
     svr.close
     end
```
[__SOURCE](7-enet-module/2-exam-server/2-enet-server-bin.md)
# 7.2.2 ethernet TCP server 示例 - 双向传输二进制数据

二进制双向传输使用 `BBuf` (二进制缓冲区) 对象进行。  
(只有双向传输部分不同，其余与传输字符串数据相同。)

发送

1. 创建 `enet.BBuf` 对象。
2. 使用 `BBuf.append()` 函数将所需的二进制数据附加到 `BBuf` 对象。
3. 将 BBuf 对象发送为 `ENET.send_bbuf()` 函数的参数。

接收

1. 创建 `enet.BBuf` 对象。
2. 使用 `ENET.recv_bbuf()` 函数接收二进制数据到 BBuf 对象。
3. 使用 `BBuf.read_nums()` 函数从 `BBuf` 对象中读取所需的二进制数据。

```python
     # 1. 导入 enet 模块后，使用构造函数创建 ENet 对象
     import enet
     var svr=enet.ENet("tcp")
     
     # 2. 设置 IP 地址和端口号
     svr.ip_addr="192.168.1.172" # 远程（对方）IP 地址
     svr.lport=51001 # 本地（自身）端口
     # (端口号 49152-65535（除了 50000-50005）包含动态或私有端口)
     
     # 3. 打开以太网套接字
     svr.open
     var ret
     ret=svr.listen()
     ret=svr.accept() # 等待客户端连接
     print svr.state() # 如果为 1，则正常。

     # 发送 --------------------------------
     # 4-1. 创建 BBuf 对象
     var bbuf=enet.BBuf()

     # (示例二进制数据)
     var arr=[ -3, 0, 1 ]
     
     # 4-2. 将二进制数据附加到 BBuf 对象
     bbuf.clear()
     bbuf.append("s4", arr) # 附加小端签名4字节数据

     # 4-3. 发送 BBuf 对象
     ret=svr.send_bbuf(bbuf)

     # 接收 --------------------------------
     # 4-1. 创建 BBuf 对象
     var bbuf2=enet.BBuf()
     
     # 4-2. 接收二进制数据到 BBuf 对象
     #     (如果 3 秒没有响应，跳转到 *TimeOut 标签)
     svr.recv_bbuf bbuf2,3000,*TimeOut

     # 4-3. 从 BBuf 对象读取二进制数据。
     var nums=bbuf2.read_nums("U2", 0, 3) # 读取 3 个大端无符号2字节数据
     print nums
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

* 字符串参数如 "s4" 和 "U2" 决定二进制数据格式，如字节序类型、签名/无签名及字节数。有关更多信息，请参见 [7.4.2 支持的格式](../4-bbuf/2-format.md)。
[__SOURCE](7-enet-module/3-enet/README.md)
# 7.3 ENet 对象

The `ENet` object provides a socket interface for Ethernet communication.  
See the examples in the previous section for instructions on how to use them.
[__SOURCE](7-enet-module/3-enet/1-enet-creator.md)
# 7.3.1 `ENet` 创建者

### 描述

创建一个以太网对象。返回创建对象的引用。

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
        如果省略，将被识别为 "udp"。</td>
    </tr>
  </tbody>
</table>

### 返回值

创建对象的引用。

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
      <th style="text-align:left">变量名</th>
      <th style="text-align:left">数据类型</th>
      <th style="text-align:left">描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">ip_addr</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        可读/可写<br>
        设置或获取通信对手（远程）的 IP 地址。<br>
        仅在调用 open 语句时应用。
      </td>
    </tr>
    <tr>
      <td style="text-align:left">rport</td>
      <td style="text-align:left">number</td>
      <td style="text-align:left">
        可读/可写<br>
        设置或获取通信对手（远程）的端口号。<br>
        仅在调用 open 语句时应用。
      </td>
    </tr>
    <tr>
      <td style="text-align:left">lport</td>
      <td style="text-align:left">number</td>
      <td style="text-align:left">
        可读/可写<br>
        仅在 UDP 对等和 TCP 服务器中使用，在 TCP 客户端中被忽略。<br>
        设置或获取控制器自己的（本地）端口号。<br>
        默认值为 0（如果未指定），在这种情况下，此端口号将自动生成。<br>
        仅在调用 open 语句时应用。<br>
        控制器上的 50000-50005 端口是预分配的 lports，无法使用。
      </td>
    </tr>
  </tbody>
</table>
[__SOURCE](7-enet-module/3-enet/3-enet-member-func/README.md)
# 7.3.3 `ENet` 成员函数

* 当从成员函数获取返回值时，请确保将参数用括号括起来。
  
  ```python
  var nitem=obj.func(param1,param2) # (O) ; 括号是必需的
  var nitem=obj.func param1,param2 # (X) ; 语法错误
  ```

* 可以省略括号，未获取返回值。

  ```python
  obj.func(param1,param2) # (O)
  obj.func param1,param2 # (O) ; 括号省略
  ```
[__SOURCE](7-enet-module/3-enet/3-enet-member-func/enet-accept.md)
# `accept`

### Description

作为以太网 TCP 通信中的服务器，它等待来自客户端的连接请求。当请求发生时，创建连接。  
不用于 UDP 对等通信。


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
        超时。如果经过，则继续执行下一个命令或跳转到超时地址。<br>
        如果未指定，则无限期等待。
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>address on timeout</td>
      <td>
        超时时跳转的地址。<br>
        如果未指定，则继续执行下一个命令。
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
        OK (完成)
      </td>
      <td></td>
    </tr>  
    <tr>
      <td>0</td>
      <td>
        等待中
      </td>
      <td></td>
    </tr>
    <tr>
      <td>-1</td>
      <td>超时</td>
      <td></td>
    </tr>
    <tr>
      <td>-2</td>
      <td>错误</td>
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
# `关闭 (close)`

### 描述

关闭以进行以太网 TCP 或 UDP 通信的连接。

### 语法

`{ENet object}.close`

### 示例

```python
enet_to_sensor.close
```
[__SOURCE](7-enet-module/3-enet/3-enet-member-func/enet-connect.md)
# `连接 (connect)`

### 描述


作为以太网 TCP 通信中的客户端，它尝试连接到服务器。
在 UDP 对等通信中不使用。

### 语法

`{ENet object}.connect [{等待时间}] [, {超时地址}]`


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
      <td>等待时间</td>
      <td>
        超时。如果经过，则继续下一个命令或跳转到超时地址。<br>
        如果未指定，则无限期等待。
      </td>
      <td>毫秒</td>
    </tr>
    <tr>
      <td>超时地址</td>
      <td>
        超时时跳转的地址。<br>
        如果未指定，则继续下一个命令。
      </td>
      <td>地址</td>
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
      <td>1</td>
      <td>
        成功（完成）
      </td>
      <td></td>
    </tr>  
    <tr>
      <td>0</td>
      <td>
        等待中
      </td>
      <td></td>
    </tr>
    <tr>
      <td>-1</td>
      <td>超时</td>
      <td></td>
    </tr>
    <tr>
      <td>-2</td>
      <td>错误</td>
      <td></td>
    </tr>  
  </tbody>
</table>


### 示例

```python
var ret=enet_to_sensor.connect(5000)
```

```python
enet_to_sensor.connect 5000,*TimeOut
```
[__SOURCE](7-enet-module/3-enet/3-enet-member-func/enet-listen.md)
# `listen`

### Description

作为以太网 TCP 通信中的服务器，它为客户端的连接请求做准备。 
在 UDP 点对点通信中未使用。


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
        未被接受的待处理连接的允许连接数。<br>
        如果未指定，将无限期等待。
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
      <td>错误</td>
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
# `open`

### 描述

打开以进行以太网 TCP 或 UDP 通信的连接。

### 语法

`{ENet object}.open`

### 示例

```python
enet_to_sensor.open
```
[__SOURCE](7-enet-module/3-enet/3-enet-member-func/enet-recv.md)
# `recv`

### Description

从以太网对象接收字符串数据。接收到的字符串可以通过返回值或 `result()` 函数获取。


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
        超时。如果超时，则执行下一个命令或跳转到超时的地址。<br>
        如果未指定，则无限期等待。
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>address on timeout</td>
      <td>
        超时后跳转的地址。<br>
        如果未指定，则执行下一个命令。
      </td>
      <td>address</td>
    </tr>
  </tbody>
</table>


### Return value

接收到的字符串。


### Example

```python
var msg
msg=enet_to_sensor.recv
msg=enet_to_sensor.recv(5000)
msg=enet_to_sensor.recv(5000,*TimeOut)
end

*TimeOut
print "超时！来自传感器没有响应"
end
```
[__SOURCE](7-enet-module/3-enet/3-enet-member-func/enet-recv_bbuf.md)
# `recv_bbuf`

### Description

从以太网对象接收二进制数据并将其存储在 [BBuf](../../4-bbuf/README.md) 对象中。


### Syntax

`{ENet object}.recv_bbuf {BBuf onject}[,{waiting time}][,{address on timeout}]`


### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">名称</th>
      <th style="text-align:left">含义</th>
      <th style="text-align:left">杂项</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>BBuf object</td>
      <td>
        用于存储接收到的二进制数据的BBuf对象
      </td>
      <td></td>
    </tr>
    <tr>
      <td>waiting time</td>
      <td>
        超时。如果超时，则继续执行下一个命令或跳转到超时地址。<br>
        如果未指定，则无限等待。
      </td>
      <td>毫秒</td>
    </tr>
    <tr>
      <td>address on timeout</td>
      <td>
        超时后跳转到的地址。<br>
        如果未指定，继续执行下一个命令。
      </td>
      <td>地址</td>
    </tr>
  </tbody>
</table>


### Return value

接收到的数据数量。


### Example

```python
var bbuf=enet_to_sensor.BBuf()
enet_to_sensor.recv bbuf
enet_to_sensor.recv bbuf, 5000
var nitem=enet_to_sensor.recv(bbuf,5000,*TimeOut)
end

*TimeOut
print "超时！传感器无响应"
end
```
[__SOURCE](7-enet-module/3-enet/3-enet-member-func/enet-send.md)
# `send`

### Description

将字符串数据发送到以太网对象。

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
        要发送的字符串
      </td>
      <td style="text-align:left">字符串</td>
    </tr>
  </tbody>
</table>

### Return value

发送的字节数。

### Example

```python
enet_to_sensor.send "rob:"+10+", command:"+cmd+"\n"
```
[__SOURCE](7-enet-module/3-enet/3-enet-member-func/enet-send_bbuf.md)
# `send_bbuf`

### Description

发送 [BBuf](../../4-bbuf/README.md) 对象到以太网对象。


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
        要发送的二进制缓冲区对象。
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>


### Return value

发送的字节数。


### Example

```python
var bbuf=enet.BBuf()
var arr=[ -3, 0, 1 ]
bbuf.append("s4", arr)
var nitem=cli.send_bbuf(bbuf)
```
[__SOURCE](7-enet-module/3-enet/3-enet-member-func/enet-set_send_trail_null.md)
# `set_send_trail_null`

### Description

当使用 `ENet.send()` 函数发送字符串时，它设置是否附加终止空字符发送。（默认值为 false）

### Syntax

`{ENet object}.set_send_trail_null(true|false)`

### Return value

无。

### Example

```python
enet_to_sensor.set_send_trail_null(true)
enet_to_sensor.send "ACK"
enet_to_sensor.set_send_trail_null(false)
```
[__SOURCE](7-enet-module/3-enet/3-enet-member-func/enet-state.md)
# `状态 (state)`

### Description

返回以太网对象的状态。


### Syntax

`{ENet object}.state`


### Return value

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
      <td>1</td>
      <td>
        已连接。 <br>
        （在UDP的情况下，甚至仅仅是`open`也被视为已连接。<br>
         在TCP的情况下，只有在`open`之后执行`listen`、`连接 (connect)`和`accept`时才被视为已连接。
      </td>
      <td></td>
    </tr>
    <tr>
      <td>0</td>
      <td>未连接。</td>
      <td></td>
    </tr>
    <tr>
      <td>-1</td>
      <td>创建以太网套接字失败。</td>
      <td></td>
    </tr>
    <tr>
      <td>-2</td>
      <td>绑定以太网套接字失败。</td>
      <td></td>
    </tr>
    <tr>
      <td>-3</td>
      <td>连接失败。</td>
      <td></td>
    </tr>
    <tr>
      <td>-4</td>
      <td>监听失败。</td>
      <td></td>
    </tr>
    <tr>
      <td>-5</td>
      <td>接受失败。</td>
      <td></td>
    </tr>
  </tbody>
</table>


### Example

```python
var ret = enet_to_sensor.state()
```
[__SOURCE](7-enet-module/4-bbuf/README.md)
# 7.4 `BBuf` 对象

A `BBuf (Binary Buffer)` 对象封装要通过以太网通信发送和接收的二进制数据。
有关用法，请参见二进制通信示例。

[7.1.2 点对点，客户端示例 - 二进制传输](../1-exam-client/2-enet-client-bin.md)

[7.2.2 以太网 TCP 服务器 - 二进制传输](../2-exam-server/2-enet-server-bin.md)
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

成员函数 `append()` 或 `read_num()` 需要指定类型作为参数。

该格式由 1 个字母表示有符号/无符号/浮点数和 1 个数字表示字节数构成。<br>
如果字母是大写，则为大端字节序；如果是小写，则为小端字节序。

<table>
  <thead>
    <tr>
      <th>格式</th>
      <th>字节序</th>
      <th>类型</th>
      <th>字节数</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>"S1"</td>
      <td>大端字节序<br>
      <td>有符号整数<br>
      <td>1字节<br>
    </tr>
    <tr>
      <td>"S2"</td>
      <td>大端字节序<br>
      <td>有符号整数<br>
      <td>2字节<br>
    </tr>
    <tr>
      <td>"S4"</td>
      <td>大端字节序<br>
      <td>有符号整数<br>
      <td>4字节<br>
    </tr>
    <tr>
      <td>"U1"</td>
      <td>大端字节序<br>
      <td>无符号整数<br>
      <td>1字节<br>
    </tr>
    <tr>
      <td>"U2"</td>
      <td>大端字节序<br>
      <td>无符号整数<br>
      <td>2字节<br>
    </tr>
    <tr>
      <td>"U4"</td>
      <td>大端字节序<br>
      <td>无符号整数<br>
      <td>4字节<br>
    </tr>
    <tr>
      <td>"F4"</td>
      <td>大端字节序<br>
      <td>单精度实数<br>
      <td>4字节<br>
    </tr>
    <tr>
      <td>"F8"</td>
      <td>大端字节序<br>
      <td>双精度实数<br>
      <td>8字节<br>
    </tr>
    <tr>
      <td>"s1"</td>
      <td>小端字节序<br>
      <td>有符号整数<br>
      <td>1字节<br>
    </tr>
    <tr>
      <td>"s2"</td>
      <td>小端字节序<br>
      <td>有符号整数<br>
      <td>2字节<br>
    </tr>
    <tr>
      <td>"s4"</td>
      <td>小端字节序<br>
      <td>有符号整数<br>
      <td>4字节<br>
    </tr>
    <tr>
      <td>"u1"</td>
      <td>小端字节序<br>
      <td>无符号整数<br>
      <td>1字节<br>
    </tr>
    <tr>
      <td>"u2"</td>
      <td>小端字节序<br>
      <td>无符号整数<br>
      <td>2字节<br>
    </tr>
    <tr>
      <td>"u4"</td>
      <td>小端字节序<br>
      <td>无符号整数<br>
      <td>4字节<br>
    </tr>
    <tr>
      <td>"f4"</td>
      <td>小端字节序<br>
      <td>单精度实数<br>
      <td>4字节<br>
    </tr>
    <tr>
      <td>"f8"</td>
      <td>小端字节序<br>
      <td>双精度实数<br>
      <td>8字节<br>
    </tr>
	 <tr>

  </tbody>
</table>
[__SOURCE](7-enet-module/4-bbuf/3-bbuf-member-func/README.md)
# 7.4.2 `BBuf` 成员函数
[__SOURCE](7-enet-module/4-bbuf/3-bbuf-member-func/bbuf-append.md)
# `添加 (append)`

### Description

将指定格式的数据附加到二进制缓冲区。

### Syntax

`{BBuf object}.append {format},{data}`

### Parameters

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
      <td style="text-align:left">format</td>
      <td style="text-align:left">二进制格式<sup>*</sup><br>
      例如 "U4", "s2"
      </td>
      <td style="text-align:left">字符串</td>
    </tr>
    <tr>
      <td style="text-align:left">data</td>
      <td style="text-align:left">
        要附加到二进制缓冲区的数据
      </td>
      <td style="text-align:left">原始数据,<br>或原始数据的1-D数组</td>
    </tr>
  </tbody>
</table>

<br>

* 请参阅 [7.4.2 支持的格式](../2-format.md)。
* 如果数据与指定格式类型不同，将自动隐式转换类型。例如，如果格式为 "s2"（2字节整数），而数据为浮点值 3.7，则整数值 3(0x0003) 将附加到缓冲区。相反，如果格式为 "f4"（4字节实数），而数据为整数值 -3，则实值 -3.0(0xC0400000) 将存储在缓冲区中。
* 如果格式为无符号，而数据为负数，则会发生错误，因此请小心。

<br>

### Return value

附加的数据数量。

### Example

```python
var bbuf=enet.BBuf()
bbuf.append("F8", 9.80665)
bbuf.append("U4", [2, 3, 5, 7, 11, 13])
```
[__SOURCE](7-enet-module/4-bbuf/3-bbuf-member-func/bbuf-clear.md)
# `初始化 (clear)`

### Description

删除存储在二进制缓冲区中的所有数据。


### Syntax

`{BBuf object}.clear()`


### Parameters

无


### Example

```python
var bbuf=enet.BBuf()
bbuf.append("s4", 20)
bbuf.append("s4", -10)
bbuf.clear()
```
[__SOURCE](7-enet-module/4-bbuf/3-bbuf-member-func/bbuf-nbyte.md)
# `nbyte`

### Syntax

`{BBuf object}.nbyte`


### Return value

二进制数据的字节数


### Example

```python
var bbuf=enet.BBuf()
bbuf.append("s4", 20)
bbuf.append("s4", -10)
print bbuf.nbyte() # "8"
```
[__SOURCE](7-enet-module/4-bbuf/3-bbuf-member-func/bbuf-read_num.md)
# `read_num`

### Description

从二进制缓冲区的指定位置读取数值，并返回该值。

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
      <td style="text-align:left">二进制数据格式<sup>*</sup><br>
      例如 "U4", "s2"<br>
      </td>
      <td style="text-align:left">string</td>
    </tr>
	 <tr>
      <td style="text-align:left">offset</td>
      <td style="text-align:left">
        读取数据的位置 (0-based byte offset)
      </td>
      <td style="text-align:left">integer</td>
    </tr>
  </tbody>
</table>

<br>

\* 请参见 [7.4.2 Supported format](../2-format.md).
<br>
<br>

### Return value

* 读取的数值
* 如果在读取数据类型时发生错误，则返回 0。

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
# `read_nums`

### Description

从二进制缓冲区的指定位置读取指定数量的数值，并以数组格式返回。


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
			二进制数据格式<sup>*</sup><br>
      例如 "U4", "s2"
      </td>
      <td style="text-align:left">string</td>
    </tr>
	  <tr>
      <td style="text-align:left">offset</td>
      <td style="text-align:left">
        读取数据的位置（基于0的字节偏移量）
      </td>
      <td style="text-align:left">integer</td>
    </tr>
    <tr>
      <td style="text-align:left">n.item</td>
      <td style="text-align:left">
        要读取的数据数量
      </td>
      <td style="text-align:left">integer</td>
    </tr>
  </tbody>
</table>

<br>


\* 请参阅 [7.4.2 Supported format](../2-format.md).
<br>
<br>


### Return value

* 读取的数值数组。
* 如果缓冲区中的数据数量少于指定的数量，则仅读取可用的数量。
* 如果在读取数据类型时发生错误，则返回空数组。


### Example

```python
var bbuf=enet.BBuf()
bbuf.append("F8", 9.80665)
bbuf.append("U4", [2, 3, 5, 7, 11, 13])
print bbuf.read_nums("U4", 12, 3) # "[3, 5, 7]"
print bbuf.read_num("U4", 12, 6) # "[3, 5, 7, 11, 13]"
```
[__SOURCE](8-alias.md)
# 8. 别名

别名是一个可以用作变量或对象属性的替代表示法的名称。

别名是一个可以用来表示变量或对象的替代名称。您可以用简短的名称替换那些过长的属性表示法，或者用更易读的名称替换特定索引的 IO 变量。

别名通过 `alias` 语句定义，语法与 `var` 或 `global` 几乎相同。

别名的作用域与全局范围相同。也就是说，在执行 `alias` 语句后，它可以在任何后续作业中使用，即使程序周期通过主程序的 `end` 语句或 `R0 - [ENTER]` 操作被重置，它也不会被销毁。

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

在上面示例的(1)中，输出变量 `fb3.do4` 被定义为名为 `grip` 的别名，而输入变量 `fb1.diw2` 被定义为别名 `work_no`。  
在(2)中，作为 `profile` 属性的角色数组被定义为别名 `role`。  
在(3)中，内置对象 `project.robot.tools.t_0` 被定义为别名 `tool0`，这指向工具数据 \#0。

对于引用数组的别名，其元素可以用 [ ] 操作符指定，如 `role[1]`。  
对于引用对象的别名，其属性可以用 . 操作符指定，如 `tool0.mass`。

常量不能定义为别名。请使用 `global` 或 `var` 定义它。  
表达式也不能定义为别名。要小心，因为这可能导致故障。

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

在 ${cont_model} 控制器的 MAIN 模块的文件系统中，描述了创建、复制和删除目录和文件的指令。
[__SOURCE](9-file/1-file-system/1-mkdir.md)
# 9.1.1 `mkdir`

`mkdir` 是创建目录的过程。

### 描述

在 MAIN 模块中为指定路径创建目录。

- 您无法在 Teach Pendant 或 USB 存储器上创建目录。
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

A `copyfile` 是请求复制目录或文件的程序。

### Description

将指定源路径的目录或文件复制到指定的目标路径名称。

- 只能在 MAIN 模块内执行，不能在 Teach Pendant 或 USB 存储器中执行。
- 如果目标路径名称的中间路径不存在，则会创建中间路径。
- 如果目标目录已存在，则删除它并复制源目录。
- 如果目标文件已存在，则覆盖它。
- 目录中的所有子目录也将被复制。
- 目标路径名称也支持通配符 ('*', '?')。

- 因为可能会复制大型文件或整个目录，因此它在后台异步执行，以避免因复制时等待而导致的节拍时间损失。换句话说，当执行 `copyfile` 语句时，启动后台任务中的复制，立刻继续执行下一个语句。例如，您可以请求复制并执行移动语句。可以通过读取结果变量的值来确定复制是否成功完成。（也就是说，当复制失败时，不会生成错误或警告。）

- 在一项复制或删除完成之前，您无法请求另一项复制或删除。

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
        背景执行的结果<br>
        <ul>
        <li>1: 成功完成。</li>
        <li>0: 复制进行中。</li>
        <li>-1: 源路径名称无效。</li>
        <li>-2: 目标路径名称无效。</li>
        <li>-3: 复制失败。</li>
        <li>-6: 复制通配符时全部失败。</li>
        <li>-7: 复制通配符时部分失败。</li>
        <li>-11: 创建临时路径失败。</li>
        <li>-12: 复制到临时路径失败。</li>
        <li>-13: 清除现有目标路径失败。</li>
        <li>-14: 目标路径创建失败。</li>
        <li>-15: 从临时路径移动到目标路径失败。</li>
        </ul>
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">source pathname</td>
      <td style="text-align:left">
        要复制的目录路径,<br>
        或要复制的文件路径名称
      </td>
      <td style="text-align:left">string expression</td>
    </tr>
    <tr>
      <td style="text-align:left">string expression</td>
      <td style="text-align:left">
        - 以 '/' 结尾：要复制的路径。<br>
        - 不以 '/' 结尾：通过复制将创建的路径名称。
      </td>
      <td style="text-align:left">string expression</td>
    </tr>
  </tbody>
</table>

### Sample

```python
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
```

![](../../_assets/copyfile.png)
[__SOURCE](9-file/1-file-system/3-delfile.md)
# 9.1.3 `delfile`

A `delfile` 是一个请求删除目录或文件的过程。

### Description

在指定路径中删除目录或文件。

- 只能在 MAIN 模块内执行，不能在 Teach Pendant 或 USB 内存中执行。
- 目录中的所有子目录也会被删除。
- 如果指定的路径不存在，操作成功结束。
- 路径名还支持通配符 ('*', '?')。

- 因为可能会删除大文件或整个目录，所以它在后台异步进行，以避免在删除期间由于等待而导致的触发时间损失。可以通过读取结果变量的值来确定删除是否成功完成。 （即，当删除失败时，不会生成错误或警告。）

- 在一个复制或删除完成之前，你不能请求另一个复制或删除。

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
        背景执行的结果<br>
        <ul>
        <li>1: 成功完成。</li>
        <li>0: 删除进行中。</li>
        <li>-41: 删除目录失败。</li>
        <li>-42: 删除文件失败。</li>
        </ul>
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">pathname</td>
      <td style="text-align:left">
        要删除的目录路径，<br>
        或要删除的文件路径
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

解释将文件加载/保存到/从${cont_model}控制器的MAIN模块内存的语句。
[__SOURCE](9-file/2-load-save/1-load_job.md)
# 9.2.1 `load_job`

声明读取 MAIN 模块的 project/jobs/ 文件夹的更改以更新内存。


### 描述

将 MAIN 模块的 project/jobs/ 文件夹中的作业加载到新内存中。

如果您通过 FTP 或 copyfile 命令将 .job 文件复制或覆盖到 jobs/ 文件夹中，则必须执行此语句以反映内存，从而能够选择或调用作业。

- 注意：内存中不存在于 jobs/ 文件夹中的作业将被删除。
- 如果文件的修改时间不同，则会加载该文件。
- 内存中不存在的文件会被加载。

- 由于可以加载大容量 .jobs，因此在后台异步执行，以避免由于加载引起的节拍时间损失。可以通过读取结果变量的值判断加载是否成功完成。
- 当前加载完成之前，无法请求另一个加载。


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
        后台执行的结果<br>
        <ul>
        <li>1：成功完成。</li>
        <li>0：加载进行中。</li>
        </ul>
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">job filename</td>
      <td style="text-align:left">
        您只能使用 "*" 参数，这意味着所有文件。
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

支持从 V60.28-00 开始。

声明将对 MAIN 模块的 `project/vars/` 文件夹中的 .csv 文件（根全局数组）进行内存读取。

### 描述

HRScript 的全局根数组存储在 `vars/` 文件夹中，格式为 CSV 标准格式的文件。（"根" 意味着它不是另一个数组或对象的属性。）

有关变量文件的信息，请参阅以下操作手册链接。

[global variable/variable file](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/6-monitoring/3-job/3-global-variable/3-var-files?cont_model=${cont_model})

您可以使用 PC 上的文本编辑器轻松编辑 .csv 文件。
复制到 `vars/` 文件夹的编辑文件不会立即反映在内存中，而是通过在 TeachPendant 的全局变量窗口中使用 `[load all]` 功能或执行 `load_csv` 语句来实现。

- 由于较大的 .csv 文件可以加载，因此在后台异步执行以避免由于加载而导致的节拍时间损失。通过读取结果变量的值可以确定加载是否成功。
- 当前加载完成之前，不能请求另一个加载。

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
        <li>0: 正在加载中。</li>
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
如果您使用 "*" 加载所有 .csv，则内存中没有 `vars/` 文件夹中的 .csv 的根数组将被删除。
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

支持从 V60.28-00 开始。

声明将全局根数组变量存储到内存中，作为 .csv 文件，位于 MAIN 模块的 `project/vars/` 文件夹中。

### 描述

HRScript 的全局根数组存储在 `vars/` 文件夹中，作为 CSV 标准格式的文件。（“根”意味着它不是另一个数组或对象的属性。）

有关变量文件的信息，请参阅以下操作手册链接。

[global variable/variable file](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/6-monitoring/3-job/3-global-variable/3-var-files?cont_model=${cont_model})

全局根数组并不会在值更改时立即存储到 .csv 文件中。
当你按下 `Ctrl+[F7: save]` 或关闭电源时会将其保存为文件，并且你可以通过执行 `save_csv` 命令立即将其保存为文件。

- 因为可以保存大 .csv 文件，它们在后台异步执行，以避免因保存导致的失去节拍时间。可以通过读取结果变量的值来确定保存是否成功。
- 在当前保存完成之前，无法请求另一次保存。

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
        <li>0: 正在保存。</li>
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
如果通过指定 "*" 保存所有 .csv， 它不会删除 `vars/` 文件夹中的 .csv 文件，因为对应名称的根变量不存在。
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
     print "failed to save new locations."
     end
```
[__SOURCE](10-etc/README.md)
# 10. 其他事项
[__SOURCE](10-etc/1-proc/README.md)
# 10.1 其他程序
[__SOURCE](10-etc/1-proc/1-gather.md)
# 10.1.1 `gather`

`gather` 是指定数据收集功能开始和结束的过程。

### 描述

使用 `gather` 指定收集的开始和结束。收集结果文件保存如下；
- 存储路径：MAIN/project
- 文件名：0001.GDT 到 0030.GDT

最多存储 30 个收集结果文件，如果数量超出，则将覆盖先前的收集结果文件。

`gather_state()` 函数返回当前数据收集操作的状态。
  - 0 : 不在收集中。
  - 1 : 在收集中。 (gather 1 ~ gather 0)
  - 2 : 正在将收集结果保存为文件。 (gather 0~)

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

`tonl` 语句是在开始和结束之间执行位置修正的过程。

### 描述

如果您知道坐标变换关系，当您输入变换关系而不计算单独的坐标变换关系时，将应用此过程。

```python
R=[x,y,z,rx,ry,rz]
```

![](../../_assets/tonl2.png)

对于旋转矩阵，它按 Rot_z.Rot_y.Rot_x 的顺序应用。

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
        <li>on: 开始</li>
        <li>off: 结束</li>
        </ul>
      </td>
      <td style="text-align:left">开/关</td>
    </tr>
    <tr>
      <td style="text-align:left">shift</td>
      <td style="text-align:left">
        移动量
      </td>
      <td style="text-align:left">移动表达式</td>
    </tr>
  </tbody>
</table>

### 示例

```python
   global sft
   enet1.recv msg # 通过以太网接收移动量
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

`seltool` 是一个更改工具编号的过程。

### 描述

工具分为附加在机器人法兰上的机器人工具和单独安装的站点工具，`seltool` 更改每种类型的工具编号。

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
      <td style="text-align:left">tool number</td>
      <td style="text-align:left">
        工具编号<br>
        <ul>
        <li>机器人工具: 0 ~ 31</li>
        <li>站点工具: 0 ~ 3</li>
        </ul>
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">tool type</td>
      <td style="text-align:left">
        要更改工具编号的工具类型<br>
        <ul>
        <li>机器人工具: robot</li>
        <li>站点工具: station</li>
        </ul>
      </td>
      <td style="text-align:left">robot/station</td>
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

`triggout` 是一个允许您调整信号输出时间点，使其提前输出 (-) 或延迟输出 (+) 的过程。

### 描述

在持续处理命令的 contpath 1 或 2 的间隔中，您可以在命令位置到达目标位置时（准确性 OK）调整信号输出时间点，使其提前输出 (-) 或延迟输出 (+)。

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
      <td style="text-align:left">输出变量</td>
    </tr>
    <tr>
      <td style="text-align:left">output value</td>
      <td style="text-align:left">
        当为位输出(do, so)时，0 为关闭，非 0 为开启
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">ahead/behind time</td>
      <td style="text-align:left">
        -10.00 ~ 2.00 [s]<br>
        如果为 (-)，则信号在目标位置到达之前输出；如果为 (+)，则在到达之后输出。
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">ahead/behind distance</td>
      <td style="text-align:left">
        -3000 ~ 3000 [mm]<br>
        如果为 (-)，则信号在目标位置到达之前输出；如果为 (+)，则在到达之后输出。
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">x, y, z 方向的绝对位置</td>
      <td style="text-align:left">
        -3000 ~ 3000 [mm]
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">tcp 或轴向的相对距离<br>
      tcp : 如果 j=0 则<br>
      轴向方向 : 如果 j=1 以上则<br>
      </td>
      <td style="text-align:left">
        tcp : -3000 ~ 3000 [mm], 轴向方向 : -3000 ~ 3000 [mm] 或 [deg]<br>
        如果为 (-)，则信号在相对距离到达之前输出；如果为 (+)，则在到达之后输出。
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
  </tbody>
</table>

### 示例

```python
   move L,spd=300mm/s,accu=3,tool=1
   triggout do1,val=1,time=-0.5 #在达到步骤前0.5秒打开do1
   triggout do1,val=1,dist=-100.0,j=0 #当tcp到达步骤位置和相对距离-100mm时打开do1
   triggout do1,val=1,dist=-3.0,j=1 #当轴 1 到达步骤位置和相对距离-100mm时打开do1
   triggout do1,val=1,x=-100.0 #当X坐标值达到-100mm时打开do1
   triggout do1,val=1,x=-100.0,y=-100.0 #当X, Y坐标值达到-100mm时打开do1
   move L,spd=30%,accu=2,tool=1
   end
```

{% hint style="warning" %}
* **包含 `triggout` 命令的步骤** 用作参考点，系统检查是否在 **下一个步骤结束之前发出信号**。  
* 如果 **在该时间范围内没有信号输出**，则显示以下警告：  
  **W0241: _"在步骤范围内未输出triggout信号。"_**

{% endhint %}
[__SOURCE](10-etc/1-proc/5-intr_def.md)
# 10.1.5 `intr_def`

`intr_def` 是一个定义中断条件、观察间隔和中断发生时运行的程序的过程。

### 语法

中断功能是一种程序调用。当机器人在中断观察间隔内工作时，它会在满足预定义的中断条件时调用指定的任务。当被调用的程序完成运行后，它会返回到之前运行的程序的位置并继续运行。

![](../../_assets/intr_def_1.png)

### 简介

- 仅在中断观察间隔内操作。
- 支持算术表达式作为中断条件表达式。
- 在执行中断程序时允许其他中断处理（多个中断）。

### 中断被清除的时间点

如果发生以下操作，所有定义的中断会自动清除。

- 执行 'R0: 任务重置' 时
- 程序首次运行时
- 在更改程序计数器（步骤/功能 #）后启动时

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
        <li>on: 定义一个新的中断。</li>
        <li>off: 删除已定义的中断。（忽略第3个及后续参数。）</li>
        </ul>
      </td>
      <td style="text-align:left">on/off</td>
    </tr>
    <tr>
      <td style="text-align:left">中断编号</td>
      <td style="text-align:left">
        要定义或删除的中断编号。<br>
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">中断条件</td>
      <td style="text-align:left">
        导致中断的条件表达式。
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">条件匹配值</td>
      <td style="text-align:left">
        生成中断的条件表达式的值。
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">调用程序编号</td>
      <td style="text-align:left">
        中断发生时要调用的程序编号。
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">[once]</td>
      <td style="text-align:left">
        在中断观察间隔中仅处理一次中断，而不处理额外的中断。
      </td>
      <td style="text-align:left">once</td>
    </tr>
  </tbody>
</table>

### 错误

- E1351 : 当不删除就重新定义已经定义的中断编号时发生。请检查创建的程序。

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

`typeof` 是获取变量或表达式类型的过程。结果通过 `result()` 函数返回。

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

The `gasp_check` statement estimates the pressure of the gas spring mounted on the robot and checks whether it is normal.

### Description

![](../../_assets/gasp_check.png)

- To estimate the pressure, the axis equipped with the gas spring is reciprocated by -20 degrees from its current position.(Recommended to be performed at the H-axis 140 degree position)
- You can monitor pressure by saving the estimated pressure as a variable.
- 用户可以输入正常压力和容差。如果估算的压力超出范围，设定的错误输出信号会开启。

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
        正常压力作为错误发生的参考值[bar]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">tolerance</td>
      <td style="text-align:left">
        估计压力误差容差[bar]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">error output signal</td>
      <td style="text-align:left">
        信号输出当错误发生时
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
* For accurate estimation, [Axis add weight setting](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/7-system/4-robot-parameter/7-axis-add-weight/README?cont_model=${cont_model}) and [Load estimation function](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/7-system/7-auto-calibration/3-load-estimation?cont_model=${cont_model}) must be preceded before using the function.
* For a detailed description of the gas spring pressure check monitoring function, please refer to the link below.
[](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/6-monitoring/4-system/2-system-diagnosis/2-gas-pressure-check?cont_model=${cont_model})
* The estimated gas spring pressure may vary depending on the initial posture at the start of measurement.
During the robot's initial setup, please manage the pressure values based on the measurements taken at each reference posture, and regularly measure the pressure in the same posture to compare it with the initial values.
If a significant difference is observed in the measured values, please inspect the condition of the equipment.  

{% endhint %}
[__SOURCE](10-etc/1-proc/8-optime.md)
# 10.1.8 `optime`

`optime` 语句是一种用于启动或更新操作时间测量的过程。

### 描述

通常，操作时间的测量在按下启动按钮时开始，并且当程序执行 `end` 时，操作时间会自动更新。  
然而，如果程序在不执行 `end` 的情况下使用 `goto` 语句跳回开头，操作时间将继续增加。在这种情况下，监控的操作时间值变得毫无意义。

为了解决这种情况，`optime` 语句允许用户明确指定操作时间测量开始和更新的点。

### 语法
```python
optime <parameter>
```
### 参数
| 项目      | 描述                                                              | 备注 |
| --------- | ------------------------------------------------------------------ | ---- |
| 参数      | - cycle_start: 开始测量<br>- cycle_end: 更新测量                 |      |

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

`count_up` 语句是一个过程，它将指定变量的值增加 1，当超过预设值时将其重置为初始值。

### 描述

每次执行该语句时，它会将指定变量的值增加 1。  
如果变量值超过预设值，则将变量重置为指定的初始值。

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
| 项目     | 描述                                                                   | 备注    |
| -------- | ---------------------------------------------------------------------- | ------- |
| 变量     | 作为计数器，其值将被增加的变量                                        |         |
| init     | 当变量超过预设值时分配的初始值                                        |         |
| preset   | 变量的最大值                                                          |         |

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

`count_dn` 语句是一个过程，它将指定变量的值减少 1，当该值小于预设值时，将其重置为初始值。

### 描述

该语句每次执行时将指定变量的值减少 1。  
如果变量值小于预设值，则变量被重置为初始值指定的值。

执行  
```python
count_dn cnt, init=100, preset=0
```
的结果与执行以下四行代码的结果相同：

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
| 项目     | 描述                                                                 | 备注 |
| -------- | ---------------------------------------------------------------------- | ----- |
| 变量     | 将作为计数器减少值的变量                                             |       |
| init     | 当变量小于 `preset` 值时要分配的初始值                             |       |
| preset   | 变量的最小值                                                          |       |


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

`cycle_end` 语句是一个过程，清除所有由于执行 `call` 语句而被管理的调用堆栈。

### 描述

当程序在调用堆栈存在时执行 `end` 语句，程序执行将返回到执行 `call` 语句的位置并继续运行。  
但是，当执行 `cycle_end` 语句时，所有管理的调用堆栈都会被清除。因此，程序不会返回到 `call` 语句的位置，而是停止执行。

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
# 10.1.12 `speed_out` 语句

`speed_out` 语句是一个过程，用于计算与机器人的当前运动速度成正比的值，并将结果分配给指定的变量。  
它仅在执行 `移动 (move)` 语句时运行，且插值设置为 ` (L)` 或 `C按钮 (C)`。

### 描述

此语句计算与机器人的当前移动速度成正比的值，并将计算结果存储在指定变量中。  

如果执行以下命令，如图所示，计算出与当前机器人速度 ` (x)` 对应的值 ` (y)`，并将其分配给 dow10。
...  
```python
speed_out on,min_spd=100,max_spd=2000,min_val=10,max_val=100,var=dow10
```

![](../../_assets/speed_out.png)

### 语法
```python
speed_out <on/off>, min_spd=<最低速度>, max_spd=<最高速度>, min_val=<最小值>, max_val=<最大值>, var=<数值变量>
```

### 参数
| 项目    | 描述                                                        | 备注              |
| ------- | ------------------------------------------------------------ | ------------------ |
| on/off  | 指定函数启用的部分                                          |                    |
| min_spd | 指定最小机器人移动速度 [mm/s]                              |                    |
| max_spd | 指定最大机器人移动速度 [mm/s]                              |                    |
| min_val | 指定与最小机器人速度对应的值                              |                    |
| max_val | 指定与最大机器人速度对应的值                              |                    |
| var     | 指定存储计算值的变量                                        | 数值变量           |

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

`任务 (task)` 语句是一种用于执行多任务功能的过程。  
有关 `任务 (task)` 语句的详细信息，请参阅以下链接：  
[${cont_model} 控制器功能手册 - 多任务](https://hrbook-hrc.web.app/#/view/doc-multi-task/zh/README?cont_model=${cont_model})  

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

`toolchng` 语句是用于更改分配给附加轴的伺服工具的过程。  
有关 `toolchng` 语句的详细信息，请参阅以下链接：  
[${cont_model} 机器人控制器功能手册 - 伺服工具更换](https://hrbook-hrc.web.app/#/view/doc-svtool-change/zh/README?cont_model=${cont_model})

### 语法

```python
toolchng on/off, tg=<change target>, di=<connection complete signal>, wait=<waiting time>
```
[__SOURCE](10-etc/1-proc/15-json_parse.md)
# 10.1.15 `json_parse`

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
    <td style="text-align:left">JSON 字符串仍在被解析中。数据尚不可用。</td>
  </tr>
  <tr>
    <td style="text-align:left">finished</td>
    <td style="text-align:left">JSON 字符串解析完成。数据现在可以使用。</td>
  </tr>
  </tbody>
</table>



### Examples
```python
    json_parse "[1, 2, 3, 4]"
    var r = result()
    wait r.status == "finished", 10 # 等待进程完成，最大超时为 10 秒。
    var jr = r.data   # r.data 的类型为 array
    print jr          # [1, 2, 3, 4] 打印
```

```python
    json_parse "3.141592"
    var r = result()
    wait r.status == "finished", 10 # 等待进程完成，最大超时为 10 秒。
    var jr = r.data    # r.data 的类型为 double
    print jr           # 3.141592 打印
```
```python
    json_parse "{\"test\": \"value\"}" # 双引号必须在 JSON 字符串中进行转义。
    var r = result()
    wait r.status == "finished", 10 # 等待进程完成，最大超时为 10 秒。
    var jr = r.data    # r.data 的类型为 JObject
    print jr           # { _type: "JObject", _sub_file: "", _desc: "", test: "value" } 打印
```
[__SOURCE](10-etc/1-proc/16-brake_check.md)
# 10.1.16 `brake_check`

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
* 请勿在产品运行时进入操作区域或触碰机器人。存在受伤的风险。
{% endhint %}

{% hint style="info" %}
* 仅支持配备气弹簧的机器人
* 为了准确估算，在使用此功能之前必须先进行 [Axis add weight setting](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/7-system/4-robot-parameter/7-axis-add-weight/README?cont_model=${cont_model}) 和 [Load estimation function](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/7-system/7-auto-calibration/3-load-estimation?cont_model=${cont_model})。
* 有关刹车检查监控功能的详细描述，请参阅下面的链接。
[](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/6-monitoring/4-system/2-system-diagnosis/1-brake-check?cont_model=${cont_model})
{% endhint %}
[__SOURCE](10-etc/2-func/README.md)
# 10.2 其他功能
[__SOURCE](10-etc/2-func/1-rducs.md)
# 10.2.1 `rducs` - 用户坐标系

### 描述

读取生成的用户坐标系作为姿态的功能。

- 将创建的用户坐标系的位置/方向复制到其姿态值中。
- 如果未创建或参数无效，将以错误中断作业执行。

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
        背景执行的结果<br>
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
        确定
      </td>
      <td></td>
    </tr>  
  </tbody>
</table>

### 错误

- E14613 : 当实际参数与形式参数不匹配时发生。检查实际参数。
- E14614 : 当用户坐标编号不是数字时发生。请重新指定用户坐标编号。
- E14615 : 当用户坐标编号不在1到20之间时发生。请更改用户坐标编号。
- E1336 : 如果这是未注册的用户坐标编号，则发生。请更改用户坐标编号。

### 示例

```python
   var p_uc2=Pose(0,0,0,0,0,0,"base")
   var res=rducs(2,p_uc2)
   end
```
[__SOURCE](10-etc/2-func/2-segment.md)
# 10.2.2 `segment`

`segment` 是将起始位置和结束位置之间的距离均匀划分的函数。

### 描述

将函数因子之间的距离均匀划分，并根据指定计数器存储与位置和姿态相关的姿态值到姿态变量中。
![](../../_assets/image_segment_1.png)

例如，如果 `P3=segment(P1,P2,3,2)`，将 `P1` 起始位置到 `P2` 目标位置之间的距离划分为 3 个相等部分，并将第 2 个姿态的位姿和旋转值存储到 `P3` 姿态变量中。

当你将途经位置作为函数的参数添加时，由起始位置、途经点和目标位置组成的弧上的距离被均匀划分，位姿和旋转的姿态值被存储在姿态变量中。

![](../../_assets/image_segment_2.png)

例如，如果 `P10=segment (P1,P2,P3,4,2)`，则由 `P1` 起始姿态和 `P2` 途经姿态 `P3` 目标姿态组成的弧上的距离被划分为 4 个相等部分，指定的第 2 个姿态的位姿和旋转值被存储到 `P10` 姿态变量中。

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
        起始姿态
      </td>
      <td style="text-align:left">姿态表达</td>
    </tr>
    <tr>
      <td style="text-align:left">via pose</td>
      <td style="text-align:left">
        途经姿态
      <td style="text-align:left">姿态表达</td>
    </tr>
    <tr>
      <td style="text-align:left">end pose</td>
      <td style="text-align:left">
        结束姿态
      </td>
      <td style="text-align:left">姿态表达</td>
    </tr>
    <tr>
      <td style="text-align:left">division number</td>
      <td style="text-align:left">
        划分数量<br>
        (1 ~ 30000)
      </td>
      <td style="text-align:left">算术表达</td>
    </tr>
    <tr>
      <td style="text-align:left">counter</td>
      <td style="text-align:left">
        要存储的姿态计数器编号<br>
        (0 ~ 300000, 0: 起始姿态)
      </td>
      <td style="text-align:left">算术表达</td>
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
     po2=Pose(1500.000,500.000,1938.000,0.000,0.000,0.000) # 途经姿态
     po3=Pose(2000.000,0.000,1938.000,0.000,0.000,0.000) # 结束姿态
     po10=segment(po1,po2,po3,5,3)
     end
```
[__SOURCE](10-etc/2-func/3-intersection.md)
# 10.2.3 `intersection`

您可以使用 `intersection` 函数找到与直线以最短距离相交的点，或查找通过的直线与另一条直线的最短距离相交。

### 描述

如果您指定两点形成一条直线和另一点作为参数，您将获得一条连接直线和一个点的交叉位置，且该位置的距离最短。

![](../../_assets/image_intersection_1.png)

如果您指定两点形成一条直线和两点形成另一条直线作为参数，您可以找到这两条直线的最短距离交点。交点是您指定的第一条直线的交点。

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
      <td style="text-align:left">姿态表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">straight-line ref.pose 2</td>
      <td style="text-align:left">
        第一条直线的第二个参考姿态
      <td style="text-align:left">姿态表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">position ref.pose</td>
      <td style="text-align:left">
        用于查找直线和最短距离位置的姿态
      </td>
      <td style="text-align:left">姿态表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">straight-line ref.pose 3</td>
      <td style="text-align:left">
        第二条直线的第一个参考姿态
      </td>
      <td style="text-align:left">姿态表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">straight-line ref.pose 4</td>
      <td style="text-align:left">
        第二条直线的第二个参考姿态
      </td>
      <td style="text-align:left">姿态表达式</td>
    </tr>
  </tbody>
</table>

### 示例

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
# 10.2.4 `rand`

您可以使用 `rand` 函数生成随机数。

### 描述
根据函数的参数，它生成介于 0 和 1 之间的随机实数或在指定范围内的随机整数。

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
      <td style="text-align:left">input/output signal</td>
      <td style="text-align:left">
        输入/输出信号变量名
      </td>
      <td style="text-align:left">输入/输出信号变量</td>
    </tr>
    <tr>
      <td style="text-align:left">number of bits</td>
      <td style="text-align:left">
        从输入/输出信号读取的位数
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
[__SOURCE](10-etc/2-func/6-sigout.md)
# 10.2.6 `sigout`

使用 `sigout` 函数时，您可以通过将其指定为 `int` 类型值来输出输出信号的特定范围。

支持版本： V70.02-00

### 描述
- 输入要用作起始的输出信号名称。
- 设置要输出的位数。
- 设置要输出的值。

### 语法

```python
result=sigout(<output signal>,<number of bits>,<output value>)
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
      <td style="text-align:left">output signal</td>
      <td style="text-align:left">
        输出信号变量名称 (bit)
      </td>
      <td style="text-align:left">输出信号变量</td>
    </tr>
    <tr>
      <td style="text-align:left">number of bits</td>
      <td style="text-align:left">
        要输出的信号的位数
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">output value</td>
      <td style="text-align:left">
        要输出的值
      <td style="text-align:left">变量</td>
    </tr>
  </tbody>
</table>

### 示例

```python
     var result1,result2,result3
     result1=sigout(do4,4,7)
     result2=sigout(fb2.do0,2,2)
     result3=sigout(fn1.do24,8,55)
     end
```
[__SOURCE](10-etc/3-sysvar/README.md)
# 10.3 系统变量
[__SOURCE](10-etc/3-sysvar/_acc_rate.md)
# `_acc_rate`

获取或设置速度轮廓中的加速度。

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
   # 打印当前的加速度率，并设置为70%。
   print _acc_rate
   _acc_rate=70
   ...
   end
```
[__SOURCE](10-etc/3-sysvar/_dec_rate.md)
# `_dec_rate`

获取或设置速度配置中的减速率。

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
   # 打印当前减速率，并设置为70%。
   print _dec_rate
   _dec_rate=70
   ...
   end
```
[__SOURCE](10-etc/3-sysvar/_intr_no.md)
# `_intr.no`

`_intr.no`系统变量是发生的中断编号。

### Description

当因为`intr_def`过程中的条件表达式满足而发生中断时，您可以使用`_intr.no`来确定程序是由哪个中断编号调用的。

### Syntax

```python
var res
res = _intr.no
```

### Sample

```python
   ...
   if _intr.no==1  # 如果发生中断编号 1
   print "通过传感器 1 激活，发生中断。"
   else if _intr.no==2 # 如果发生中断编号 2
   print "通过传感器 2 激活，发生中断。"
   stop # robot stops
   endif
   ...
   end
```
[__SOURCE](10-etc/3-sysvar/_intr_target.md)
# `_intr.target`

`_intr.target` 系统变量调整机器人的目标位置到达状态。


### Description

在移动语句中，这用于在移动时发生中断时调整位置，并在调用程序执行结束后返回到上一个程序的位置。


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
# `_spd_rate`

获取或设置播放速度。

### Description

与 cond.set 相同的设置 - 播放速度。

- 单位 : %
- 范围 : 1 到 100
- 默认值 : 100

### Syntax

```python
var res
res = _spd_rate
```

### Sample

```python
   ...
   # 如果播放速度小于 50%，提高到 100%。
   if _spd_rate<50
     _spd_rate=100
   ...
   end
```
[__SOURCE](10-etc/3-sysvar/_task_enable.md)
# `_task.enable`

### Description

一个系统变量，用于确定子任务是否处于活动状态。

### Syntax

```python
var res
res = _task[1].enable
```

### Sample

```python
   ...
   if _task[1].enable==1  # 如果子任务 1 活动
   print "子任务 1 活动"
   endif
   ...
   end
```
[__SOURCE](10-etc/3-sysvar/_tool.md)
# `_tool`

`_tool` 是一个系统变量，用于读取或更改工具数据。

### 描述

- 读取注册的工具数据（重量/质心/转动惯量）或更改工具数据。
- 如果工具数据未注册或成员无效，则会发生错误并中断作业执行。

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

- E14550 : 当工具数据的成员无效时发生。确保设置的工具数据的成员是质量、cx、cy、cz、ixx、iyy、izz。
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

读取或设置电机在控制额外轴时旋转的速度。

### Description

额外轴必须在夹具轴上设置为速度控制模式。<br>
单位是 rpm。您可以设置一个介于 -10000 和 10000 之间的值，默认值为 0。<br>
如果指定为 -，电机将反向旋转。

### Syntax

```python
var res
_vel_rpm_cmd[6] = 1000 # 以 1000 rpm 的速度旋转 7 轴电机 
res = _vel_rpm_cmd[6] # 赋值 7 轴电机的旋转速度 
```

### Sample

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

### Description

`_weaving` 用于更改当前选择的编织条件。

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
         编织类型 (0=单振动, 1=三角形, 2=L形, 3=圆形)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">frequency</td>
      <td style="text-align:left">
        频率[Hz]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">left_distance</td>
      <td style="text-align:left">
        向左的距离[mm]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">right_distance</td>
      <td style="text-align:left">
        向右的距离[mm]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">angle</td>
      <td style="text-align:left">
        角度[deg]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">offset_angle</td>
      <td style="text-align:left">
        偏移角度[deg]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">wall_direction</td>
      <td style="text-align:left">
        墙面方向 (0=垂直, 1=水平, 2= torch 方向)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">forward_angle</td>
      <td style="text-align:left">
        向前角度[deg]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">boundary_limit</td>
      <td style="text-align:left">
        边界限制 (0=有效, 1=无效)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">segment_time_1</td>
      <td style="text-align:left">
        段 (1~4) 移动时间[s]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">segment_delay_1</td>
      <td style="text-align:left">
        段 (1~4) 计时器(编织停止)[s]
      </td>
      <td style="text-align:left">variable</td>
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




### Sample

```python
   weaving on,cnd=1
   move P,spd=50%,accu=3,tool=1
   _weaving.frequency=5    # 将编织频率改为5Hz
   move P,spd=50%,accu=3,tool=1
   weaving off
   end
```
[__SOURCE](10-etc/3-sysvar/_pc.md)
# `_pc`

### Description

`_pc` 用于获取当前程序计数器信息。<br>
程序计数器由程序号、步骤号和功能号组成。

### Syntax

```python
var sno=_pc.cur_sno  # 分配当前步骤号
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
         光标当前所在的步骤号
      </td>
      <td style="text-align:left">变量</td>
    </tr>
  </tbody>
</table>




### `cur_sno` sample : 如果直到条件不满足，移动到上一个步骤。

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
[__SOURCE](10-etc/3-sysvar/_soft_limit.md)
# `_soft_limit`

读取或设置软件限制的值。

### Description

单位是线性轴的毫米和旋转轴的度数。您可以在指定的最小值和最大值范围内设置值。

### Syntax

```python
var res
res = _soft_limit[2].min
```

### Sample

```python
   ...
   # 将第一个轴的软件限制的最小值设置为 -90 度。
   print _soft_limit[0].min
   _soft_limit[0].min=-90
   ...
   end
```
[__SOURCE](10-etc/3-sysvar/_ax.md)
# `_ax`

用于通过轴名称读取轴索引。

### Description

轴索引是通过参考值0获得的。然而，如果轴不存在，则分配-1。指定跟随"_ax."的字符串作为轴名称。轴名称支持小写和大写字母。

支持版本 V70.02-00

### Syntax

```python
var res
res = _ax.v # 获取 V 轴索引
```

### Sample

```python
   ...
   # 打印 R1 轴的当前位置信息。
   global po
   po=cpo("joint")
   print po.j[_ax.R1]
   ...
   end
```
[__SOURCE](10-etc/3-sysvar/_total_ax.md)
# `_total_ax`

读取当前系统中的轴总数。

### Description

它不能作为赋值语句的左侧。

支持从 V70.02-00

### Syntax

```python
var res
res = _total_ax
```

### Sample

```python
   ...
   # 输出当前系统中的轴总数。
   print _total_ax
   ...
   end
```
[__SOURCE](10-etc/3-sysvar/_aux_ax.md)
# `_aux_ax`

读取当前系统中的辅助轴数量。

### Description

它不能作为赋值语句的左侧。

Supported from V70.02-00

### Syntax

```python
var res
res = _aux_ax
```

### Sample

```python
   ...
   # 输出当前系统中的辅助轴数量。
   print _aux_ax
   ...
   end
```
[__SOURCE](10-etc/3-sysvar/_mech_type.md)
# `_mech_type`

读取当前选择的机器人类型。

### Description

它不能作为赋值语句的左侧。

支持的版本为 V70.02-00

### Syntax

```python
var res
res = _mech_type
```

### Sample

```python
   ...
   # 打印当前的机器人类型。
   print _mech_type
   ...
   end
```