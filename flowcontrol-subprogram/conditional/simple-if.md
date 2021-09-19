# 3.4.1 Single-Line if

### Description

The form of a single-line if statement is as follows: If &lt;Boolean expression&gt; is true, branching to &lt;address&gt; will occur. If false, moving to the next statement will occur.

### Syntax

```python
if <bool expression> then <address>
```

### Example

Below is an example of the single-line if statement. If the condition that pressure is greater than the limit is true, branching to the label address “\*err will occur,” making it possible to print a warning that the pressure is too high. If the condition is false, the next statement will be executed one after the other without branching, so “In normal operation ” will be printed, ending the program.

```python
var pressure=95, limit=90
if pressure > limit then *err
print "in normal operation."
end
*err
print "warning: pressure is too high."
```

