# 6.5.3 시리얼 통신 예제

``` python
Hyundai Robot Job File; { version: 1.6, mech_type: "388(HS220-02)", total_axis: 6, aux_axis: 0 }
     
     # sci 모듈 import 후, 생성자로 Sci 객체 생성 
     import sci
     var sci2=sci.Sci(2)   #port no. (com2)
     
     # default open
     # send
     sci2.send "test"

     # receive (선택옵션: 3000msec 타임 아웃시, 99행으로 분기)
     var msg=sci2.recv(3000,99)
     print msg

     # close 
     sci2.close
     
     # re-open
     sci2.open

     end

  99 print "error"

```


