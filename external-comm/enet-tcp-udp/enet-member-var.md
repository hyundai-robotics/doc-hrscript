# 6.2.2 Member Variables

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
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>Allows reading/writing</p>
        <p>Designates or acquires the IP address of the communication counterpart</p>
        <p>Applicable only when calling the open statement</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">rport</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>Allows reading/writing</p>
        <p>Designates or acquires the port number of the communication counterpart
          (Remote)</p>
        <p>Applicable only when calling the open statement</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">lport</td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">
        <p>Allows reading/writing</p>
        <p>Used in UDP communication and ignored in TCP communication</p>
        <p>Designates or acquires the port number of the controller itself (Local)</p>
        <p>The default value is 0 (if not designated), in which case the controller&#x2019;s
          port number will be automatically created.</p>
        <p>Applicable only when calling the open statement</p>
      </td>
    </tr>
  </tbody>
</table>

