# 5.14 外部控制

### 描述  
* 机器人的运动位置命令生成由外部设备执行，这个生成的外部命令通过以太网或串行通信作为字符串数据传输到 ${cont_model} 控制器。 ${cont_model} 控制器接收该命令并控制机器人。

### 语法 
```python
     global onl_trj
     var msg # 位姿或位姿类型字符串

     onl_trj=online.Traject()
     onl_trj.time_from_start=-1.0
     onl_trj.look_ahead_time=1.0
     onl_trj.interval=0.1
     onl_trj.init
     onl_trj.buf_in msg
 
```

### 参数 
* `time_from_start` : 从起始位置到现在的经过时间 (-1: 禁用)  
* `look_head_time` : 机器人移动的时间延迟 (单位 : [s])  
* `interval` : 生成命令之间的时间间隔 (单位 : [s])  
* `init` : 在线轨迹初始化，清除命令缓冲区  
* `buf_in`  : 将位姿或位姿类型字符串添加到命令缓冲区


### 示例
> 机器人通过接收外部生成的命令来移动，采用enet通信。

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
     onl_trj.look_ahead_time=1.0 # 机器人移动开始的延迟时间
     onl_trj.interval=0.1 # 生成命令的采样时间
     onl_trj.init # 缓冲区初始化

     var msg
10   enet0.recv
     str_pose=result()
      if msg == "stop"
       onl_trj.init # 缓冲区清除 (快速停止)
     else
       onl_trj.buf_in msg 
     endif    
     goto 10
     end 
```


--- 
{% hint style="info" %}

* 当前接收到的位姿或位姿类型字符串只能是轴-角坐标格式。
* 位姿字符串只能是数组格式的轴-角坐标 (例如 [0.000,90.000,0.000,0.000,-90.000,0.000])。    

{% endhint %}