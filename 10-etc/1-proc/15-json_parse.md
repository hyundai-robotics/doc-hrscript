# 10.1.15 `json_parse`

Supported from V60.32-00

The `json_parse` procedure parses a JSON string to build an object, an array, or a value.

### Syntax

Right after the procedure starts, the `result()` function returns a result object used for checking the status and storing the result data.
```python
    json_parse <json string literal/value>
    var r = result()
```

You must wait for this procedure to complete.
```python
    wait r.status == "finished"
```

The result of parsing will be stored in `r.data`. An error may occur if the procedure is not allowed to finish before accessing the result.


##### status

<table>
  <thread>
    <th style="text-align:left">status</th>
    <th style="text-align:left">details</th>
  </thread>
  <tbody>
  <tr>
    <td style="text-align:left">parsing</td>
    <td style="text-align:left">The JSON string is still being parsed. The data cannot be used yet.</td>
  </tr>
  <tr>
    <td style="text-align:left">finished</td>
    <td style="text-align:left">JSON string parsing is complete. The data can now be used.</td>
  </tr>
  </tbody>
</table>



### Examples
```python
    json_parse "[1, 2, 3, 4]"
    var r = result()
    wait r.status == "finished", 10 # Wait for the process to complete, with a maximum timeout of 10 seconds.
    var jr = r.data   # The type of r.data is array
    print jr          # [1, 2, 3, 4] printed
```

```python
    json_parse "3.141592"
    var r = result()
    wait r.status == "finished", 10 # Wait for the process to complete, with a maximum timeout of 10 seconds.
    var jr = r.data    # The type of r.data is double
    print jr           # 3.141592 printed
```
```python
    json_parse "{\"test\": \"value\"}" # Double quotes must be escaped inside a JSON string.
    var r = result()
    wait r.status == "finished", 10 # Wait for the process to complete, with a maximum timeout of 10 seconds.
    var jr = r.data    # The type of r.data is JObject
    print jr           # { _type: "JObject", _sub_file: "", _desc: "", test: "value" } printed
```
