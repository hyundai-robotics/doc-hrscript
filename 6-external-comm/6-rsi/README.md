# 6.6 RSI module : Sensor Interface

Supported from V70.02-00.

"RSI" stands for "Remote Sensor Interface".

The robot's position data, etc., is transmitted in real time to a device that supports RSI via the controller's Ethernet communication. <br>
(Robot controller -> Remote sensor device) <br>

Ethernet communication supports UDP, TCP Client, and TCP Server. <br>
For information on Ethernet communication settings, please refer to the separate "[${cont_model} Controller Operation Manual - TP630](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/7-system/3-control-parameter/9-network-setting/2-service/4-enet-comm-setting?cont_model=${cont_model})". 


To use this feature, you must create an RSI object as a global variable as follows.

```python
global rsi
rsi=com.RSI(_enet0)  # _enet0 uses the "enet0" object in Ethernet communication settings 
```

After creating the RSI object, you can call member procedures such as on, off, and put.

After executing 'on', data transmission begins.

After executing off, data transmission stops. 

You can change the transmitted value or add a new tag by calling put. 


<br>

### Transfer data
The data being transmitted can have option tags added to the basic tags by executing HRScript statements. <br>
Tags are structured as follows. <br>

##### Basic tags <br>

- cur_po : These are the current values ​​for the robot's position and orientation. (x, y, z, rx, ry, rz) 
- tsp : This is the time elapsed from the previous data transmission to the current data transmission.(us) <br>
- index : It is a value that is initialized to 0 after rsi.on is executed and increases by 1 each time data is transmitted. <br>
You can use this to check for missing communications.
- trigger : This is a tag automatically generated with a value of 0 after running rsi.on. <br>
You can change the value to 1 by executing rsi.put("trigger", 1) and configure logic to read and process the value from the sensor device.  
##### Option tags <br>
- cpo_cmd : These are command values ​​for the robot's position and orientation. (x, y, z, rx, ry, rz)  <br>
When you execute rsi.put("cmd_po"), the "cmd_po" tag is added in the same format as the "cur_po" tag.
- User tags : You can add user tags and change the value of these tags by executing rsi.put("tag name", value). <br>
<br>
<br>

#### The transmitted data is as follows, depending on the document format.
You can specify the document format as "JSON" or "XML" by executing rsi.format="json" or rsi.format="xml". (Default = "JSON")
<br>

JSON Format
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

XML Format
```python
<Rob Type="HYUNDAI" tsp="3938">
    <cur_po x="2407.6" y="-37.7" z="2006.8" rx="-157.9988" ry="83.2761" rz="-159.5930"/>
    <index>167</index>
    <trigger>0</trigger>
</Rob>
```

