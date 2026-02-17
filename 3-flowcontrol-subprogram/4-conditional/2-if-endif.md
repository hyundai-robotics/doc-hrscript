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