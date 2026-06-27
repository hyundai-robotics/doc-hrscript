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