# read_num

### Description

Reads a numeric value from a specified position in the binary buffer, and returns it.


### Syntax

`{BBuf object}.read_num {format},{offset}`


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
      <td style="text-align:left">binary data format<sup>*</sup><br>
      e.g. "U4", "s2"<br>
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
  </tbody>
</table>

<br>

\* Refer to [7.4.2 Supported format](../2-format.md).
<br>
<br>

### Return value

* Numeric value read
* If an error occurs when reading the data type, it returns 0.


### Example

```python
var bbuf=enet.BBuf()
bbuf.append("F8", 9.80665)
bbuf.append("U4", [2, 3, 5, 7, 11, 13])
print bbuf.read_num("F8", 0) # "9.80665"
print bbuf.read_num("U4", 12) # "3"
print bbuf.read_num("U4", 16) # "5"
```
