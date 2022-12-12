# read_nums

### Description

Reads a specified number of numeric values from a specified position in the binary buffer and returns them in array format.


### Syntax

`{BBuf object}.read_num  {format},{offset},{n.item}`


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
      <td style="text-align:left">format</td>
      <td style="text-align:left">
			binary data format<sup>*</sup><br>
      e.g. "U4", "s2"
      </td>
      <td style="text-align:left">string</td>
    </tr>
	  <tr>
      <td style="text-align:left">offset</td>
      <td style="text-align:left">
        position at which to read the data (0-based byte offset)
      </td>
      <td style="text-align:left">integer</td>
    </tr>
    <tr>
      <td style="text-align:left">n.item</td>
      <td style="text-align:left">
        the number of data to read
      </td>
      <td style="text-align:left">integer</td>
    </tr>
  </tbody>
</table>

<br>


\* Refer to [7.4.2 Supported format](../2-format.md).
<br>
<br>


### Return value

* Array of numeric values read.
* If the number of data in the buffer is less than the specified number, only reads as many as there are.
* Returns an empty array if an error occurs when reading the data type.


### Example

```python
var bbuf=enet.BBuf()
bbuf.append("F8", 9.80665)
bbuf.append("U4", [2, 3, 5, 7, 11, 13])
print bbuf.read_nums("U4", 12, 3) # "[3, 5, 7]"
print bbuf.read_num("U4", 12, 6) # "[3, 5, 7, 11, 13]"
```
