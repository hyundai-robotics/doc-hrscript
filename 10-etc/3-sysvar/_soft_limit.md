# `_soft_limit`

Reads or sets the value of the software limit.

### Description

The units are mm for the linear axis and degrees for the rotation axis. You can set the value within the minimum to maximum range specified for the robot.

### Syntax

```python
var res
res = _soft_limit[2].min
```

### Sample

```python
   ...
   # Set the minimum value of the software limit of the 1st axis to -90 degrees.
   print _soft_limit[0].min
   _soft_limit[0].min=-90
   ...
   end
```
