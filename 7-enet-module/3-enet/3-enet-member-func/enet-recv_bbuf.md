# recv_bbuf

### Description

Receives binary data from the Ethernet object and stores it in the [BBuf](../../4-bbuf/README.md) object.


### Syntax

`{ENet object}.recv_bbuf {BBuf onject}[,{waiting time}][,{address on timeout}]`


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
      <td>BBuf object</td>
      <td>
        BBuf object to store the received binary data
      </td>
      <td></td>
    </tr>
    <tr>
      <td>waiting time</td>
      <td>
        timeout. If elapsed, proceed to the next command or jump to the address on timeout.<br>
        If not specified, wait ininfinitely.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>address on timeout</td>
      <td>
        address to which jump on timeout.<br>
        If not specified, proceed to next command.
      </td>
      <td>address</td>
    </tr>
  </tbody>
</table>


### Return value

The number of received data.


### Example

```python
var bbuf=enet_to_sensor.BBuf()
enet_to_sensor.recv bbuf
enet_to_sensor.recv bbuf, 5000
var nitem=enet_to_sensor.recv(bbuf,5000,*TimeOut)
end

*TimeOut
print "Time out! No response from sensor"
end
```

