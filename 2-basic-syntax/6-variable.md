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