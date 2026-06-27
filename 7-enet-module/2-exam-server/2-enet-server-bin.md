# 7.2.2 ethernet TCP server 示例 - 双向传输二进制数据

二进制双向传输使用 `BBuf` (二进制缓冲区) 对象进行。  
(只有双向传输部分不同，其余与传输字符串数据相同。)

发送

1. 创建 `enet.BBuf` 对象。
2. 使用 `BBuf.append()` 函数将所需的二进制数据附加到 `BBuf` 对象。
3. 将 BBuf 对象发送为 `ENET.send_bbuf()` 函数的参数。

接收

1. 创建 `enet.BBuf` 对象。
2. 使用 `ENET.recv_bbuf()` 函数接收二进制数据到 BBuf 对象。
3. 使用 `BBuf.read_nums()` 函数从 `BBuf` 对象中读取所需的二进制数据。

```python
     # 1. 导入 enet 模块后，使用构造函数创建 ENet 对象
     import enet
     var svr=enet.ENet("tcp")
     
     # 2. 设置 IP 地址和端口号
     svr.ip_addr="192.168.1.172" # 远程（对方）IP 地址
     svr.lport=51001 # 本地（自身）端口
     # (端口号 49152-65535（除了 50000-50005）包含动态或私有端口)
     
     # 3. 打开以太网套接字
     svr.open
     var ret
     ret=svr.listen()
     ret=svr.accept() # 等待客户端连接
     print svr.state() # 如果为 1，则正常。

     # 发送 --------------------------------
     # 4-1. 创建 BBuf 对象
     var bbuf=enet.BBuf()

     # (示例二进制数据)
     var arr=[ -3, 0, 1 ]
     
     # 4-2. 将二进制数据附加到 BBuf 对象
     bbuf.clear()
     bbuf.append("s4", arr) # 附加小端签名4字节数据

     # 4-3. 发送 BBuf 对象
     ret=svr.send_bbuf(bbuf)

     # 接收 --------------------------------
     # 4-1. 创建 BBuf 对象
     var bbuf2=enet.BBuf()
     
     # 4-2. 接收二进制数据到 BBuf 对象
     #     (如果 3 秒没有响应，跳转到 *TimeOut 标签)
     svr.recv_bbuf bbuf2,3000,*TimeOut

     # 4-3. 从 BBuf 对象读取二进制数据。
     var nums=bbuf2.read_nums("U2", 0, 3) # 读取 3 个大端无符号2字节数据
     print nums
     # --------------------------------

     # 5. 关闭以太网套接字
     svr.close
     print svr.state() # 如果为 0，则正常。
     delay 1.5
     end

     *TimeOut
     print "超时！"
     svr.close
     end
```

* 字符串参数如 "s4" 和 "U2" 决定二进制数据格式，如字节序类型、签名/无签名及字节数。有关更多信息，请参见 [7.4.2 支持的格式](../4-bbuf/2-format.md)。