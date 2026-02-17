# `删除 (delete)`

### 描述

请求 HTTP DELETE 服务。

删除指定的资源。

该 `body` 属性在此请求中不使用。

### 语法

&lt;HttpCli object&gt;.delete &lt;URL string, timeout, timeout fallback address&gt;


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
      <td>URL string</td>
      <td>
        请求的 URL。
      </td>
      <td></td>
    </tr>
    <tr>
      <td>Timeout</td>
      <td>
        (可选) 超时时间。如果超时到期，执行将继续到下一条语句或转到备用地址。<br>如果未指定，请求将无限期等待。<br>超时必须设置在 5 毫秒到 15 毫秒（含）之间。否则，将发生播放超时错误。<br>如果值超出此范围，则 `-9 (InvalidTimeout)` 将存储在 `状态 (status)` 中。
      </td>
      <td>毫秒</td>
    </tr>
    <tr>
      <td>Timeout fallback address</td>
      <td>
        (可选) 超时发生时的分支地址。<br>如果未指定，执行将继续到下一个地址。 
      </td>
      <td>地址</td>
    </tr>
  </tbody>
</table>
### 使用示例

```python
var domain="http://192.168.1.200:8888"
cli.delete domain+"/items"
```