# 5.9 colsense 

Robot language "colsense" is used for setting detection sensitivity in case of the function activated on. 

Users should set the function activation on/off and detection sensitivity in the TP menu. \[3: robot parameter &gt; 14: impact detection &gt; 1: Model-based collision detection \] 

--- 

### Description
* General collision detection sensitivity can be set
* Each axis collision detection sensitivity can be set 

### Syntax 
```python
colsense general,sensitivity=<general sensitivity>  
colsense axis,id=<joint number>,criteria=<each axis sensitivity> 
```

### Parameter 
* General threshold value can be set from 0 to 200, and larger value is more sensitive.(0:0ff,1~200)
* The parameter "id" is set as joint number.(1~6)  
* Axis threshold value can be set from 0 to 100, and lower value is more sensitive.(0:0ff,1~100)"

### Example 

```python
S1   move P,spd=60%,accu=0,tool=0
S2   move P,spd=60%,accu=0,tool=0
     colsense general,sensitivity=150
S3   move P,spd=60%,accu=0,tool=0
     colsense general,sensitivity=200
S4   move P,spd=60%,accu=0,tool=0
S5   move P,spd=60%,accu=0,tool=0
     colsense axis,id=1,criteria=0
     colsense axis,id=2,criteria=0
S6   move P,spd=60%,accu=0,tool=0
S7   move P,spd=60%,accu=0,tool=0
     end 
```
* The detection sensitivity value in step1 and step2 is used from setting based on the menu \[3: robot parameter &gt; 14: impact detection &gt; 1: Model-based collision detection \] 
* The General sensitivity in step3 is 150, and the value is changed as 200 in step4 and step5 
* Sensing collision on joint1 and joint2 is deactivated, and other joints collision are detected by general sensitivity as 200.  

--- 
{% hint style="info" %}

The final sensitivity value per axis is proportional to the sensitivity value of each axis, and inversely proportional to the general sensitivity value. 
{% endhint %}


