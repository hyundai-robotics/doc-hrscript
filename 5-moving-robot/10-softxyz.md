# 5.10 `softxyz`

`softxyz` 函数是一种无传感器的力控制功能，允许机器人在用户定义的条件下在笛卡尔空间中灵活移动以响应外部力量。

为确保正确操作，`工具数据和附加负载信息必须正确配置`。

{% hint style="warning" %}

由于 `softxyz` 函数是 `无传感器` 的，并且不使用力传感器，  
因此在实现完全平滑和自然运动方面存在 `固有限制`。

然而，通过根据应用环境适当调整 `softxyz_lim` 值，  
您可以在功能限制内实现尽可能平滑的运动。

因为 `softxyz_lim (pos / xnr / vel / thr)` 直接决定机器人如何响应外部力量，  
依据环境、装配过程和工具刚度，`需要进行微调`。

{% endhint %}

### 描述
* 该功能允许机器人在不使用力传感器的情况下，由外部力量在笛卡尔坐标系中位移。

---

### 语法
```python
softxyz on, crd=<reference_coordinate>
softxyz set, dpr=<stiffness>
softxyz off
```

### 参数
- `打开 (on)` : 启动 softxyz 功能  
- `关闭 (off)` : 停止 softxyz 功能  
- `set` : 修改 softxyz 设置  

- `crd` : 外部力位移的参考坐标系  
  - 可用选项：`基础 (base)`，`机器人 (robot)`，`工具 (tool)`，`user_x`

- `dpr` : 刚度值  
  - 范围：`0.0 ~ 2.0`  
  - 较高值 = `更刚性`，在外部力量下位移较少  
  - 默认：`1.0`

```python
softxyz on,  crd="base"     # 基于基础坐标系
softxyz on,  crd="robot"    # 基于机器人坐标系
softxyz on,  crd="tool"     # 基于工具坐标系
softxyz on,  crd="user_1"   # 用户定义的坐标系 #1

softxyz set, dpr=1.0        # 设置刚度 (0.0~2.0, 较高 = 更刚性)
softxyz off                 # 禁用 softxyz 功能
```
### 示例 
> 示例 1) 在允许 X、Y 和 Ry 位移的情况下沿 Z 方向组装
> * 坐标 : 机器人坐标 (crd="robot") <br>
> * 位置 (xnr) 限制 : X 和 Y 方向的范围 [-50,+50](mm)，Ry 方向的范围 [-3,+3] (度) <br>
> * 速度 (vel) 限制 : X 和 Y 方向的最大速度 5(mm/秒)，Ry 的最大速度 3(度/秒)  <br>
> * 力矩 (thr) 限制 : X 方向的阈值 3N，Y 方向的阈值 3N 和 Ry 方向的阈值 1Nm 

```python
S1   move P,spd=100mm/sec,accu=0,tool=0
     delay 2.0   # 在启用 softxyz之前所需
     softxyz_lim xnr, x=50, y=50, ry=3
     softxyz_lim vel, x=5, y=5, ry=3
     softxyz_lim thr, x=20, y=20, ry=3
     softxyz on, crd="robot"

S2   move P,spd=250mm/sec,accu=0,tool=0
     softxyz off
     end
```

> 示例 2) 注射材料处理 
> * 坐标 : 机器人坐标 (crd="robot") <br>
> * 位置 (pos) 限制 : +Y 方向的范围 [0,3]  
(mm)，-Y 方向的范围 [-200,0] (mm) <br>
> * 速度 (vel) 限制 : Y 方向的最大速度 150(mm/秒)<br>

```python
S1   move P,spd=100mm/sec,accu=0,tool=0
     delay 2.0   # 在启用 softxyz之前所需
     softxyz_lim pos, _y=300, y_=200
     softxyz_lim vel, y=150
     softxyz on, crd="robot"

S2   wait ...
     softxyz off
     end
```

--- 
> `信息`
>
> - 在使用 `softxyz on` 之前，您 `必须` 配置 `softxyz_lim` 参数  
>   (`pos`, `xnr`, `vel`, `thr`) 以设置最大位移、速度、  
>   和笛卡尔阈值。
>
> - 为了提高对外部力量的敏感性，建议您  
>   `使用 (保持机器人静止 1-2 秒) 的`delay`命令 ( command)`  
> 在执行 `softxyz on` 之前。
>
> - 如果在 softxyz 操作期间发生振动，建议进行以下调整：
>   1) *增加 `thr` 值*  
>   2) *增加 `dpr` 值*  
>   3) *减少 `vel` 值*