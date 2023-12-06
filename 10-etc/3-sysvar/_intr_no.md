# 10.3.1 _intr.no

`_intr.no` system variable is the occured interrupt number.

### Description

When an interrupt occurs because the conditional expression in the `intr_def` procedure is satisfied, you can use `_intr.no` to determine by which interrupt number the program is called.


### Syntax

```python
var res
res = _intr.no
```


### Sample

```python
   ...
   if _intr.no==1  # If interrupt number 1 occures
   print "By sensor 1 activation, interrupt occures."
   else if _intr.no==2 # If interrupt number 2 occures
   print "By sensor 2 activation, interrupt occures."
   stop # robot stops
   endif
   ...
   end
```


