# 3.7.2 Parameters and param, return

In a job program, formal parameters are used as channels through which input and output are passed. The **param** statement will define formal parameters at the beginning of the job program.

In the following example, job no. 105 is named as "dist2d" as it is a subjob that acquires the Euclidean distance from the origin to the coordinate value \(x, y\) and returns it to len.

```python
# 0001_main.job
var x,y
x=5
y=12.8
call 105_dist2d,x,y
var res=result()
print res
end
```

```python
# 0105_dist2d.job
# Calc. Euclide distance 2D
param x,y
var tmp

tmp=x*x+y*y
var len=sqr(tmp) # distance from origin
return len
```

<br>

RESULT
```python
13.742
```

In job no. 1, the dist2d subprogram is called with the **call** statement, and "x, y," which are local variables, are passed. In the dist2d subprogram, "ldX", and "ldY" defined with the **param** statement are called "formal parameters", and "x, y" passed to the **call** statement are called "actual parameters."

The dist2d program transports resulting values to external destinations through **return** statements. Returned values can be obtained by calling a result\(\) function in the called program.

(A **return** statement and an **end** statement have the same action as they end a called program and return to the main program. However, a **return** statement is different from **end** statement as the former can designate a resulting value as an element).
