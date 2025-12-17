# get

### Description

Requests an HTTP GET service.

The server retrieves the information associated with the requested URL and returns it in the response.

The response data is stored in the `body` attribute.

### Syntax

&lt;HttpCli object&gt;.get &lt;URL string, timeout, timeout fallback address&gt;


### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Item</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Note</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>URL string</td>
      <td>
        The request URL.
      </td>
      <td></td>
    </tr>
    <tr>
      <td>Timeout</td>
      <td>
        (Optional) Timeout duration. If the timeout expires, execution proceeds to the next statement or to the fallback address.<br>If not specified, the request waits indefinitely.<br>The timeout must be set between 5 ms and 15 ms (inclusive). Otherwise, a playback timeout error occurs.<br>If the value is outside this range, `-9 (InvalidTimeout)` is stored in `status`. 
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>timeout fallback address</td>
      <td>
        (Optional) The address to branch to when a timeout occurs.<br>If not specified, execution proceeds to the next address.
      </td>
      <td>Address</td>
    </tr>
  </tbody>
</table>


### Usage Example

```python
#case 1
var domain="http://192.168.1.200:8888"
cli.get domain+"/setting/max_torque"

#case 2
var url = domain+"/joints/max_speed"
cli.query = {axis: 3}
cli.get(url)
```



