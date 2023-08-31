# 5.8 coldet 

Robot language "coldet" is used for setting collision detection(of each axis) level in case of the function activated on. 

Users should set the function activation on/off and collision level in the TP menu. \[3: robot parameter &gt; 14: impact detection &gt; 2: set the collision detection(of each axis) \] 

The menu can be shown in that robot is set for detecting collision.  

If the function is activated on, default detecting level is 1. 

Also in manual mode, the default level is same. 

--- 

### Description
* Set the collision detection level 


### Syntax 
```python
coldet LV=<level> 
```

### Parameter 
* The value of level can be set from 0 to 16 (0: off)

### Example 

```python
S1   move P,spd=60%,accu=0,tool=0
S2   move P,spd=60%,accu=0,tool=0
     coldet LV=2
S3   move P,spd=60%,accu=0,tool=0
     coldet LV=3
S4   move P,spd=60%,accu=0,tool=0
S5   move P,spd=60%,accu=0,tool=0
     coldet LV=0
S6   move P,spd=60%,accu=0,tool=0
S7   move P,spd=60%,accu=0,tool=0
     end 
```
* The value of detecting level in step1 and step2 is 1. 
* The value of detecting level in step3 is 2, and that of level in step 4 and step5 is 3.
* In case of step6 and step7, the function of collision detection is deactivated. 
--- 
