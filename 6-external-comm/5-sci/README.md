# 6.5 Sci模块：串行通信

串行通信可以通过 ${cont_model} 控制器的 COM 端口进行。

要使用此功能，您必须创建一个 `Sci` 对象作为全局变量，如下所示。

此外，请确保在使用前检查 `[F2: 系统] - 2. 控制参数 - 3. 串口 ([F2: System] - 2. Control Parameters - 3. Serial Port)` 中的设置规格。

```python
global sci2
sci2=com.Sci(2)
```

创建 `Sci` 对象后，只需调用 `send`、`recv`、`open` 和 `关闭 (close)` 成员程序。

调用 `send` 时，您必须提前输入要发送的字符串。

调用 `recv` 时，它会在成功接收后分配给指定的字符串变量。

调用 open 时，将打开端口。

调用 open 时，将关闭端口。