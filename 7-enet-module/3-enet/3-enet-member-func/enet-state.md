# state

### Description

Returns the state of the ethernet object.


### Syntax

`{ENet object}.state`


### Return value

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Misc.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>
        Connected. <br>
        (In case of UDP, even just an `open` is considered connected.<br>
         In the case of TCP, it is considered connected only when `listen`, `connect`, and `accept` are performed after `open`.
      </td>
      <td></td>
    </tr>
    <tr>
      <td>0</td>
      <td>Disconnected.</td>
      <td></td>
    </tr>
    <tr>
      <td>-1</td>
      <td>Failed in creating ethernet socket.</td>
      <td></td>
    </tr>
    <tr>
      <td>-2</td>
      <td>Failed in binding ethernet socket.</td>
      <td></td>
    </tr>
    <tr>
      <td>-3</td>
      <td>Failed to connect.</td>
      <td></td>
    </tr>
    <tr>
      <td>-4</td>
      <td>Failed to listen.</td>
      <td></td>
    </tr>
    <tr>
      <td>-5</td>
      <td>Failed to accept.</td>
      <td></td>
    </tr>
  </tbody>
</table>


### Example

```python
var ret = enet_to_sensor.state()
```

