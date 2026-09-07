# 6.6.3 센서 인터페이스 예제

``` python
Hyundai Robot Job File; { version: 1.6, mech_type: "", total_axis: -1, aux_axis: -1 }
     
     # 생성자로 RSI 객체 생성후 전역 변수에 대입 
     global rsi
     rsi=com.RSI(_enet0)  # enet0 설정 객체로 통신
     rsi.format="json" # 문자열 형식 "json" 또는 "xml"
     rsi.period=5  # 데이터 전송 주기(ms)
     var ret

     # send start
     rsi.on
     ret=rsi.put("cmd_po")  # "cmd_po" 태그를 추가

     move L,spd=100mm/s,accu=1,tool=1
     ret=rsi.put("trigger", 1)  # trigger 태그 값 변경
     move L,spd=100mm/s,accu=1,tool=1
     move L,spd=100mm/s,accu=1,tool=1
     ret=rsi.put("MyValue1", 789)  # MyValue1 태그 추가
     move L,spd=100mm/s,accu=1,tool=1

     # send stop
     rsi.off

     end


```


