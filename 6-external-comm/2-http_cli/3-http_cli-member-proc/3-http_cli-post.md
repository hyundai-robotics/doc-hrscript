# `post`

### 描述

请求一个 HTTP POST 服务。

创建指定的资源。

要传输的数据必须提前分配给 `body` 属性。

远程服务器返回的响应数据存储在 `body` 属性中。

### 语法

&lt;HttpCli object&gt;.post &lt;URL string, timeout, timeout fallback address&gt;

### 参数

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
      <td>URL 字符串</td>
      <td>
      请求的 URL。
      </td>
      <td></td>
    </tr>
    <tr>
      <td>超时</td>
      <td>
        （可选）超时持续时间。如果超时过期，执行将继续到下一个语句或回退地址。<br>如果未指定，请求将无限期等待。<br>超时必须设置在 5 毫秒到 15 毫秒（包含）之间。否则，将发生播放超时错误。<br>如果值超出此范围，将在 `状态 (status)` 中存储 `-9 (InvalidTimeout)`。
      </td>
      <td>毫秒</td>
    </tr>
    <tr>
      <td>超时回退地址</td>
      <td>
        （可选）超时发生时要分支到的地址。<br>如果未指定，执行将继续到下一个地址。
      </td>
      <td>地址</td>
    </tr>
  </tbody>
</table>
### 使用示例 

```python
#案例 1
var domain="http://192.168.1.200:8888"
cli.body={ name: "WORK #32", color: "green", state: "OK" }
cli.post domain+"/display/update"

#案例 2
var url = domain+"/display/update"
cli.post url, 10, *TimeOut
```