# 3.4.5 switch-case-break-end\_switch

### Description

A **switch** statement evaluates a numeric expression and compares it with the resulting value of the numeric expression designated by a **case** statement. It is executed from the **case** statement of equal value until a **break** statement is encountered.

In the following example, if the resulting value of Expression X is equal to the resulting value of Expression B1 or B2, \(1\) through \(3\) will be executed, and it will move to the point of the **end\_switch** statement \(note that there is no **break** below the command statement B\). Meanwhile, if the resulting value of Expression X is equal to that of Expression C, \(2\) through \(3\) will be executed.

If the resulting value of Expression X is not equal to that of any **case** statement, it will be moved to the **default**, and \(4\) through \(5\) will be executed. Then, the **default** section may be omitted.

### Syntax

```python
switch <expression X>
case <expression A>
	<statement A>
	…
	break
case <expression B1>
case <expression B2>
	<statement B>	… (1)
case <expression C>
	<statement C>	… (2)
	…
	break		… (3)
default
	<statement N>	… (4)
	…
	break		… (5)
end_switch
```

Any expressions such as Boolean, numeric, string  constant, parameter, and numeric, are permissible.

### Example

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

