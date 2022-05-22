# 2.6 Variables

A variable can store values and has an identifier name. Variables are divided into global and local variables, and the difference between them will be described later. Examples of local variables are first described here.



Variables can be created with the var command, as shown in the following. This is called defining a variable. Multiple identifiers can be created at once by enumerating multiple identifiers after the var command.



```python
var myvar
var width, height, depth
```

Storing a value in a variable is called “assignment.” The assignment may be performed while defining or after defining a variable. If the assignment is not performed while defining, the variable will have a number value of 0 by default.

```python
var myvar=0
var message, width=200
message="Invalid input value"
```

In HRScript, \(=\) does not mean equal. It is used as an assignment operator and means that the value on the operator’s right side is assigned to the variable on the left side. The value stored in the variable may be printed through the print statement.

```python
var myvar=0
var message, width=200
message="Invalid input value"
print width, message
```

A different value may be assigned to a variable to which a value has already been assigned. It is called a variable because its value can change.

```python
var width=200
width=300
```



