# 6.1.3 `fn` 对象

您可以通过指定 `fb` 对象的特定区域来定义 `fn` 对象。
如果 ${cont_model} 控制器是现场总线主设备，并且有多个现场总线从设备，您可以将每个从设备的区域设置为每个 `fn` 对象，以直观地处理这些从设备。

![](../../_assets/io/io_fn.png)

有关如何设置 `fn` 区域的说明，请参见以下链接。

[操作手册：fn 块分配](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/7-system/3-control-parameter/2-io-signal-setting/12-fn-block?cont_model=${cont_model})

&nbsp;

`fn` 的语法与 `fb` 相同。
`fn` 索引范围为 0 到 63，位索引范围为 0 到 959，与 `fb` 一样。
也就是说，最大可配置索引为 fn0.do0 到 fn63.do959。

当访问未配置的不存在的 `fn` 对象或访问超出 `fn` 设置范围的 do/di 时，会发生错误。

请参见以下用例；



```python
fn2.dob3=0b00001111  	# 将 fn2 的输出字节 3 设置为二进制位
fn[4].dob1=0x0F  	# 打开 fn4 的输出字节 1 的低 4 位，并关闭高 4 位。
var work_no=fn63.dib3    # 将 fn63 的输入字节 3 赋值给 work_no 变量
if fn5.di43 then *err  	# 当 fn5.di42 打开时分支到 *err 标签。
for idx=21 to 29
  fn3.do[idx]=1  	# 打开 fn3 的所有输出信号 do21 ~ do29。
next
fn2.do3=fn2.do7=fn2.do11=1   # 同时打开 fn2 的输出信号 3、7 和 11。
```