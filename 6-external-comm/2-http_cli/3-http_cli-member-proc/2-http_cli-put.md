# `put`

### 描述

请求 HTTP PUT 服务。

更新指定的资源。

要传输的数据必须提前分配给 `body` 属性。

### 语法

&lt;HttpCli 对象&gt;.put &lt;URL 字符串, 超时, 超时回退地址&gt;


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
        （可选）超时持续时间。如果超时到期，执行将继续到下一条语句或回退地址。<br>如果未指定，请求将无限期等待。<br>超时时间必须设置在 5 毫秒到 15 毫秒之间（包括）。否则将发生播放超时错误。<br>如果值超出此范围，`-9 (InvalidTimeout)` 将存储在 `状态 (status)` 中。
      </td>
      <td>毫秒</td>
    </tr>
    <tr>
      <td>超时回退地址</td>
      <td>
        （可选）发生超时时要跳转的地址。<br>如果未指定，执行将继续到下一个地址。
      </td>
      <td>地址</td>
    </tr>
  </tbody>
</table>
### 使用示例

```python
#案例 1
var domain="http://192.168.1.200:8888"
cli.body=500
cli.put domain+"/setting/max_torque"

#案例 2
var url = domain + "/setting"
cli.body = {max_torque: 500}
cli.put(url, 10, S1)
```