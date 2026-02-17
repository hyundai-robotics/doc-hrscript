# 5.14 External control


### Description  
* The position command generation for the robot's movement is performed by an external device, and this generated external command is transmitted to the ${cont_model} controller as string data via ethernet or serial communication. The ${cont_model} controller receives this command and controls the robot. 

### Syntax 
```python
     global onl_trj
     var msg # Pose or Pose type string

     onl_trj=online.Traject()
     onl_trj.time_from_start=-1.0
     onl_trj.look_ahead_time=1.0
     onl_trj.interval=0.1
     onl_trj.init
     onl_trj.buf_in msg
 
```

### Parameter 
* `time_from_start` : elapsed time from start position (-1: disable)  
* `look_head_time` : time delay for robot moving (unit : [s])  
* `interval` : time interval between generated commands (unit : [s])  
* `init` : online trajectory init, clear command buffer  
* `buf_in`  : add pose or pose type string to the command buffer



### Example
> The robot moves by receiving commands generated externally via enet communication. 

```python
     import enet
     global enet0
     enet0=enet.ENet("tcp")
     enet0.ip_addr="192.168.1.213"
     enet0.lport=7000
     enet0.rport=7000
     var ret=enet0.open()
     ret=enet0.listen()
     ret=enet0.accept()

     global onl_trj
     onl_trj=online.Traject()
     onl_trj.time_from_start=-1.0
     onl_trj.look_ahead_time=1.0 # Delay time for robot movement start
     onl_trj.interval=0.1 # Sampling time of generated commands
     onl_trj.init # Buffer init

     var msg
10   enet0.recv
     str_pose=result()
      if msg == "stop"
       onl_trj.init # buffer clear (quick stop)
     else
       onl_trj.buf_in msg 
     endif    
     goto 10
     end 
```


--- 
{% hint style="info" %}

* Currently received pose or pose type strings can only be in axis-angle coordinates.
* Pose strings can only be in array-formatted axis-angle coordinates (e.g. [0.000,90.000,0.000,0.000,-90.000,0.000]).    

{% endhint %}
