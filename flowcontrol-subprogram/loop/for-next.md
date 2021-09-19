# 3.6.1 for-next

### Description

The format of the for-next statement, which repeats the same operation, is as follows.

First, the initial value will be assigned to the index variable. When the next statement is encountered while the statements under the for statement are executed, the index variable will add increment/decrement values and perform repetition from the point of the for statement. When the index variable passes the end value, the repetition will end.

If a step is not specified, 1 will be applied.

### Syntax

```python
for <index variable>=<initial value> to <end value> [step <increment/decrement value>]
	<statement>
	…
next
```

### Example

The following shows an example of a routine that accumulates 1 to 10 in the sum using the for-next statement. When the repetition is over, 11 and 55 will be printed on the screen.

```python
var idx
var sum=0
for idx=1 to 10
	sum=sum+idx
next
print idx, sum
end
```

