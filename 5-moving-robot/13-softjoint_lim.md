# 5.13 softjoint_lim

Before using instruction "softjoint on", user should set softjoint_lim  parameters such as joint number(j), compliance(sft), joint angle limit(ang) and torque threshold(thr). <br>

--- 

### Syntax 
```python
softjoint_lim, j=<joint number>, sft=<softness>, ang=<joint angle limit>, thr=<torque threshold> 
```

### Parameter
* j : joint number [1~6]
* sft : larger value is more soft to move [0:off,0~100]
* ang : joint angle limit [deg]
* thr : torque threshold [Nm]


### Example 
> Example1) setting parameters on joint number 3(J3) 
> * Activation on J3, softness(50), joint angle limit [-30~30] (deg) and torque threshold 10(Nm)   
```python
softjoint_lim, j=3, sft=50, ang=30, thr=10
```

> Example2) setting parameters on joint number 2 and 3(J2, J3)
> * Setting softness : J2-sft(30), J3-sft(80)  
> * Setting joint angle limit : J2[-50,+50] (deg), J3[min joint angle limit, max joint angle limit] (deg) <br>
> * Setting torque threshold : J2-thr(3)(Nm), J3-thr(5)(Nm) 


```python
S1   move P,spd=100mm/sec,accu=0,tool=0
     delay 2.0 
     softjoint_lim j=2,sft=30,ang=50,thr=3
     softjoint_lim j=3,sft=80,thr=5
     softjoint on
S2   move P,spd=250mm/sec,accu=0,tool=0
     softjoint off 
     end 
```


--- 
{% hint style="info" %}

* For using the function of softjoint, parameters on "j" and "sft" on softjoint_lim should be set. Also, if you do not set "ang" parameter, robot moves in workspace on defined softlimit. And, default parameter value on torque threshold "thr" is 0 [Nm]. 

{% endhint %}
