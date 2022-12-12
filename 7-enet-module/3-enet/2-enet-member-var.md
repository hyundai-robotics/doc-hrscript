# 7.3.2 ENet member variable

<table>
  <thead>
    <tr>
      <th style="text-align:left">Variable name</th>
      <th style="text-align:left">Data type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">ip_addr</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        readable/writable<br>
        Set or get the IP address of the communication opponent(remote).<br>
        Applied only when calling the open statement.
      </td>
    </tr>
    <tr>
      <td style="text-align:left">rport</td>
      <td style="text-align:left">number</td>
      <td style="text-align:left">
        readable/writable<br>
        Set or get the port number of the communication opponent(remote).<br>
        Applied only when calling the open statement.
      </td>
    </tr>
    <tr>
      <td style="text-align:left">lport</td>
      <td style="text-align:left">number</td>
      <td style="text-align:left">
        readable/writable<br>
        Only used in UDP peer-to-peer and TCP server, ignored in TCP client.<br>
        Set or get the controller's own (local) port number.<br>
        The default value is 0 (if not specified), in which case this port number is automatically generated.<br>
        Applied only when calling the open statement.
      </td>
    </tr>
  </tbody>
</table>

