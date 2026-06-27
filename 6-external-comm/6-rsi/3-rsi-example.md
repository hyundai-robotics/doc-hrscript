# 6.6.3 传感器接口示例

``` python
Hyundai Robot Job File; { version: 1.6, mech_type: "", total_axis: -1, aux_axis: -1 }
     
     # 使用构造函数创建RSI对象并将其分配给全局变量 
     global rsi
     rsi=com.RSI(_enet0)  # 与enet0配置对象通信
     rsi.format="json" # 字符串格式 "json" 或 "xml"
     rsi.period=5  # 数据传输周期(ms)
     var ret

     # 发送开始
     ret=rsi.on
     ret=rsi.put("cmd_po")  # 包含 "cmd_po" 标签

     move L,spd=100mm/s,accu=1,tool=1
     ret=rsi.put("trigger", 1)  # 更改触发标签值
     move L,spd=100mm/s,accu=1,tool=1
     move L,spd=100mm/s,accu=1,tool=1
     ret=rsi.put("MyValue1", 789)  # 添加 MyValue1 标签
     move L,spd=100mm/s,accu=1,tool=1

     # 发送停止
     rsi.off

     end


```