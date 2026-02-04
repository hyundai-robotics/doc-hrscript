# 5.21 shift_lim

The `shift_lim` statement is a function that improves safety when using the shift feature by setting the maximum allowable shift amount for the robot.  
If a shift value exceeding the configured limit is entered, an error is generated.

### Syntax
```python
shift_lim x=<X shift limit>, y=<Y shift limit>, z=<Z shift limit>
```

### Parameters
* x, y, z: X, Y, Z shift limit values[0~3000,mm]<br><br>

### Error Guide
* E1196: The shift amount exceeds the configured shift limit. Reduce the shift amount or readjust the shift limit value.

### Example
```python
     var po1 = Pose(0.691, 99.293, 24.758, -6.528, -48.574, 15.774, 0.000)
S1   move P, tg=po1, spd=10%, accu=0, tool=0
     shift_lim x=120, x=200, z=100
     shift crd="base", x=-150, y=70, z=10  # Shift limit exceeded error occurs
S2   move P, tg=po1, spd=10%, accu=0, tool=0
     end
```