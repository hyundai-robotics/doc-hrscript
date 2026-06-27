# 6.5 Sci module : Serial communication

串行通信可以通过 ${cont_model} 控制器的 COM 端口进行。

要使用此功能，您必须创建一个 `Sci` 对象作为全局变量，如下所示。

另外，在使用之前，请务必检查 `[F2: 系统] - 2. Control Parameters - 3. Serial Port ([F2: System] - 2. Control Parameters - 3. Serial Port)` 中的设置规格。

```python
global sci2
sci2=com.Sci(2)
```

创建 `Sci` 对象后，只需调用 `send`、`recv`、`open` 和 `关闭 (close)` 成员过程。

调用 `send` 时，必须事先输入要发送的字符串。

调用 `recv` 时，成功接收后会分配给指定的字符串变量。

调用 open 时，端口会被打开。

调用 open 时，端口将关闭。