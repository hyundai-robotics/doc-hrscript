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
      <td style="text-align:left">Any</td>
      <td style="text-align:left">
        <p>要传输的数据必须在PUT和POST请求之前分配。<br><br>如果给`body`分配了一个对象以外的值，执行时URL的最后路径段将被视为键。<br><br>GET和POST请求的响应数据存储在`body`中。<br><br>在HRScript中，不支持直接访问`body`的成员变量。要修改或使用数据，必须先将其分配给另一个变量。</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">query</td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">
        用于需要查询参数的GET服务。<br>与GET请求一起发送的数据必须预先分配。
      </td>
    </tr>
    <tr>
      <td style="text-align:left">status</td>
      <td style="text-align:left">int</td>
      <td style="text-align:left">
        <p>
            返回HTTP响应代码和错误代码。(请参阅[6.2.4节, HTTP通信代码](./4-http_cli-code.md))
          <br/>
        </p>
      </td>
    </tr>
  </tbody>
</table>

<br/>

`body`和`query`都使用对象数据类型。

对象类型支持`{ key: value }`格式。

```python
cli.body = { name: "WORK #32", color: "green", state: "OK" }
cli.query = { axis: 3 }
```