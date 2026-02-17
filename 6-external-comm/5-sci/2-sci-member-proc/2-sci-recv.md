# recv

### Description

Call `Sci`'s `recv` to receive a string.


### Syntax

&lt;Sci object&gt;.recv string variable \[,{timeout}\] \[,{goto address}\]


### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Item</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Etc</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>string variable</td>
      <td>
        A string variable that will hold the entered string when successfully received.<br>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>timeout</td>
      <td>
        When no data is received for a specified time, it branches to the goto address, and if there is no goto address, an error occurs.<br>
        If not specified, it waits indefinitely.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>goto address</td>
      <td>
        Address to branch to when timeout occurs.<br>
        If not specified, it stops with an error.
      </td>
      <td>address</td>
    </tr>
  </tbody>
</table>


### Example

```python
   var msg
   sci2.recv msg,5000,*timeout
   print msg
   ...
   ...
   *timeout
   print "timeout error"
   stop
```



