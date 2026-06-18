# 6.6 RSI 모듈 : 센서 인터페이스

V70.02-00부터 지원됩니다.

"RSI"는  "원격 센서 인터페이스"의 약자입니다.

제어기의 이더넷 통신을 통해 로봇의 위치데이터등을 RSI를 지원하는 장치로 실시간으로 전송합니다. <br>
(로봇 제어기 -> 원격 센서 장치) <br>

이더넷 통신으로는 UDP, TCP Client, TCP Server 모두 지원합니다. <br>
이더넷 통신 설정에 대한 내용은 별도의 "[${cont_model} 제어기 조작 설명서 - TP630](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/ko-tp630/7-system/3-control-parameter/9-network-setting/2-service/4-enet-comm-setting?cont_model=${cont_model})"를 참조하십시오. 


이 기능을 사용하기 위해서는 아래와 같이 RSI 객체를 전역변수로 생성해야 합니다.

```python
global rsi
rsi=com.RSI(_enet0)  # _enet0는 이더넷 통신 설정에서 "enet0"의 객체를 사용 
```

RSI 객체를 생성한 후에는 on, off, put등의 멤버 프로시져를 호출하면 됩니다.

on를 실행한 후에는 데이터 전송을 시작합니다.

off를 실행한 후에는 데이터 전송을 정지합니다. 

put를 호출하여 전송값을 변경하거나 새로운 태그를 추가할 수 있습니다. 


<br>

### 전송 데이터
전송하는 데이터는 기본 태그에 HRScript 명령문 실행에 의해 사용자가 태그를 추가할 수 있습니다. <br>
기본 태그는 하기와 같이 구성됩니다.
- cpo_cur : 로봇의 위치와 자세에 대한 현재값입니다. (x, y, z, rx, ry, rz) 
- cpo_cmd : 로봇의 위치와 자세에 대한 지령값입니다. (x, y, z, rx, ry, rz) <br>
- tsp : 이전 데이터 전송 후 현재 데이터 전송까지 소요된 시간입니다.(us) <br>
- index : rsi.on 실행 후 0으로 초기화 되며 데이터를 전송할 때마다 1씩 증가하는 값입니다. <br>
이를 사용하여 통신 누락을 확인할 수 있습니다.
- trigger : rsi.on 실행 후 0의 값으로 생성되는 사용자 태그입니다. <br>
HRScript 명령문 실행에 의해 값을 변경하여 센서 장치에서 읽어 처리하는 로직을 구성할 수 있습니다.  
- 사용자 태그 : HRScript 명령문 실행에 의해 사용자 태그를 추가하고 이 태그의 값을 변경할 수 있습니다. <br>
rsi.on 실행 후 추가된 사용자 태그는 모두 클리어 됩니다.
<br>
<br>

#### 전송 데이터는 문서 형식에 따라 하기와 같습니다.
rsi.format="json" 또는 rsi.format="xml"의 HRScript 명령문 실행에 의해 문서 형식을 "JSON" 또는 "XML"로 지정할 수 있습니다. (기본값 = "JSON")
<br>

JSON 형식
```python
{
	"cpo_cur" : {
		"x" : 2407.675176,
		"y" : -38.666578,
		"z" : 2006.844781,
		"rx" : -158.004863,
		"ry" : 83.273921,
		"rz" : -159.598022
	},
	"cpo_cmd" : {
		"x" : 2407.697000,
		"y" : -59.810000,
		"z" : 2006.820000,
		"rx" : -158.036000,
		"ry" : 83.271000,
		"rz" : -159.618000
	},
	"tsp" : 3812,
	"index" : 186,
	"trigger" : 0
}
```
<br>

XML 형식
```python
<Rob Type="HYUNDAI" tsp="3938">
    <cpo_cur x="2407.6" y="-37.7" z="2006.8" rx="-157.9988" ry="83.2761" rz="-159.5930"/>
    <cpo_cmd x="2407.6" y="-63.0" z="2006.8" rx="-158.018" ry="83.276" rz="-159.56"/>
    <index>167</index>
    <trigger>0</trigger>
</Rob>
```

