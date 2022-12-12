# listen

### Description

As a server in Ethernet TCP communication, it prepares for a connection request from the client side. 
Not used in UDP peer-to-peer communication.


### Syntax

`{ENet object}.listen [{backlog}]`


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
      <td>backlog</td>
      <td>
        The permitted connection of the pending connection which is not acceptted.<br>
        If not specified, wait ininfinitely.
      </td>
      <td></td>
    </tr>
  </tbody>
</table>


### Return value

<table>
  <thead>
    <tr>
      <th style="text-align:left">Value</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Misc.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>
        OK
      </td>
      <td></td>
    </tr>
    <tr>
      <td>-1</td>
      <td>error</td>
      <td></td>
    </tr>	 
  </tbody>
</table>


### Example

```python
enet_to_sensor.listen
enet_to_sensor.accept 5000,*TimeOut
```
