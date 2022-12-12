# 8. Alias

Alias is a name that can be used as an alternative to the notation of a variable or a property of an object.

Alias is an alternative name can be used to notate a variable or object. You can replace property notations that are too long to be repeated with concise names, or replace IO variables at specific indexes with more readable names.

An alias is defined with the **alias** statement, and the syntax is almost identical to that of **var** or **global**.

The scope of an alias is the same as global. That is, after the alias statement is executed, it can be used in any subsequent job, and is not destroyed even if the program cycle is reset by the end statement of the main program or the R0 \[ENTER\] operation.

```python
global myval=3, yourname="Jane"
val i=0,msg="hello"
val profile = { name: "Paul", age: 43, role: [ "CTO", "engineer" ] }

alias grip=fb3.do4, work_no=fb1.diw2 # (1)
alias role=profile.role # (2)
alias tool0=project.robot.tools.t_0 # (3)

# usage
grip=1
print work_no
print role[1]
tool0.mass=12
```

In (1) of the above example, the output variable **fb3.do4** was defined as an alias named **grip**, and the input variable **fb1.diw2** was defined as an alias **work_no**.  
In (2), the role array which is an property of **profile**, is defined as alias **role**.  
In (3), the built-in object **project.robot.tools.t_0** is defined as alias **tool0**, which points to tool-data \#0.

For an alias refer to an array, its element can be specified with [ ] operator, like **role[1]**.  
For an alias refer to an object, its property can be specified with . operator, like **tool0.mass**.

A constant cannot be defined as an alias. Define it using **global** or **var**.  
Expression cannot be defined as alias, either. Be careful as it may cause malfunction.


```python
#alias pie=3.141592 # (X)
#alias unit="mm/s" # (X)
global pie=3.141592 # (O)
global unit="mm/s" # (O)

#alias pie_2 = pie*pie # (X)
```
