# 5.10 softxyz 


The softxyz function is a sensorless force-control feature that allows the robot  
to move flexibly in Cartesian space in response to external forces under user-defined conditions.

To ensure proper operation, **tool data and additional payload information must be configured correctly**.

---

## ⚠️ Caution

Since the softxyz function is **sensorless** and does not use a force sensor,  
there are **inherent limitations** in achieving fully smooth and natural motion.

However, by tuning the `softxyz_lim` values appropriately for the application environment,  
you can achieve the smoothest possible motion within the functional limitations.

Because `softxyz_lim (pos / xnr / vel / thr)` directly determines how the robot responds to external force,  
**fine-tuning is required** depending on the environment, assembly process, and tool stiffness.

---

### Description
* A function that allows the robot to be displaced in a Cartesian coordinate system by external force without using a force sensor.

---

### Syntax
```python
softxyz on, crd=<reference_coordinate>
softxyz set, dpr=<stiffness>
softxyz off
```

### Parameter 
* on : function start, off : function end  
* crd : coordinates (base, robot, tool, user)
```python
softxyz on, crd="base"   
softxyz on, crd="robot"  
softxyz on, crd="tool"   
softxyz on, crd="user_1"  
softxyz off  
```


### Example 
> Example 1) In case that robot move toward X, Y, Ry for assembling Z direction 
> * Coordinate : robot coordinate (crd="robot") <br>
> * Position (xnr) limit : the range of X and Y direction [-50,+50](mm), the range of Ry direction [-3,+3] (deg) <br>
> * Velocity (vel) limit : the maximum speed of X and Y direction 5(mm/sec), the maximum speed of Ry 3(deg/sec)  <br>
> * Torque (thr) limit : the threshold of X direction 3N, that of Y direction 3N and that of Ry direction 1Nm 

```python
S1   move P,spd=100mm/sec,accu=0,tool=0
     delay 2.0 # before softxyz on  
     softxyz_lim xnr, x=50, y=50, ry=3
     softxyz_lim vel, x=5, y=5, ry=3
     softxyz_lim thr, x=3, y=3, ry=1
     softxyz on, crd="robot"
S2   move P,spd=250mm/sec,accu=0,tool=0
     softxyz off 
     end 
```

> Example 2) Injection materials handling 
> * Coordinate : robot coordinate (crd="robot") <br>
> * Position (pos) limit : the range of +Y direction [0,3]  
(mm) , the range of -Y direction [-200,0] (mm) <br>
> * Velocity (vel) limit : the maximum speed of Y direction 150(mm/sec)<br>


```python
S1   move P,spd=100mm/sec,accu=0,tool=0
     delay 2.0 # before softxyz on  
     softxyz_lim pos, _y=300, y_=200
     softxyz_lim vel, y=150
     softxyz on, crd="robot"
S2   wait ... 
     softxyz off 
     end 
```

--- 
{% hint style="info" %}

* Before using "softxyz on", user should set softxyz_lim parameters such as pos, xnr, vel and thr. 

* For upgrading sensorless force control performance, user should set "delay" command as "delay 1.0" befor "softxyz on". 

{% endhint %}
