# 2.10 import문

### 설명

일부 기능은 hrspace 내장 기능으로서는 기본 제공하지 않지만, 플러그인 모듈(plug-in module)의 형태로 지원되기도 합니다.

hrscript의 일부 기능은 hrscript가 기본으로 제공하지 않지만, 플러그인 모듈(plug-in module)의 형태로 지원하기도 합니다.
기본 옵션으로서 미리 설치되어 있는 모듈도 있고, 사용자가 설치해주어야 하는 모듈도 있습니다.  
모듈은 `import`문을 써서 제어기로 load 해야만 로봇언어에서 사용 가능합니다.

### 문법

import &lt;모듈명&gt; [as &lt;별칭&gt;]

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">모듈명</td>
      <td style="text-align:left">
        모듈의 이름
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">별칭(alias)</td>
      <td style="text-align:left">
        로봇언어 프로그램 내에서 사용할 이름.<br>
        지정하면 모듈명 대신 사용 가능.
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

가령, 로봇언어에서 이더넷 TCP나 UDP 통신을 하기 위해서는 `enet`이라는 기본 옵션 모듈을 `import`해야 합니다.

`import`를 수행하고 나면, `enet`이라는 이름의 모듈 객체가 전역 스코프(global scope)에 생성됩니다. 아래 예제의 `enet.ENet()`와 같이 모듈 객체의 멤버변수나 멤버함수를 사용할 수 있으며, 특히 멤버함수 중 생성자를 호출하여 새로운 객체를 생성할 수 있습니다.

### 사용 예

아래 예에서는,  
(1) `enet` 모듈 객체를 `import` 했습니다.  
(2) `enet.ENet()` 생성자 함수를 호출하여 새로운 이더넷 소켓 객체를 생성한 후 이를 `cli` 라는 이름의 지역변수에 대입했습니다.  
(3) `cli` 객체의 `ip_addr` 멤버변수에 문자열을 대입했습니다.

```python
import enet # (1)
var cli=enet.ENet() # (2)
cli.ip_addr="192.168.1.172" # (3)
```

아래와 같이 작성해도 동일한 동작을 수행합니다.

```python
import enet as enet_module # (1)
var cli=enet_module.ENet() # (2)
cli.ip_addr="192.168.1.172" # (3)
```

* 이 절에서는 `import`문에 대한 개략적인 문법만 다루었습니다. 이 후, 모듈 기능들을 설명하는 절에서 `import`의 사용 예를 자주 보게 될 것입니다.
