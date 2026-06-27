# 7.1.1 peer-to-peer, client 示例 - 传输字符串数据

按照以下步骤进行：

1. 在导入 `enet` 模块后，通过构造函数创建一个 `ENet` 对象。
2. 使用成员变量设置 IP 地址和端口号。
   - `注意：控制器上的端口 50000-50005 是预分配的 lports，无法使用。`
3. 使用 `open` 成员过程打开以太网套接字，并使用 `state()` 成员变量检查状态。
\(对于 TCP 通信，在打开之后还必须调用 `连接 (connect)` 过程。\)
1. 使用 `send` 和 `recv` 成员过程进行传输。
2. 使用 `关闭 (close)` 成员过程关闭通信连接。

<br>

### UDP peer-to-peer
```python
     # 1. 在导入 enet 模块后，通过构造函数创建一个 ENet 对象
     import enet
     var cli=enet.ENet() # 默认 enet 模式是 "udp"

     # 2. 设置 IP 地址和端口号
     cli.ip_addr="192.168.1.172" # 远程（对手）IP 地址
     cli.lport=51001 # 本地（自己）端口
     cli.rport=51002 # 远程（对手）端口
     # (端口号 49152-65535（排除 50000-50005）包含动态或私有端口)

     # 3. 打开以太网套接字
     cli.open
     
     print cli.state() # 如果是 1，则正常。

     # --------------------------------
     # 4-1. 字符串传输
     cli.send "hello, peer.\n"

     # 4-2. 字符串接收
     #     (如果 5 秒内未接收到，跳转到 *TimeOut 标签)
     var msg
     cli.recv 5000, *TimeOut
     var msg=result() # 接收到的字符串
     print msg
     delay 1.0
     # --------------------------------

     # 5. 关闭以太网套接字
     cli.close
     print cli.state() # 如果是 0，则正常。
     delay 1.5
     end

     *TimeOut
     print "时间到了!"
     cli.close
     end
```
<br>

### TCP client
(仅 `lport` 和 `连接 (connect)` 部分与 peer-to-peer 不同。)
```python
     # 1. 在导入 enet 模块后，通过构造函数创建一个 ENet 对象
     import enet
     var cli=enet.ENet("tcp")

     # 2. 设置 IP 地址和端口号
     cli.ip_addr="192.168.1.172" # 远程（对手）IP 地址
     cli.lport=0 # 本地（自己）端口；随机
     cli.rport=51002 # 远程（对手）端口
     # (端口号 49152-65535 包含动态或私有端口)

     # 3. 打开以太网套接字
     cli.open
     cli.connect # 连接到服务器。
     print cli.state() # 如果是 1，则正常。

     # --------------------------------
     # 4-1. 字符串传输
     cli.send "hello, peer.\n"

     # 4-2. 字符串接收
     #     (如果 5 秒内未接收到，跳转到 *TimeOut 标签)
     var msg
     cli.recv 5000, *TimeOut
     var msg=result() # 接收到的字符串
     print msg
     delay 1.0
     # --------------------------------

     # 5. 关闭以太网套接字
     cli.close
     print cli.state() # 如果是 0，则正常。
     delay 1.5
     end

     *TimeOut
     print "时间到了!"
     cli.close
     end
```