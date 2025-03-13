# 5.14 외부 제어(External control)


## 설명 
* 로봇의 이동에 대한 위치 지령 생성은 외부 장치에서 수행하고 이 생성된 외부 지령을 이더넷이나 시리얼 통신을 통해 문자열 데이터로 Hi6 제어기에 전송하면 Hi6 제어기는 이 지령을 수신하여 해당 로봇을 제어하는 기능입니다. 


## 문법 
```python
     global onl_trj
     var msg # 포즈 or 포즈형 문자열

     onl_trj=online.Traject()
     onl_trj.time_from_start=-1.0
     onl_trj.look_ahead_time=1.0
     onl_trj.interval=0.1
     onl_trj.init
     onl_trj.buf_in msg
 
```

## 파라미터 
* time_from_start : 시작 지령으로 부터 경과된 시간 (-1= 미사용)
* look_ahead_time : 지령 출력을 위한 지연시간 (단위 [s])
* interval : 생성된 지령의 샘플링 시간 (단위 [s])
* init : 온라인 지령상태 초기화, 지령 버퍼를 초기화 
* buf_in : <포즈> 또는 <포즈형 문자열>을 지령 버퍼에 추가  



## 사용 예 
> enet 통신을 통해 외부에서 생성된 지령을 수신하여 로봇을 이동합니다. 

```python
     import enet
     global enet0
     enet0=enet.ENet("tcp")
     enet0.ip_addr="192.168.1.213"
     enet0.lport=7000
     enet0.rport=7000
     enet0.open()
     var ret=enet0.open()
     ret=enet0.listen()
     ret=enet0.accept()

     global onl_trj
     onl_trj=online.Traject()
     onl_trj.time_from_start=-1.0
     onl_trj.look_ahead_time=1.0 # 로봇이동 시작의 지연시간
     onl_trj.interval=0.1 # 생성된 지령의 샘플링 시간
     onl_trj.init # 버퍼 초기화

     var msg
10   enet0.recv
     msg=result()
     if msg == "stop"
       onl_trj.init # 버퍼 클리어 (즉시정지)
     else
       onl_trj.buf_in msg 
     endif
     goto 10
     end 
```


--- 
{% hint style="info" %}

* 현재 수신된 포즈나 포즈형의 문자열은 축각도 좌표로만 가능합니다.  
* 포즈형 문자열은 배열 형식의 축각도 좌표로만 가능합니다. (ex. [0.000,90.000,0.000,0.000,-90.000,0.000])  

{% endhint %}
