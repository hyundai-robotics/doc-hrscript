# `get`

### 描述

请求一个 HTTP GET 服务。

服务器检索与请求的 URL 相关的信息并在响应中返回。

响应数据存储在 `body` 属性中。

### 语法

&lt;HttpCli object&gt;.get &lt;URL string, timeout, timeout fallback address&gt;


### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">项</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
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
        （可选）超时持续时间。如果超时到期，则执行进入下一条语句或转到后备地址。<br>如果未指定，请求将无限等待。<br>超时时间必须设置在 5 毫秒和 15 毫秒（含）之间。否则，将发生播放超时错误。<br>如果值超出此范围，`-9 (InvalidTimeout)` 将存储在 `状态 (status)` 中。 
      </td>
      <td>毫秒</td>
    </tr>
    <tr>
      <td>timeout fallback address</td>
      <td>
        （可选）发生超时时转向的地址。<br>如果未指定，执行将进入下一个地址。
      </td>
      <td>地址</td>
    </tr>
  </tbody>
</table>
### 使用示例

```python
#案例 1
var domain="http://192.168.1.200:8888"
cli.get domain+"/setting/max_torque"

#案例 2
var url = domain+"/joints/max_speed"
cli.query = {axis: 3}
cli.get url, 10, *timeout
# cli.get(url, 10, *timeout) 也可能
```