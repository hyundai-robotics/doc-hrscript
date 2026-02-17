# 5.13 `softjoint_lim`

在使用指令 `softjoint on` 之前，用户应设置 `softjoint_lim` 参数，例如关节编号（`字母j (j)`）、柔性（`sft`）、关节角度限制（`ang`）和扭矩阈值（`thr`）。 <br>

--- 

### 语法 
```python
softjoint_lim, j=<关节编号>, sft=<柔性>, ang=<关节角度限制>, thr=<扭矩阈值> 
```

### 参数
* j : 关节编号 [1~6]
* sft : 更大的值使移动更柔软 [0:off,0~100]
* ang : 关节角度限制 [度]
* thr : 扭矩阈值 [Nm]


### 示例 
> 示例1）设置关节编号 3(J3) 上的参数 
> * 在 J3 上激活，柔性(50)，关节角度限制 [-30~30] (度) 和扭矩阈值 10(Nm)   
```python
softjoint_lim, j=3, sft=50, ang=30, thr=10
```

> 示例2）设置关节编号 2 和 3(J2, J3) 上的参数
> * 设置柔性 : J2-sft(30), J3-sft(80)  
> * 设置关节角度限制 : J2[-50,+50] (度), J3[最小关节角度限制, 最大关节角度限制] (度) <br>
> * 设置扭矩阈值 : J2-thr(3)(Nm), J3-thr(5)(Nm) 


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

* 使用 `softjoint` 功能时，应设置 `字母j (j)` 和 `sft` 的参数在 `softjoint_lim` 上。如果不设置 `ang` 参数，机器人将在定义的软限制内移动。而扭矩阈值 `thr` 的默认参数值为 0 [Nm]。 

{% endhint %}