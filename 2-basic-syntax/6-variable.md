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