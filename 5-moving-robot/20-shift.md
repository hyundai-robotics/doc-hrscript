# 5.20 `shift`

### Description
The `shift` statement translates an already taught point in the XYZ coordinate system while maintaining the tool orientation (tool angles).

### Syntax
```python
shift crd=<reference coordinate>,x=<X shift value>,y=<Y shift value>,z=<Z shift value>
```

### Parameters
* crd : Reference coordinate system
["base": base, "robot": robot, "tool": tool, "joint": joint, "u": user]
* x, y, z : X, Y, Z shift values [0-3000, mm]

### Example
```python
     var po1=Pose(0.691,99.293,24.758,-6.528,-48.574,15.774,0.000)
S1   move P,tg=po1,spd=10%,accu=0,tool=0
     shift crd="base",x=200,z=100
S2   move P,tg=po1,spd=10%,accu=0,tool=0
     shift crd="u1",x=-150,y=70,z=10
S3   move P,tg=po1,spd=10%,accu=0,tool=0
     end
```