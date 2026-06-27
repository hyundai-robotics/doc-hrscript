# `put`

### Description

请求一个 HTTP PUT 服务。

更新指定的资源。

要传输的数据必须事先分配给 `body` 属性。

### Syntax

&lt;HttpCli object&gt;.put &lt;URL string, timeout, timeout fallback address&gt;

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
        请求的 URL。
      </td>
      <td></td>
    </tr>
    <tr>
      <td>Timeout</td>
      <td>
        （可选）超时时间。 如果超时到期，执行将继续到下一个语句或备用地址。<br>如果未指定，请求将无限期等待。<br>超时时间必须设定在 5 ms 到 15 ms 之间（包括）。 否则，将发生播放超时错误。<br>如果值超出此范围，则 `-9 (InvalidTimeout)` 被存储在 `状态 (status)` 中。
      </td>
      <td>毫秒</td>
    </tr>
    <tr>
      <td>timeout fallback address</td>
      <td>
        （可选）在发生超时时跳转的地址。<br>如果未指定，执行将继续到下一个地址。
      </td>
      <td>地址</td>
    </tr>
  </tbody>
</table>

### Usage Example

```python
#case 1
var domain="http://192.168.1.200:8888"
cli.body=500
cli.put domain+"/setting/max_torque"

#case 2
var url = domain + "/setting"
cli.body = {max_torque: 500}
cli.put(url, 10, S1)
```