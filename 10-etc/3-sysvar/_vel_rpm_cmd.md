# `_vel_rpm_cmd`

Reads or sets the speed at which the motor rotates when controlling speed for an additional axis.

### Description

The additional axis must be set to speed control mode on the jig axis.<br>
The unit is rpm. You can set a value between -10000 and 10000, and the default value is 0. <br>
If specified as -, the motor rotates in reverse.

### Syntax

```python
var res
_vel_rpm_cmd[6] = 1000 # Rotate the 7-axis motor at 1000 rpm 
res = _vel_rpm_cmd[6] # Assign the rotation speed of the 7-axis motor 
```

### Sample

```python
   ...
   # After print the current 7-axis motor rotation speed, set it to 1000 rpm.
   print _vel_rpm_cmd[6]
   _vel_rpm_cmd[6]=1000
   ...
   end
```
