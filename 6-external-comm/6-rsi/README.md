# 6.6 RSI模块 : 传感器接口

支持自 V70.02-00。

"RSI" 代表 "远程传感器接口"。

机器人的位置信息等实时通过控制器的以太网通信传输到支持 RSI 的设备。 <br>
(机器人控制器 -> 远程传感器设备) <br>

以太网通信支持 UDP、TCP客户端和 TCP服务器。 <br>
有关以太网通信设置的信息，请参阅单独的 "[${cont_model} 控制器操作手册 - TP630](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/7-system/3-control-parameter/9-network-setting/2-service/4-enet-comm-setting?cont_model=${cont_model})"。

要使用此功能，您必须创建一个 RSI 对象作为全局变量，如下所示。

```python
global rsi
rsi=com.RSI(_enet0)  # _enet0 使用以太网通信设置中的 "enet0" 对象 
```

创建 RSI 对象后，您可以调用成员程序，例如 on、off 和 put。

执行 'on' 后，数据传输开始。

执行 off 后，数据传输停止。

您可以通过调用 put 来更改传输的值或添加新的标签。 

<br>

### 传输数据
通过执行 HRScript 语句，可以向基本标签添加选项标签。 <br>
标签的结构如下。 <br>

##### 基本标签 <br>

- cur_po : 这些是机器人的当前位置和方向的当前值。 (x, y, z, rx, ry, rz) 
- tsp : 这是从上一次数据传输到当前数据传输的时间经过时间。 (us) <br>
- index : 这是一个在执行 rsi.on 后初始化为 0 的值，每次传输数据时增加 1。 <br>
您可以通过它检查丢失的通信。
- trigger : 这是在运行 rsi.on 后自动生成的，值为 0 的标签。 <br>
您可以通过执行 rsi.put("trigger", 1) 将值更改为 1，并配置逻辑以从传感器设备读取和处理该值。  
##### 选项标签 <br>
- cpo_cmd : 这些是机器人的位置和方向的命令值。 (x, y, z, rx, ry, rz)  <br>
当您执行 rsi.put("cmd_po") 时，"cmd_po" 标签将以与 "cur_po" 标签相同的格式添加。
- 用户标签 : 您可以添加用户标签并通过执行 rsi.put("tag name", value) 来更改这些标签的值。 <br>
<br>
<br>

#### 传输的数据如下，具体取决于文档格式。
您可以通过执行 rsi.format="json" 或 rsi.format="xml" 来指定文档格式为 "JSON" 或 "XML"。 (默认 = "JSON")
<br>

JSON格式
```python
{
	"cur_po" : {
		"x" : 2407.675176,
		"y" : -38.666578,
		"z" : 2006.844781,
		"rx" : -158.004863,
		"ry" : 83.273921,
		"rz" : -159.598022
	},
	"tsp" : 3812,
	"index" : 186,
	"trigger" : 0
}
```
<br>

XML格式
```python
<Rob Type="HYUNDAI" tsp="3938">
    <cur_po x="2407.6" y="-37.7" z="2006.8" rx="-157.9988" ry="83.2761" rz="-159.5930"/>
    <index>167</index>
    <trigger>0</trigger>
</Rob>
```