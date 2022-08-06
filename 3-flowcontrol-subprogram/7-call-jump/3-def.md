# 3.7.3 def (defining user function)

since V60.05-06

### Description

You can define user functions in the job with **def** statement and call it with **call** statement. Similar to **param** statement, **def** statement can specify a list of formal parameters. The actual parameter values of the **call** statement are passed to the formal parameters.
The execution of a function defined by **def** statement returns to the next statement after the **call** statement when executing **return** statement or **end** statement

User functions are called by name rather than number, so its readability is better than sub-program. And you can group multiple related functions into one subprogram to make your project structure better.


### Syntax

```python
def <user function name> [,parameter1[=default value],parameter2[=default value],...]
```

Specify the user function name after **def**. Function names must follow the rules defined in the section [2.2 Identifier](../../2-basic-syntax/2-identifier.md). In addition, it should be globally unique name. Be careful not to duplicate the new name with other function names or other variable names.
After that, specify the formal parameters. You can also specify a default value for each parameter. If you omit a actual parameter in the call statement, the formal parameter is initialized to the default value. If you start specifying a default value for a particular formal parameter, you must specify all paramters until last parameter.


```python
# examples of formal parameters default value
def set_work,mass,cx=0,cy=0,cz=0 # legal example
def set_work,mass,cx=0,cy,cz     # illegal example
```

### Example

Below are examples of user function calls with **call** statements and the results. We've presented the Euclidean distance example in the previous section to describe the subprogram. Now let's define user functions for Euclidean distance and Manhattan distance respectively and call them.


```python
# 0001_main.job
var x,y
x=5
y=12.8

call euclid_dist,x,y
var res=result()
print "euclid=",res # 13.7419

call manhattan_dist,x,y
var res=result()
print "manhattan=",res # 17.8
end
```

```python
# 0008_dist.job

# Calc. Euclide distance 2D
def euclid_dist,x,y
var tmp
tmp=x*x+y*y
var len=sqr(tmp) # distance from origin
return len

# Calc. Manhattan distance 2D
def manhattan_dist,x,y
var len=x+y
return len
```

<br>

RESULT
```python
euclid= 13.7419
manhattan= 17.8
end
```


