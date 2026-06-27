# 7.3.2 `ENet` 成员变量

<table>
  <thead>
    <tr>
      <th style="text-align:left">变量名</th>
      <th style="text-align:left">数据类型</th>
      <th style="text-align:left">描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">ip_addr</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        可读/可写<br>
        设置或获取通信对手（远程）的 IP 地址。<br>
        仅在调用 open 语句时应用。
      </td>
    </tr>
    <tr>
      <td style="text-align:left">rport</td>
      <td style="text-align:left">number</td>
      <td style="text-align:left">
        可读/可写<br>
        设置或获取通信对手（远程）的端口号。<br>
        仅在调用 open 语句时应用。
      </td>
    </tr>
    <tr>
      <td style="text-align:left">lport</td>
      <td style="text-align:left">number</td>
      <td style="text-align:left">
        可读/可写<br>
        仅在 UDP 对等和 TCP 服务器中使用，在 TCP 客户端中被忽略。<br>
        设置或获取控制器自己的（本地）端口号。<br>
        默认值为 0（如果未指定），在这种情况下，此端口号将自动生成。<br>
        仅在调用 open 语句时应用。<br>
        控制器上的 50000-50005 端口是预分配的 lports，无法使用。
      </td>
    </tr>
  </tbody>
</table>