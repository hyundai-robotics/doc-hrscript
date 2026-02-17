# 2.10 `import`

### 描述

某些功能不是 hrspace 的内置功能，但也以插件模块的形式得到支持。

一些模块作为默认选项预先安装，而另一些则需要您自行安装。  
该模块必须在机器人语言中通过 `import` 语句加载到控制器中，然后才能使用。

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

例如，为了在机器人语言中执行以太网 TCP 或 UDP 通信，您必须 `import` 名为 `enet` 的默认选项模块。

在执行 `import` 后，一个名为 `enet` 的模块对象将在全局作用域中创建。正如下面的例子 `enet.ENet()`，您可以访问模块对象的成员变量或调用成员函数，特别是在调用成员函数中的 `creator` 时，您可以创建新的对象。

### 示例

在下面的示例中，  
(1) `enet` 模块对象已被 `import`。
(2) 调用了 `enet.ENet()` 创建函数以创建一个新的以太网套接字对象，并将其分配给名为 `cli` 的局部变量。  
(3) 将一个字符串分配给对象 `cli` 的成员变量 `ip_addr`。

```python
import enet # (1)
var cli=enet.ENet() # (2)
cli.ip_addr="192.168.1.172" # (3)
```

以下面的方式编写时也会执行相同的操作。

```python
import enet as enet_module # (1)
var cli=enet_module.ENet() # (2)
cli.ip_addr="192.168.1.172" # (3)
```

* 本节仅涵盖了 `import` 声明的粗略语法。您将在后面的章节中看到关于模块功能的 `import` 使用示例。