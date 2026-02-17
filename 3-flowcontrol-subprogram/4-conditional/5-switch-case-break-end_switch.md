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
