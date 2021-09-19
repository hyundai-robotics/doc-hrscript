# post

### Description

Requests the HTTP post service.

It is required to assign the data, which is to be transmitted, to the body property in advance.

The response data is to be received to the body property.

### Syntax

&lt;HttpCli object&gt;.post &lt;URL string&gt;

### Example

```python
var domain="http://192.168.1.200:8888"
cli.body={ name: "WORK #32", color: "green", state: "OK" }
cli.post domain+"/display/update"
```

