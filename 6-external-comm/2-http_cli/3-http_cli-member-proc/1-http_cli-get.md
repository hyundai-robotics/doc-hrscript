# `get`

### Description

请求HTTP GET服务。

服务器检索与请求的URL相关的信息并在响应中返回。

响应数据存储在`body`属性中。

### Syntax

&lt;HttpCli object&gt;.get &lt;URL string, timeout, timeout fallback address&gt;

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Item</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Note</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>URL string</td>
      <td>
        请求的URL。
      </td>
      <td></td>
    </tr>
    <tr>
      <td>Timeout</td>
      <td>
        （可选）超时时间。如果超时到期，则执行将继续进入下一条语句或备用地址。<br>如果没有指定，请求将无限期等待。<br>超时必须设置在5 ms到15 ms（包含）之间。否则，将发生播放超时错误。<br>如果值超出此范围，`-9 (InvalidTimeout)`将存储在`状态 (status)`中。
      </td>
      <td>毫秒</td>
    </tr>
    <tr>
      <td>timeout fallback address</td>
      <td>
        （可选）超时发生时分支的地址。<br>如果没有指定，执行将继续进入下一个地址。
      </td>
      <td>地址</td>
    </tr>
  </tbody>
</table>

### Usage Example

```python
#case 1
var domain="http://192.168.1.200:8888"
cli.get domain+"/setting/max_torque"

#case 2
var url = domain+"/joints/max_speed"
cli.query = {axis: 3}
cli.get url, 10, *timeout
# cli.get(url, 10, *timeout) also possible
```