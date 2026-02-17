# 7.2.1 ethernet TCP 服务器 - 收发字符串数据

按照以下步骤操作：

1. 导入 `enet` 模块后，用构造函数创建一个 `ENet` 对象。
2. 使用成员变量设置 IP 地址和端口号。 (不需要设置远程端口。)
   - `注意：控制器的端口 50000-50005 已被预分配，无法使用。`
3. 使用 `open` 成员过程打开以太网套接字，并调用 `listen()`、`accept()` 函数。通过 `state()` 成员变量检查状态。
4. 使用 `send` 和 `recv` 成员过程进行收发。
5. 使用 `关闭 (close)` 成员过程关闭通信连接。


```python
     # 1. 导入 enet 模块后，用构造函数创建一个 ENet 对象
     import enet
     var svr=enet.ENet("tcp")
     
     # 2. 设置 IP 地址和端口号
     svr.ip_addr="192.168.1.172" # 远程（对手）IP 地址
     svr.lport=51001 # 本地（自我）端口
     # (端口号 49152-65535（不包括 50000-50005）包含动态或私有端口)
     
     # 3. 打开以太网套接字
     svr.open
     var ret
     ret=svr.listen()
     ret=svr.accept() # 等待客户端连接
     print svr.state() # 如果为 1，则正常。
     
     # --------------------------------
     # 4-1. 字符串发送
     svr.send "欢迎，我是一个 TCP 服务器。\n"
     
     # 4-2. 字符串接收
     #     (如果 5 秒内没有接收到，跳转到 *TimeOut 标签)
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
     print "超时！"
     svr.close
     end
```
