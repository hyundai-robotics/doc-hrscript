# 7.2.1 ethernet TCP server - 传输字符串数据

Follow these steps:

1. 在导入 `enet` 模块后，使用构造函数创建 `ENet` 对象。
2. 用成员变量设置 IP 地址和端口号。 (不需要设置远程端口。)
   - `注意: 控制器上的端口 50000-50005 是预分配的 lports，不能使用。`
3. 使用 `open` 成员过程打开以太网套接字，并调用 `listen()`、`accept()` 函数。使用 `state()` 成员变量检查状态。
4. 使用 `send` 和 `recv` 成员过程进行传输。
5. 使用 `关闭 (close)` 成员过程关闭通信连接。


```python
     # 1. 在导入 enet 模块后，创建一个 ENet 对象
     import enet
     var svr=enet.ENet("tcp")
     
     # 2. 设置 IP 地址和端口号
     svr.ip_addr="192.168.1.172" # 远程（对手）IP 地址
     svr.lport=51001 # 本地（自己）端口
     # (端口号 49152-65535（除 50000-50005 外）包含动态或私人端口)
     
     # 3. 打开以太网套接字
     svr.open
     var ret
     ret=svr.listen()
     ret=svr.accept() # 等待客户端连接
     print svr.state() # 如果为 1，则正常。
     
     # --------------------------------
     # 4-1. 字符串传输
     svr.send "欢迎，我是一个 TCP 服务器。\n"
     
     # 4-2. 字符串接收
     #     （如果 5 秒内未接收，跳转到 *TimeOut 标签）
     svr.recv 5000,*TimeOut
     var msg=result() # 接收到的字符串
     print msg
     delay 1.0
     # --------------------------------
     
     # 5. 关闭以太网套接字
     svr.close
     print svr.state() # 如果为 0，则正常。
     delay 1.5
     end

     *TimeOut
     print "超时!"
     svr.close
     end
```