# 2.10 import

### Description

Some features are not supported as hrspace's built-in features, but are also supported in the form of plug-in modules.

Some modules are pre-installed as default options, while others require you to install them.  
The module must be loaded into the controller with the `import` statement before it can be used in the robot language.

### Syntax

import &lt;module name&gt; [as &lt;alias&gt;]

### Parameter

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">module name</td>
      <td style="text-align:left">
        module's name
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">alias</td>
      <td style="text-align:left">
			Name to be used within the robot language program.<br>
			If specified, it can be used instead of the module name.
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

For example, in order to perform Ethernet TCP or UDP communication in the robot language, you must `import` the default option module called `enet`.

After executing the `import`, a module object named `enet` is created in the global scope. As in the example below `enet.ENet()`, you can access to a member variable or call a member function of a module object, and especially by calling a `creator` from among the member functions, you can create new object.

### Example

In the example below,  
(1) `enet` module object has been `import`ed.  
(2) The `enet.ENet()` creator function was called to create a new Ethernet socket object and assigned it into a local variable named `cli`.  
(3) Assigned a string to member variable `ip_addr` of the object `cli`.

```python
import enet # (1)
var cli=enet.ENet() # (2)
cli.ip_addr="192.168.1.172" # (3)
```

It does the same thing when you code it as below.

```python
import enet as enet_module # (1)
var cli=enet_module.ENet() # (2)
cli.ip_addr="192.168.1.172" # (3)
```

* This section only covered the rough syntax of the `import` statement. You will often see examples of the use of `import` in the later sections describing module features.