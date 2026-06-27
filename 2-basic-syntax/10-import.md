# 2.10 `import`

### 描述

一些功能并不是 hrspace 的内置功能，但也以插件模块的形式提供支持。

某些模块作为默认选项预装，而其他模块则需要您安装它们。  
该模块必须在机器人语言中通过 `import` 语句加载到控制器中，才能使用。

### 语法

import &lt;module name&gt; [as &lt;alias&gt;]

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">module name</td>
      <td style="text-align:left">
        模块的名称
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">alias</td>
      <td style="text-align:left">
			在机器人语言程序中使用的名称。<br>
			如果指定，可以代替模块名称使用。
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

例如，若要在机器人语言中进行以太网 TCP 或 UDP 通信，必须 `import` 名为 `enet` 的默认选项模块。

执行 `import` 后，在全局范围内创建一个名为 `enet` 的模块对象。如下面的示例 `enet.ENet()`，您可以访问模块对象的成员变量或调用成员函数，特别是通过调用成员函数中的 `creator`，您可以创建新对象。

### 示例

在下面的示例中，  
(1) `enet` 模块对象已被 `import`。  
(2) 调用 `enet.ENet()` 创建一个新的以太网套接字对象，并将其分配给名为 `cli` 的局部变量。  
(3) 将一个字符串分配给对象 `cli` 的成员变量 `ip_addr`。

```python
import enet # (1)
var cli=enet.ENet() # (2)
cli.ip_addr="192.168.1.172" # (3)
```

以如下方式编写代码时，效果也是一样的。

```python
import enet as enet_module # (1)
var cli=enet_module.ENet() # (2)
cli.ip_addr="192.168.1.172" # (3)
```

* 本节仅涵盖了 `import` 语句的粗略语法。您将在后面的章节中看到 `import` 的使用示例，这些章节描述模块功能。