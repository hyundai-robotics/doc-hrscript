# `post`

### Description

请求 HTTP POST 服务。

创建指定的资源。

要传输的数据必须提前分配给 `body` 属性。

远程服务器返回的响应数据存储在 `body` 属性中。

### Syntax

&lt;HttpCli object&gt;.post &lt;URL string, timeout, timeout fallback address&gt;

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">项目</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>URL string</td>
      <td>
      请求 URL。
      </td>
      <td></td>
    </tr>
    <tr>
      <td>Timeout</td>
      <td>
        （可选）超时时间。如果超时到期，执行将继续到下一个语句或后备地址。<br>如果未指定，请求将无限期等待。<br>超时必须设置在 5 ms 和 15 ms（包括）之间。否则，将发生播放超时错误。<br>如果值超出此范围，`-9 (InvalidTimeout)` 将存储在 `状态 (status)` 中。
      </td>
      <td>毫秒</td>
    </tr>
    <tr>
      <td>timeout fallback address</td>
      <td>
        （可选）发生超时时的分支地址。<br>如果未指定，执行将继续到下一个地址。
      </td>
      <td>地址</td>
    </tr>
  </tbody>
</table>

### Usage Example 

```python
#case 1
var domain="http://192.168.1.200:8888"
cli.body={ name: "WORK #32", color: "green", state: "OK" }
cli.post domain+"/display/update"

#case 2
var url = domain+"/display/update"
cli.post url, 10, *TimeOut
```