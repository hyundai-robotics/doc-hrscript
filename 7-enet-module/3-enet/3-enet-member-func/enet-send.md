# send

### Description

Send string data to ethernet object.


### Syntax

`{ENet object}.send {msg}`



### Parameters

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
      <td style="text-align:left">msg</td>
      <td style="text-align:left">
        string to send
      </td>
      <td style="text-align:left">string</td>
    </tr>
  </tbody>
</table>


### Return value

The number of bytes sent.


### Example

```python
enet_to_sensor.send "rob:"+10+", command:"+cmd+"\n"
```



