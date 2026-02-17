# `delete`

### Description

Requests an HTTP DELETE service.

Deletes the specified resource.

The `body` attribute is not used for this request.

### Syntax

&lt;HttpCli object&gt;.delete &lt;URL string, timeout, timeout fallback address&gt;


### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Item</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Notes</th>
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
      <td>Timeout fallback address</td>
      <td>
        (Optional) The address to branch to when a timeout occurs.<br>If not specified, execution proceeds to the next address. 
      </td>
      <td>Address</td>
    </tr>
  </tbody>
</table>

### Usage Example

```python
var domain="http://192.168.1.200:8888"
cli.delete domain+"/items"
```

