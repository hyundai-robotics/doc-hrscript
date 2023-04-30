# 10.1.6 typeof

`typeof` is the procedure for getting the type of a variable or an expression. The result is returned from the `result()` function.


### Syntax

```python
typeof <expression>
```


### Sample

```python
     global done=true,msg="Timeout Error"
     var a=-2000, b=3.14
     var myarr=[1,2,3]
     var myobj={x:30, y:"off"}
     var po=Pose(0,90,0,0,0,0)

     typeof done
     print result() # "bool" 
     typeof msg
     print result() # "string"
     typeof a
     print result() # "int"
     typeof b
     print result() # "double"
     typeof myarr
     print result() # "array"
     typeof myobj
     print result() # "object"
     typeof po
     print result() # "object"
     end
```
