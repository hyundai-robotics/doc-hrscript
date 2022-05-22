# put

### Description

Requests the HTTP put service

It is required to assign the data, which is to be transmitted, to the body property in advance.

### Syntax

&lt;HttpCli object&gt;.put &lt;URL string&gt;

### Example

```python
var domain="http://192.168.1.200:8888"
cli.body=500
cli.put domain+"/setting/max_torque"
```



