# 3.6.2 break, continue

### Description

The `break` and `continue` are used between `for`~`next` statements explained in this previous section.

- When run into `break` in the `for`~`next` block, the loop stops its repetition and branch to the `next` statement.
- When run into `continue` in the `for`~`next` block, it doesn't proceed to the next statement, but does an increment/decrement of the index variable, and branch to the `for` statement.

### Syntax

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

### Example

This is an example of outputting all the names in the array using the `for`~`next` statement, except for names with more than 5 characters, but stopping when an empty string is encountered.

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

Result

```python
Anna
James
Tom
```
