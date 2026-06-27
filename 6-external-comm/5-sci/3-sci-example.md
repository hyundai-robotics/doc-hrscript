# 6.5.3 串行通信示例

``` python
Hyundai Robot Job File; { version: 1.6, mech_type: "", total_axis: -1, aux_axis: -1 }
     
     # 使用构造函数创建 Sci 对象并将其分配给全局变量 
     global sci2
     sci2=com.Sci(2)   #port no. (com2)
     
     # 清除接收缓冲区
     var ret
     ret=sci2.clr_rbuf()

     # 发送
     sci2.send "test"

     # 接收 (选项: 当超过 3000ms 时，转到 *timeout)
     var msg
     sci2.recv msg,3000,*timeout
     print msg

     end

     *timeout
     print "error"
     stop

```