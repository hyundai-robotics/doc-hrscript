# accept

### Description

As a server in Ethernet TCP communication, it waits for a connection request from the client side. Creates a connection when a request occurs.
Not used in UDP peer-to-peer communication.


### Syntax

`{ENet object}.accept [{waiting time}] [, {address on timeout}]`


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
        OK (completed)
      </td>
      <td></td>
    </tr>  
    <tr>
      <td>0</td>
      <td>
        waiting
      </td>
      <td></td>
    </tr>
    <tr>
      <td>-1</td>
      <td>timeout</td>
      <td></td>
    </tr>
    <tr>
      <td>-2</td>
      <td>error</td>
      <td></td>
    </tr>    
  </tbody>
</table>


### Example

```python
enet_to_sensor.listen
var ret=enet_to_sensor.accept(5000)
```

```python
enet_to_sensor.listen
enet_to_sensor.accept 5000,*TimeOut
```

