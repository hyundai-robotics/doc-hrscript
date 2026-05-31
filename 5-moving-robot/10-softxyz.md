# 5.10 `softxyz`


The `softxyz` function is a sensorless force-control feature that allows the robot to move flexibly in Cartesian space in response to external forces under user-defined conditions.

To ensure proper operation, `tool data and additional payload information must be configured correctly`.

{% hint style="warning" %}

Since the `softxyz` function is `sensorless` and does not use a force sensor,  
there are `inherent limitations` in achieving fully smooth and natural motion.

However, by tuning the `softxyz_lim` values appropriately for the application environment,  
you can achieve the smoothest possible motion within the functional limitations.

Because `softxyz_lim (pos / xnr / vel / thr)` directly determines how the robot responds to external force,  
`fine-tuning is required` depending on the environment, assembly process, and tool stiffness.

{% endhint %}

### Description
* A function that allows the robot to be displaced in a Cartesian coordinate system by external force without using a force sensor.

---

### Syntax
```python
softxyz on, crd=<reference_coordinate>
softxyz set, dpr=<stiffness>
softxyz off
```

### Parameters
- `on` : Start the softxyz function  
- `off` : Stop the softxyz function  
- `set` : Modify softxyz settings  

- `crd` : Reference coordinate system for external-force displacement  
  - Available options: `base`, `robot`, `tool`, `user_x`

- `dpr` : Stiffness value  
  - Range: `0.0 ~ 2.0`  
  - Higher values = `stiffer`, less displacement under external force  
  - Default: `1.0`

```python
softxyz on,  crd="base"     # Based on the base coordinate system
softxyz on,  crd="robot"    # Based on the robot coordinate system
softxyz on,  crd="tool"     # Based on the tool coordinate system
softxyz on,  crd="user_1"   # User-defined coordinate system #1

softxyz set, dpr=1.0        # Set stiffness (0.0~2.0, higher = stiffer)
softxyz off                 # Disable the softxyz function
```


### Example 
> Example 1) Assembly along the Z-direction while allowing displacement in X, Y, and Ry
> * Coordinate : robot coordinate (crd="robot") <br>
> * Position (xnr) limit : the range of X and Y direction [-50,+50] (mm), the range of Ry direction [-3,+3] (deg) <br>
> * Velocity (vel) limit : the maximum speed of X and Y direction 5(mm/sec), the maximum speed of Ry 3(deg/sec)  <br>
> * Torque (thr) limit : the threshold of X direction 3N, that of Y direction 3N and that of Ry direction 1Nm 

```python
S1   move P,spd=100mm/sec,accu=0,tool=0
     delay 2.0   # Required before enabling softxyz
     softxyz_lim xnr, x=50, y=50, ry=3
     softxyz_lim vel, x=5, y=5, ry=3
     softxyz_lim thr, x=20, y=20, ry=3
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
     delay 2.0   # Required before enabling softxyz
     softxyz_lim pos, _y=300, y_=200
     softxyz_lim vel, y=150
     softxyz on, crd="robot"

S2   wait ...
     softxyz off
     end
```

--- 
> `Information`
>
> - Before using `softxyz on`, you `must` configure the `softxyz_lim` parameters  
>   (`pos`, `xnr`, `vel`, `thr`) to set the maximum displacement, speed,  
>   and Cartesian threshold values.
>
> - To improve sensitivity to external force, it is recommended to  
>   `keep the robot stationary for 1-2 seconds using the `delay` command`  
>   before executing `softxyz on`.
>
> - If vibration occurs during softxyz operation, the following adjustments are recommended:
>   1) *Increase the `thr` value*  
>   2) *Increase the `dpr` value*  
>   3) *Decrease the `vel` value*