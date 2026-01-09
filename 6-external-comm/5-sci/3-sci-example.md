# 6.5.3 시리얼 통신 예제

``` python
Hyundai Robot Job File; { version: 1.6, mech_type: "", total_axis: -1, aux_axis: -1 }
     
     # 생성자로 Sci 객체 생성후 전역 변수에 대입 
     global sci2
     sci2=sci.Sci(2)   #port no. (com2)
     
     # clear receive buffer
     var ret
     ret=sci2.clr_rbuf()

     # send
     sci2.send "test"

     # receive (선택옵션: 3000ms 타임 아웃시, *timeout으로 분기)
     var msg
     sci2.recv msg,3000,*timeout
     print msg

     end

     *timeout
     print "error"
     stop

```


