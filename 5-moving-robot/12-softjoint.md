# 5.12 softjoint

softjoint instruction is sensorless force control, that allows the robot to move compliantly in joint space with respect to external forces in the environment set by the user. <br>

User should check the validity of robot tool and additional axis information for increasing function accuracy. <br>



--- 

### Description 
* Without using sensor, move compliantly in joint space with respect to external forces in the environment set by the user. 


### Syntax 
```python
softjoint on
softjoint off  
```

### Parameter
* on : function start
* off : function end 



--- 
{% hint style="info" %}

* Before using "softjoint on", user should set softjoint_lim parameters such as joint number(j), softness(sft), joint angle limit(ang) and torque threshold(thr).

* For upgrading sensorless force control performance, user should set "delay" command as "delay 1.0" befor "softjoint on".  

{% endhint %}
