# 10.3.3 _tool

`_tool` is a system variable for reading or changing tool data.


### Description

- Read the registered tool data (weight/center of mass/inertia) or change the tool data.
- If the tool data is not registered or if the member is not valid, an error occurs and the job execution is interrupted.


### Syntax

```python
<shift variable> = _tool3
_tool3 = <shift>
_tool[3] = <shift>
_tool[5].mass = <arithmetic expression>
_tool[5].cx = <arithmetic expression>
_tool[5].cy = <arithmetic expression>
_tool[5].cz = <arithmetic expression>
_tool[5].ixx = <arithmetic expression>
_tool[5].iyy = <arithmetic expression>
_tool[5].izz = <arithmetic expression>
```


### Errors

- E14550 : Occurs when the member of the tool data is not valid. Make sure that the members of the set tool data are mass, cx, cy, cz, ixx, iyy, izz.
- E14286 : Occurs when the right side of the assignment statement is not a shift type or when the member of the tool variable is not valid. Please specify the right side correctly.


### Sample

```python
   var sft=Shift(100,20,30,0,0,0,"tool")
   _tool3=sft
   move L,spd=30%,accu=1,tool=3
   end
```
