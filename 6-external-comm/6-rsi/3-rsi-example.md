# 6.6.3 Sensor interface example

``` python
Hyundai Robot Job File; { version: 1.6, mech_type: "", total_axis: -1, aux_axis: -1 }
     
     # Create an RSI object using the constructor and assign it to a global variable 
     global rsi
     rsi=com.RSI(_enet0)  # Communicate with the enet0 configuration object
     rsi.format="json" # String format "json" or "xml"
     rsi.period=5  # data transmission cycle(ms)
     var ret

     # send start
     ret=rsi.on
     ret=rsi.put("cmd_po")  # Include "cmd_po" tag

     move L,spd=100mm/s,accu=1,tool=1
     ret=rsi.put("trigger", 1)  # Change trigger tag value
     move L,spd=100mm/s,accu=1,tool=1
     move L,spd=100mm/s,accu=1,tool=1
     ret=rsi.put("MyValue1", 789)  # Add MyValue1 tag
     move L,spd=100mm/s,accu=1,tool=1

     # send stop
     rsi.off

     end


```


