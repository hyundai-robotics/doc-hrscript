# `_triggout.w241_enable`

_triggout.w241_enable is a system variable used to enable or disable the warning message generated when the system fails to determine whether the signal was successfully output during the distance-based triggout command.

### Description

It can be set to 0 or 1, with a default value of 1. This is supported from version V70.04-00 onwards.

### Syntax

```python
_triggout.w241_enable=0
```

### Sample

```python
     # Disable warning output; the default value upon controller boot is 1.
     triggout.w241_enable=0
     
     print "warning mode = ",_triggout.w241_enable
     
     var cmd_dist=-20
     do20=0
     
S1   move P,spd=30%,accu=0,tool=0  
     delay 1
S2   move P,spd=cmd_spd%,accu=cmd_acc,tool=0 
     
     #---------------------------
     triggout do20,val=1,dist=cmd_dist,j=5
     #---------------------------
     
S3   move P,spd=cmd_spd%,accu=cmd_acc,tool=0  
S4   move P,spd=cmd_spd%,accu=cmd_acc,tool=0  
     delay 1
     end
```
