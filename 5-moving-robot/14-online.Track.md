# 5.14 online.Track


### Description  
* As position increments are input to Ethernet through UDP communication, robot move toward the command. 

### Syntax 
```python
     global onl_track
     var desired_pose 

     onl_track=online.Track()
     onl_track.time_from_start=-1.0
     onl_track.look_ahead_time=1.0
     onl_track.exe_interval=0.1
     onl_track.init
     onl_track.exe desired_pose
 
```

### Parameter 
* init : initial setting  
* exe  : user should set the pose data in joint space coordinate  



### Example
> joint angle data is obtained from "msg" command through "enet" command. 

```python
     import enet
     global enet0
     global onl_track
     var desired_pose
     var msg
     enet0=enet.ENet("udp")
     enet0.ip_addr="192.168.0.7"
     enet0.lport=7000
     enet0.rport=7000
     enet0.open
     
     onl_track=online.Track()
     onl_track.time_from_start=-1.0
     onl_track.look_ahead_time=1.0
     onl_track.exe_interval=0.1
     onl_track.init

10   enet0.recv msg
     desired_pose=Pose(msg)
     onl_track.exe desired_pose
     goto 10
     end 
```


--- 
{% hint style="info" %}

* The role of robot language "online" is that robot move toward desired joint angle command from "enet" through UDP communication.   

{% endhint %}
