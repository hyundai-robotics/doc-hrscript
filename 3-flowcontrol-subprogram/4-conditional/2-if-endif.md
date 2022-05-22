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

