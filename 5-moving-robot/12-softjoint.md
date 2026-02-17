# 5.12 `softjoint`

`softjoint` 指令是无传感器的力控制，允许机器人在关节空间中以用户设定的外部力量为参考进行顺应移动。 <br>

用户应检查机器人工具和附加轴信息的有效性，以提高功能准确性。 <br>



--- 

### 描述 
* 在不使用传感器的情况下，以用户设定的环境中外部力量为参考，在关节空间中顺应移动。 


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

* 在使用 `softjoint on` 之前，用户应设置 softjoint_lim 参数，例如关节号 (`字母j (j)`)、柔软度 (`sft`)、关节角度限制 (`ang`) 和扭矩阈值 (`thr`)。

* 为了提升无传感器力控制性能，用户应该在 `softjoint on` 之前设置 `延迟 (delay)` 命令为 `delay 1.0`。  

{% endhint %}