# 5.12 `softjoint`

`softjoint` 指令是无传感器的力控制，允许机器人在关节空间中相对于用户设定的环境中的外部力量以顺应方式移动。 <br>

用户应检查机器人工具和附加轴信息的有效性，以提高功能的准确性。 <br>

--- 

### 描述 
* 无需使用传感器，在关节空间中相对于用户设定的环境中的外部力量以顺应方式移动。 

### 语法 
```python
softjoint on
softjoint off  
```

### 参数
* on : 功能开始
* off : 功能结束 

--- 
{% hint style="info" %}

* 在使用 `softjoint on` 之前，用户应设置 softjoint_lim 参数，例如关节编号(` (j)`)、柔软度(`sft`)、关节角度限制(`ang`)和扭矩阈值(`thr`)。

* 为了提升无传感器力控制性能，用户应在 `softjoint on` 之前将 `时间延迟 (delay)` 命令设置为 `delay 1.0`。  

{% endhint %}