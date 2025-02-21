# 6.5.3 Serial communication example

``` python
Hyundai Robot Job File; { version: 1.6, mech_type: "", total_axis: -1, aux_axis: -1 }
     
     # Create a Sci object using the constructor and assign it to a global variable 
     global sci2
     sci2=sci.Sci(2)   #port no. (com2)
     
     # clear receive buffer
     var ret
     ret=sci2.clr_rbuf()

     # send
     sci2.send "test"

     # receive (option: when 3000ms over, goto *timeout)
     var msg
     sci2.recv msg,3000,*timeout
     print msg

     end

     *timeout
     print "error"
     stop

```


