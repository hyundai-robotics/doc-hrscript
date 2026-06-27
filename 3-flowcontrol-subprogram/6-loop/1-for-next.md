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