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