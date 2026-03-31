# `_ax`

It is used to read the axis index by the axis name.

### Description

The axis index is obtained with 0 based value. Specify the string following "_ax." as the axis name. Axis name supports both lowercase and uppercase.

### Syntax

```python
var res
res = _ax.v # Get V-axis index
```

### Sample

```python
   ...
   # Print the current position of the R1 axis.
   global po
   po=cpo("joint")
   print po.j[_ax.R1]
   ...
   end
```
