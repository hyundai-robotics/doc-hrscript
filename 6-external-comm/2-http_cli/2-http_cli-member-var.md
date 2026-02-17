# 6.2.2 成员变量

<table>
  <thead>
    <tr>
      <th style="text-align:left">变量</th>
      <th style="text-align:left">数据类型</th>
      <th style="text-align:left">描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">body</td>
      <td style="text-align:left">任意</td>
      <td style="text-align:left">
        <p>传输的数据必须在 PUT 和 POST 请求之前分配。<br><br>如果将对象以外的值分配给 `body`，在执行期间 URL 的最后路径段将作为键处理。<br><br>来自 GET 和 POST 请求的响应数据存储在 `body` 中。<br><br>在 HRScript 中，不支持直接访问 `body` 的成员变量。要修改或使用数据，首先将其分配给另一个变量。</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">query</td>
      <td style="text-align:left">对象</td>
      <td style="text-align:left">
        用于需要查询参数的 GET 服务。<br>与 GET 请求一起发送的数据必须提前分配。
      </td>
    </tr>
    <tr>
      <td style="text-align:left">status</td>
      <td style="text-align:left">int</td>
      <td style="text-align:left">
        <p>
            返回 HTTP 响应代码和错误代码。 (请参见 [6.2.4 节，HTTP 通信代码](./4-http_cli-code.md))
          <br/>
        </p>
      </td>
    </tr>
  </tbody>
</table>

<br/>

`body` 和 `query` 都使用对象数据类型。

对象类型以 `{ key: value }` 格式支持。

cli.body = { name: "WORK #32", color: "green", state: "OK" }
cli.query = { axis: 3 }