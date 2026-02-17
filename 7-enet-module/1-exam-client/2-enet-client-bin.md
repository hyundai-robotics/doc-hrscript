# 7.1.2 点对点，客户端示例 - 发送接收二进制数据

二进制发送接收是通过 `BBuf`（二进制缓冲区）对象执行的。  
（只有发送接收的部分不同，其余与发送接收字符串数据的部分相同。）

发送

1. 创建 `enet.BBuf` 对象。
2. 使用 `BBuf.append()` 函数将所需的二进制数据附加到 `BBuf` 对象。
3. 作为 `ENET.send_bbuf()` 的一个函数发送 BBuf 对象。


接收

1. 创建 `enet.BBuf` 对象。
2. 使用 `ENET.recv_bbuf()` 函数接收二进制数据到 BBuf 对象中。
3. 使用 `BBuf.read_nums()` 函数从 `BBuf` 对象中读取所需的二进制数据。


<br>

### UDP 点对点
```python
     # 1. 导入 enet 模块后，使用构造函数创建 ENet 对象
     import enet
     var cli=enet.ENet() # 对于 TCP 通信，ENet("tcp")

     # 2. 设置 IP 地址和端口号
     cli.ip_addr="192.168.1.172" # 远程（对手）IP 地址
     cli.lport=51001 # 本地（自身）端口
     cli.rport=51002 # 远程（对手）端口
     # （端口号 49152-65535（除 50000-50005）为动态或私有端口）

     # 3. 打开以太网套接字
     cli.open
     
     print cli.state() # 如果为 1，则正常。

     # 发送 --------------------------------
     # 4-1. 创建 BBuf 对象
     var bbuf=enet.BBuf()

     # （示例二进制数据）
     var arr=[ -3, 0, 1 ]
     
     # 4-2. 将二进制数据附加到 BBuf 对象
     bbuf.clear()
     bbuf.append("s4", arr) # 附加小端有符号 4 字节数据

     # 4-3. 发送 BBuf 对象
     var ret
     ret=cli.send_bbuf(bbuf)

     # 接收 --------------------------------
     # 4-1. 创建 BBuf 对象
     var bbuf2=enet.BBuf()
     
     # 4-2. 接收二进制数据到 BBuf 对象
     #     （如果 3 秒内没有响应，跳转到 *TimeOut 标签）
     cli.recv_bbuf bbuf2,3000,*TimeOut

     # 4-3. 从 BBuf 对象中读取二进制数据。
     var nums=bbuf2.read_nums("U2", 0, 3) # 读取 3 个大端无符号 2 字节数据
     print nums
     # --------------------------------

     # 5. 关闭以太网套接字
     cli.close
     print cli.state() # 如果为 0，则正常。
     delay 1.5
     end

     *TimeOut
     print "超时！"
     cli.close
     end
```
### TCP 客户端
(仅 `lport` 和 `连接 (connect)` 部分与点对点不同。)
```python
     # 1. 导入 enet 模块后，用构造函数创建一个 ENet 对象
     import enet
     var cli=enet.ENet() # 对于 TCP 通信，ENet("tcp")

     # 2. 设置 IP 地址和端口号
     cli.ip_addr="192.168.1.172" # 远程 (对手) IP 地址
     cli.lport=0 # 本地 (自己) 端口；随机
     cli.rport=51002 # 远程 (对手) 端口
     # (端口号 49152-65535 包含动态或私有端口)

     # 3. 打开以太网套接字
     cli.open
     cli.connect # 连接到服务器。
     print cli.state() # 如果为 1，表示正常。

     # 发送 --------------------------------
     # 4-1. 创建 BBuf 对象
     var bbuf=enet.BBuf()

     # (样本二进制数据)
     var arr=[ -3, 0, 1 ]
     
     # 4-2. 将二进制数据附加到 BBuf 对象
     bbuf.clear()
     bbuf.append("s4", arr) # 附加小端符号的4字节数据

     # 4-3. 发送 BBuf 对象
     var ret
     ret=cli.send_bbuf(bbuf)

     # 接收 --------------------------------
     # 4-1. 创建 BBuf 对象
     var bbuf2=enet.BBuf()
     
     # 4-2. 将二进制数据接收进入 BBuf 对象
     #     (如果 3 秒内没有响应，则跳转到 *TimeOut 标签)
     cli.recv_bbuf bbuf2,3000,*TimeOut

     # 4-3. 从 BBuf 对象中读取二进制数据。
     var nums=bbuf2.read_nums("U2", 0, 3) # 读取 3 个大端无符号 2 字节数据
     print nums
     # --------------------------------

     # 5. 关闭以太网套接字
     cli.close
     print cli.state() # 如果为 0，表示正常。
     delay 1.5
     end

     *TimeOut
     print "超时!"
     cli.close
     end
```
* 字符串参数如 "s4" 和 "U2" 决定二进制数据格式，例如字节序类型、符号/无符号和字节数。更多信息，请参见 [7.4.2 Supported format](../4-bbuf/2-format.md)。