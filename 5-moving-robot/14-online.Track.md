# 5.14 online.Track


## 설명 
* UDP에 의해 이더넷으로 위치 증분이 입력될 때, 이를 반영하여 로봇을 제어 


## 문법 
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

## 파라미터 
* init : 초기 설정값 확정 
* exe <포즈데이터> : <포즈> 데이터는 로봇의 축 각도로 설정  



## 사용 예 
> enet 명령어를 통해 외부에서 로봇 각축 데이터 msg 명령을 전달 받는다. 

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

* online 명령어는 enet 명령어를 통해 외부로 부터 UDP 통신을 이용하여 전달 받은 외부 지령으로, 로봇을 움직이게 합니다.    

{% endhint %}
