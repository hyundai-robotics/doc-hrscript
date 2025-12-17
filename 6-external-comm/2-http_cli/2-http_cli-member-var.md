# 6.2.2 Member Variables

<table>
  <thead>
    <tr>
      <th style="text-align:left">Variable</th>
      <th style="text-align:left">Data Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">body</td>
      <td style="text-align:left">Any</td>
      <td style="text-align:left">
        <p>The data to be transmitted must be assigned in advance for PUT and POST requests.<br><br>If a value other than an object is assigned to `body`, the last path segment of the URL is treated as the key during execution.<br><br>The response data from GET and POST requests is stored in `body`.<br><br>In HRScript, direct access to the member variables of `body` is not supported. To modify or use the data, assign it to another variable first.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">query</td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">
        Used for GET services that require query parameters.<br>The data to be sent with a GET request must be assigned in advance.
      </td>
    </tr>
    <tr>
      <td style="text-align:left">status</td>
      <td style="text-align:left">int</td>
      <td style="text-align:left">
        <p>
            Returns the HTTP response code and error code. (See Section [6.2.4, HTTP Communication Codes](./4-http_cli-code.md))
          <br/>
        </p>
      </td>
    </tr>
  </tbody>
</table>

<br/>

Both `body` and `query` use the object data type.

The object type is supported in the `{ key: value }` format.

```python
cli.body = { name: "WORK #32", color: "green", state: "OK" }
cli.query = { axis: 3 }
```

